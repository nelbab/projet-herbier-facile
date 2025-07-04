# 🎴 Développement applications mobiles 🌷


## 🔭 1. Objectifs

- Créer des applications `Android` et `iOS`.
- Faciliter l'utilisation directement sur le terrain.

## 📖 2. Points à vérifier pour Capacitor

- `Capacitor` n'accepte pas les API directement.
- Un projet `Next js` est bien adapté à l'utilisation de `Capacitor`.
- Fonctionnement particulier pour le traitement des photos
- Images enregistrées sur le serveur sont déjà optimisées pour la version mobiles.
- Possibilité de créer une application Android et une application iOS.

## 👩‍💻 3. Modifications apportées au projet

- Création d'un service API pour la gestion des appels API suivant si c'est l'application Web ou l'application mobile.<br />
Exemple d'un GET :
```
  async get<T>(endpoint: string, options: FetchOptions = {}): Promise<T> {
    const url = this.getUrl(endpoint);
    
    const response = await this.fetchWithTimeout(url, {
      method: 'GET',
      headers: this.getDefaultHeaders(),
      ...options,
    });

    return this.handleResponse<T>(response);
  }
```
```
// Récupérer une plante par ID
  getByIdPlante: (id: string) => apiService.get<Plante>(`/plante/${id}`),
```
- Ajout upload d'images spécifique pour mobile.
```
{/* Boutons pour mobile (Capacitor) */}
{isCapacitor && (
    <div className="flex gap-4 mb-4">
        <Button
            type="button"
            onClick={() => handleTakePicture(formik.setFieldValue)}
            className="flex items-center gap-2 bg-[#318d45] text-white"
            size="sm"
        >
            <CameraIcon className="h-5 w-5" />
            Prendre une photo
        </Button>
        <Button
            type="button"
            onClick={() => handleSelectFromGallery(formik.setFieldValue)}
            className="flex items-center gap-2 bg-[#318d45] text-white"
            size="sm"
        >
            <PhotoIcon className="h-5 w-5" />
            Choisir depuis la galerie
        </Button>
    </div>
)}
```

## 📑 4. Tests

- Ils sont effectués à l'aide d'`Android studio`.


## 🛠️ 5. Technologies utilisées

<a href="https://capacitorjs.com/" target="_blank"><img style="margin: 10px" src="images/capacitor.png" alt="Capacitor" title="Capacitor" height="50" /></a>
<a href="https://nextjs.org/" target="_blank"><img style="margin: 10px" src="images/nextjs.png" alt="NextJS" title="NextJS" height="50" /></a>
<a href="https://developer.android.com/studio?hl=fr" target="_blank"><img style="margin: 10px" src="images/android.png" alt="android studio" title="android studio" height="50" /></a>


## 🎯 6. Conclusion

