# 🌿 Conception 🌷

<br />
La création de cette application web d'herbier facile me permet de concevoir un outil numérique pratique pour répertorier, organiser et consulter une collection de plantes, d'herbes ou d'espèces botaniques. L'objectif est de créer une interface simple et intuitive, accessible à tous, y compris aux débutants en botanique.<br /> 
Voici une présentation générale pour la conception d'une telle application : <br /><br />

## 1. 🚀 Objectifs de l'application

###    • Facilité d'utilisation : 
Permettre aux utilisateurs de créer et gérer un herbier numérique sans compétences techniques.
###    • Référencement des plantes : 
Offrir un moyen pratique de cataloguer les plantes, avec des informations comme le nom commun, le nom latin, la description,  la famille, la catégorie, l'image, la comestibilité, la localisation ou la date de l’image.
###    • Accessibilité : 
Permettre un accès facile sur différents appareils (ordinateurs, tablettes, smartphones) via un navigateur web.
###     • Partage et visibilité publique : 
Permettre aux utilisateurs de rendre certaines fiches et photos accessibles à tous via des pages publiques dédiées (consultables sans authentification).
<br /><br />

## 2. 💡 Fonctionnalités principales

###    • Création de fiches de plantes : Les utilisateurs peuvent ajouter une plante à leur herbier avec les détails suivants :

        ◦ Nom commun et latin
        ◦ Description physique
        ◦ Catégorie
        ◦ Famille
        ◦ Type
        ◦ Image de la plante
        ◦ Date et lieu de l'image
        ◦ Comestibilité.
###    • Recherche et filtrage : 
Implémenter une fonctionnalité de recherche avancée permettant aux utilisateurs de trouver facilement une plante en fonction de critères (nom, catégorie, localisation, etc...).
###    • Interface conviviale : 
Une interface simple avec un tableau de bord clair pour gérer les plantes et les informations associées. Cela inclut des boutons clairs pour ajouter, modifier ou supprimer des fiches, ainsi qu'une vue en liste de l’herbier.
###    • Gestion des utilisateurs : 
Les utilisateurs peuvent créer des comptes pour enregistrer et synchroniser leurs herbiers en ligne. 
###    • Sauvegarde et exportation : 
Les utilisateurs peuvent exporter leur herbier sous forme de fichier PDF ou CSV pour le conserver en local ou le partager facilement.
###    • Publication publique
Les utilisateurs peuvent sélectionner une fiche ou une photo et la publier.
- Les éléments publiés apparaissent automatiquement dans :
    - la page Herbier public (liste de toutes les plantes rendues publiques),
    - la page Fiche de plante publique (détail d’une plante partagée),
    - la page Galerie de photos publique (vignettes de toutes les photos publiques).
- Un badge « public » distingue visuellement les contenus partagés.
- Les visiteurs non‑connectés peuvent consulter, mais pas modifier, ces contenus.
<br /><br />

## 3. 🛠️ Technologies utilisées

###    • Frontend (interface utilisateur) : 
Utilisation de technologies modernes telles que HTML5, TypeScript avec les frameworks comme Next.Js, React, Taiwind CSS  pour construire une interface dynamique et interactive.
###    • Backend (gestion des données) : 
Un serveur basé sur Node.js avec Next.Js, et l'ORM Prisma pour gérer les requêtes des utilisateurs, les données des plantes, les comptes utilisateurs, etc.
###    • Base de données : 
Une base de données relationnelle MySQL, pour stocker les informations relatives aux plantes et aux utilisateurs.
###    • Hébergement et déploiement : 
Utilisation du service AWS pour l'hébergement de l'application, offrant ainsi une solution scalable et accessible à tous.
<br /><br />

## 4. 🧩 Maquettes de l'application

L'interface doit être claire, simple et agréable à utiliser. Voici les éléments clés de la maquette :
###    • Page d'accueil : 
Présentation générale de l'application et bouton de connexion/inscription.
###    • Page dashboard : 
Affichage des plantes ajoutées, avec des options pour en ajouter de nouvelles ou les modifier.
###    • Page prolile : 
Permet de modifier les informations du profile ou le supprimer.
###    • Page de fiche de plante : 
Un formulaire de saisie facile à utiliser, avec des champs pour les informations nécessaires, et la possibilité de télécharger une photo.
###    • Page de herbier: 
Affichage la liste des plantes.
###    • Page de gallerie de photos : 
Affichage des plantes en gallerie pour avoir une vue globale.
###    • Page de herbier Administrateur : 
Affichage la liste des plantes et les gérer (exemple supprimer les photos et fiches non conformes).
###    • Page de gallerie Administrateur : 
Affichage des plantes en gallerie pour avoir une vue globale et les gérer (exemple supprimer les photos et fiches non conformes).
###    • Page prolile Administrateur : 
Permet de modifier les informations des profiles, changer le role ou les supprimer.
###    • Page Herbier public
Liste filtrable de toutes les fiches publiques.
###    • Page Fiche de plante publique
Vue détail d’une fiche partagée (URL partageable).
###    • Page Galerie de photos publique
Galerie responsive des images publiques permettant d'avoir un apperçu des images publiques.
<br /><br />

## 5. 📝 Étapes de développement

###    • Phase 1 : Planification : 
Définir précisément les fonctionnalités nécessaires et les exigences techniques. Concevoir les maquettes de l'interface.
###    • Phase 2 : Développement Frontend : 
Créer l'interface utilisateur (UI) avec un design simple et responsive.
###    • Phase 3 : Développement Backend : 
Créer la logique serveur pour gérer les utilisateurs, les herbiers et la base de données.
###    • Phase 4 : Test : 
Tester l'application sur différents appareils et navigateurs pour s'assurer de son bon fonctionnement.
###    • Phase 5 : Lancement et maintenance : 
Déployer l'application et effectuer des mises à jour régulières en fonction des retours des utilisateurs.
<br /><br />

## 6. 🎯 Conclusion

Cette application d'herbier simple et intuitive permet de rapprocher le monde de la botanique des utilisateurs débutants ou passionnés, tout en offrant une solution pratique pour la gestion et les connaissances sur les plantes.<br />
En offrant la possibilité de partager facilement leurs découvertes via des pages publiques, ce qui renforce la dimension collaborative et pédagogique du projet. 