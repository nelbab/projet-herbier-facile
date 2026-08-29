# 📊 Statistiques du tableau de bord

## ✨ Présentation

Le tableau de bord d'**Herbier Facile** a été enrichi avec un module de statistiques permettant à l'utilisateur d'obtenir une vue synthétique de son herbier.

L'objectif est de rendre les données de l'herbier plus facilement exploitables grâce à plusieurs indicateurs calculés automatiquement à partir des plantes enregistrées.

Cette fonctionnalité permet notamment de connaître la composition de son herbier, sa diversité botanique, la répartition des plantes et son évolution récente.

---

## 🎯 Objectifs

L'ajout des statistiques répond à plusieurs objectifs :

* offrir une vision globale de l'herbier ;
* mettre en valeur les données enregistrées par l'utilisateur ;
* fournir des indicateurs simples et immédiatement compréhensibles ;
* éviter une navigation dans les différentes fiches pour obtenir ces informations ;
* proposer une fonctionnalité dynamique, actualisée à partir des données de l'utilisateur.

---

## 📈 Les indicateurs

Le tableau de bord présente actuellement **8 indicateurs principaux**.

### 🌿 Nombre de plantes

Affiche le nombre total de plantes présentes dans l'herbier.

> **Exemple :** 42 plantes dans l'herbier

---

### 🏷️ Familles botaniques

Indique le nombre de familles différentes représentées dans l'herbier.

La famille la plus représentée est également affichée avec son nombre d'occurrences.

> **Exemple :**
> 18 familles différentes
> Top : *Asteraceae* (7)

---

### 🌍 Plantes publiques

Indique le nombre de plantes de l'herbier configurées comme publiques.

Cet indicateur permet de visualiser rapidement la partie de l'herbier rendue accessible publiquement.

---

### ✅ Plantes validées

Affiche le nombre de plantes ayant été validées.

Cet indicateur permet de distinguer les fiches validées des autres fiches enregistrées dans l'herbier.

---

### ☀️ Ajouts récents

Compte les plantes ajoutées au cours des **30 derniers jours**.

Cette statistique permet de visualiser l'activité récente de l'utilisateur dans son herbier.

La période est calculée dynamiquement à partir de la date courante.

---

### ✨ Plantes comestibles

Indique le nombre de plantes identifiées comme comestibles.

Le calcul utilise la valeur `OUI` du champ `comestible`.

Les valeurs sont normalisées avant comparaison afin de rendre le calcul plus robuste.

---

### 📑 Catégories

Affiche le nombre de catégories différentes présentes dans l'herbier.

La catégorie la plus représentée est également indiquée avec son nombre d'occurrences.

> **Exemple :**
> 6 catégories différentes
> Top : *Arbuste* (12)

---

### 📍 Départements

Indique le nombre de départements différents associés aux plantes de l'herbier.

Le département le plus représenté est également affiché.

> **Exemple :**
> 4 départements différents
> Top : *Maine-et-Loire* (15)

---

## ⚙️ Fonctionnement technique

Les statistiques sont calculées à partir des plantes de l'utilisateur.

Lors du chargement du dashboard, l'application récupère :

1. les 10 dernières plantes pour l'affichage du carrousel ;
2. la dernière plante ajoutée ;
3. l'ensemble des plantes nécessaires au calcul des statistiques.

Les données utilisées pour les statistiques sont stockées dans un état React dédié :

```typescript
const [statsPlantes, setStatsPlantes] = useState<Plante[]>([]);
```

Les statistiques sont ensuite calculées avec `useMemo`.

```typescript
const stats = useMemo(() => {
    const total = statsPlantes.length;

    const famillesUniques = new Set(
        statsPlantes
            .map((p) => p.famille)
            .filter((f) => !!f)
    ).size;

    // ...

    return {
        total,
        famillesUniques,
        publiques,
        validees,
        recentes,
        comestibles,
        topFamille,
        topCategorie,
        topDepartement,
        categoriesUniques,
        departementsUniques,
    };
}, [statsPlantes]);
```

L'utilisation de `useMemo` permet de mémoriser le résultat et d'éviter de recalculer inutilement les statistiques lorsque les données des plantes n'ont pas changé.

---

## 🔎 Calcul des valeurs les plus représentées

Une fonction générique a été créée afin de rechercher la valeur la plus fréquente d'un champ texte.

```typescript
const topValue = (
    getField: (p: Plante) => string | undefined | null
) => {
    const counts = new Map<string, number>();

    statsPlantes.forEach((p) => {
        const value = getField(p)?.trim();

        if (!value) return;

        counts.set(
            value,
            (counts.get(value) || 0) + 1
        );
    });

    // Recherche de la valeur la plus fréquente
};
```

Cette fonction est réutilisée pour plusieurs données :

```typescript
const topFamille = topValue((p) => p.famille);
const topCategorie = topValue((p) => p.categorie);
const topDepartement = topValue((p) => p.departement);
```

Cette approche permet d'éviter de dupliquer la logique de comptage pour chaque statistique.

---

## 🧮 Gestion des données

Les valeurs uniques sont calculées avec `Set`.

Par exemple, pour les familles :

```typescript
const famillesUniques = new Set(
    statsPlantes
        .map((p) => p.famille)
        .filter((f) => !!f)
).size;
```

Le même principe est utilisé pour les catégories et les départements.

Pour les plantes ajoutées récemment, une date correspondant aux 30 derniers jours est calculée puis comparée à la date d'ajout de chaque plante.

```typescript
const trenteJoursAgo = new Date();

trenteJoursAgo.setDate(
    trenteJoursAgo.getDate() - 30
);
```

---

## 🖥️ Interface utilisateur

Les statistiques sont intégrées directement dans le tableau de bord sous la forme de cartes.

Chaque carte contient :

* une icône permettant d'identifier rapidement le type d'information ;
* la valeur principale ;
* éventuellement une information complémentaire ;
* le libellé de la statistique.

La mise en page utilise une grille responsive :

```text
┌──────────────┬──────────────┬──────────────┬──────────────┐
│ 🌿           │ 🏷️           │ 🌍           │ ✅           │
│     42       │     18       │     25       │     37       │
│   Plantes    │   Familles   │  Publiques   │   Validées   │
├──────────────┼──────────────┼──────────────┼──────────────┤
│ ☀️           │ ✨           │ 📑           │ 📍           │
│      5       │     12       │      6       │      4       │
│ 30 derniers  │ Comestibles  │ Catégories   │ Départements │
└──────────────┴──────────────┴──────────────┴──────────────┘
```

La grille s'adapte à la taille de l'écran afin de conserver une présentation utilisable sur ordinateur comme sur mobile.

---

## ⏳ Gestion du chargement

Pendant le chargement des données, les valeurs statistiques sont remplacées par un indicateur de chargement.

Cela évite d'afficher temporairement des valeurs incorrectes ou de donner l'impression que l'utilisateur possède zéro plante.

```typescript
{dataLoading ? (
    <div className="animate-spin ..."></div>
) : (
    <span>
        {stats.total}
    </span>
)}
```

---

## 🧠 Choix techniques

Cette fonctionnalité m'a permis de mettre en œuvre plusieurs mécanismes de React et TypeScript :

* `useState` pour gérer les données ;
* `useEffect` pour déclencher le chargement des données ;
* `useCallback` pour mémoriser la fonction de chargement ;
* `useMemo` pour optimiser le calcul des statistiques ;
* `Set` pour déterminer le nombre de valeurs uniques ;
* `Map` pour compter les occurrences ;
* TypeScript pour typer les données et les fonctions ;
* Tailwind CSS pour la mise en forme responsive ;
* Heroicons pour représenter visuellement les différents indicateurs.

---

## ⚠️ Évolution possible

Actuellement, les statistiques sont calculées à partir des plantes récupérées pour l'utilisateur.

Une évolution possible serait de créer des **endpoints dédiés aux statistiques côté backend**.

Cela permettrait notamment d'éviter de récupérer toutes les plantes uniquement pour calculer des compteurs.

Par exemple :

```text
GET /api/plante/stats
```

Le backend pourrait alors effectuer directement les agrégations nécessaires et retourner uniquement les données utiles au dashboard.

Cette évolution serait particulièrement intéressante lorsque le volume de plantes devient important.

---

## 🚀 Résultat

L'ajout de ce module transforme le tableau de bord en véritable **vue synthétique de l'herbier**.

L'utilisateur peut désormais visualiser immédiatement :

* la taille de son herbier ;
* sa diversité botanique ;
* la visibilité de ses plantes ;
* leur état de validation ;
* son activité récente ;
* le nombre de plantes comestibles ;
* la diversité des catégories ;
* la répartition géographique.

Cette fonctionnalité améliore ainsi la lisibilité des données et apporte une dimension plus dynamique et informative au tableau de bord d'**Herbier Facile**.
