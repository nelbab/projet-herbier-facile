# 🎴 Développement applications mobiles 🌷

## ✨ Introduction
Ce document présente la démarche d’intégration de `Capacitor` dans un projet web développé avec `Next.js`, dans le but de générer des applications mobiles natives pour `Android` et `iOS`. Il met en avant les choix techniques, les adaptations spécifiques au mobile (notamment la gestion des images), ainsi que les résultats obtenus à travers des tests sur différents environnements.
<br><br>

## 🔭 1. Objectifs

- Créer des applications `Android` et `iOS`.
- Faciliter l'utilisation directement sur le terrain.
<br><br>

## 📖 2. Points à vérifier pour Capacitor

- `Capacitor` n'accepte pas les API directement.
- Un projet `Next js` est bien adapté à l'utilisation de `Capacitor`.
- Fonctionnement particulier pour le traitement des photos
- Images enregistrées sur le serveur sont déjà optimisées pour la version mobiles.
- Possibilité de créer une application Android et une application iOS.
<br><br>

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
<br><br>

## 📑 4. Tests

### a. Les tests ont été réalisés dans deux environnements :

📱 Smartphone réel : Samsung Galaxy SM-M135F (Android 13).

💻 Émulateur : Android Studio – API 34 (UpsideDownCake, Android 14.0).

### b. Fonctionnalités testées :
- Chargement de l’application
- Authentification
- Navigation générale
- Affichage des fiches, de l'herbier, de la galerie photos
- Prise de photo avec l’appareil
- Sélection d’une image depuis la galerie
- Envoi des données au serveur

Tous les tests se sont déroulés correctement et ont validé le bon fonctionnement des principales fonctionnalités.

**Les tests iOS seront effectués ultérieurement**, une fois le projet ouvert et configuré sur un environnement macOS avec Xcode.
<br><br>


## 🛠️ 5. Technologies utilisées

<a href="https://capacitorjs.com/" target="_blank"><img style="margin: 10px" src="images/capacitor.png" alt="Capacitor" title="Capacitor" height="50" /></a>
<a href="https://nextjs.org/" target="_blank"><img style="margin: 10px" src="images/nextjs.png" alt="NextJS" title="NextJS" height="50" /></a>
<a href="https://developer.android.com/studio?hl=fr" target="_blank"><img style="margin: 10px" src="images/android.png" alt="android studio" title="android studio" height="50" /></a>
<br><br>

## 🚀 6. Build et publication
La génération des applications mobiles s’effectue avec les commandes `Capacitor` :
- ```npx cap build android``` → pour générer l’application Android
- ```npx cap build ios``` → pour générer l’application iOS (via Xcode sur macOS)

Les étapes de déploiement comprennent :
- Ouverture du projet dans `Android Studio` ou `Xcode`
- Signature de l’application
- Génération d’un fichier .apk (Android) ou .ipa (iOS)
- Publication via Google Play Console ou Apple App Store Connect

### ➕ Remarque

Le projet iOS a été initialisé, mais **n’a pas encore été testé ni finalisé**.  
👉 **Les étapes de build, test et publication sur l’App Store seront réalisées prochainement**, lorsque l’environnement de développement iOS sera opérationnel.
<br><br>

## 🔧 7. Scripts NPM et commandes Capacitor
L'intégration mobile repose sur une série de commandes définies dans le fichier package.json, facilitant le développement, le test, la synchronisation, et le build de l'application.

### a. Scripts principaux :
Extrait du package.json :
```
"scripts": {
  "dev": "next dev",
  "dev:mobile": "cross-env NEXT_BUILD_TARGET=export next dev",
  "build": "next build",
  "build:export": "cross-env NEXT_BUILD_TARGET=export next build && next export",
  "start": "next start",
  "cap:sync": "npx cap sync",
  "cap:run:android": "npx cap sync android && npx @capacitor/assets generate && npx cap run android",
  "cap:run:ios": "npx cap sync ios && npx @capacitor/assets generate && npx cap run ios",
  "cap:open:android": "npx cap sync android && npx @capacitor/assets generate && npx cap open android",
  "cap:open:ios": "npx cap sync ios && npx @capacitor/assets generate && npx cap open ios",
  "cap:dev:android": "npx @capacitor/assets generate && npx cap run android --live-reload",
  "cap:dev:ios": "npx @capacitor/assets generate && npx cap run ios --live-reload",
}
```
### b. Ces scripts permettent notamment :

- de compiler l'application en mode export (build:export)
- de lancer l’app en live-reload sur un périphérique mobile (cap:dev:*)
- de synchroniser et ouvrir le projet dans Android Studio ou Xcode (cap:open:*)
<br><br>

## ⚙️ 8. Configuration Capacitor
La configuration de `Capacitor` est définie dans capacitor.config.ts. Elle inclut :
l’ID de l'application (com.herbierfacile.app)

- le nom (Herbier Facile)
- la source web (out, via next export)
- les permissions, icônes et splashscreens
- les options spécifiques `Android` et `iOS`
- les icônes sont générées automatiquement pour `Android` et `iOS`

capacitor.config.ts :
```
const config: CapacitorConfig = {
  appId: "com.herbierfacile.app",
  appName: "Herbier Facile",
  webDir: "out",

  server: {
    url: "https://herbier-facile.fr", 
    cleartext: false
  },

  plugins: {
    Camera: {
      permissions: ['camera', 'photos'],
      androidPresentationStyle: 'fullscreen'
    },
    SplashScreen: {
      launchShowDuration: 2000,
      backgroundColor: '#e5fae9',
      showSpinner: false
    },
    StatusBar: {
      style: 'default',
      backgroundColor: '#e5fae9'
    },
    CapacitorHttp: {
      enabled: true
    },
    CapacitorAssets: {
      iconPath: 'src/assets/icon.png',
      splashPath: 'src/assets/splash.png',
      androidIconBackgroundColor: '#e5fae9',
      androidIconForegroundColor: '#171717'
    }
  },

  android: {
    allowMixedContent: true,
    captureInput: true,
    webContentsDebuggingEnabled: true,
  },

  ios: {
    contentInset: 'automatic',
    scrollEnabled: true,
  }
};
```
<br>

## 🔐 9. Permissions Android (AndroidManifest.xml)
Voici les autorisations définies dans le fichier AndroidManifest.xml pour garantir l'accès à la caméra et à la galerie, tout en respectant les spécificités des différentes versions d'Android :

Etraits du AndroidManifest.xml :
```
<!-- Internet pour appels API -->
<uses-permission android:name="android.permission.INTERNET" />

<!-- Pour la prise de photo -->
<uses-permission android:name="android.permission.CAMERA" />

<!-- Accès à la galerie (Android ≤ 12) -->
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

<!-- Accès aux médias (Android 13+) -->
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />

<!-- Déclaration des fonctionnalités caméra -->
<uses-feature android:name="android.hardware.camera" android:required="false" />
<uses-feature android:name="android.hardware.camera.autofocus" android:required="false" />
```

Et le provider nécessaire à la gestion sécurisée des fichiers photo :
```
<provider
  android:name="androidx.core.content.FileProvider"
  android:authorities="${applicationId}.fileprovider"
  android:exported="false"
  android:grantUriPermissions="true">
  <meta-data android:name="android.support.FILE_PROVIDER_PATHS" android:resource="@xml/file_paths" />
</provider>
```
<br>

## 🔭 10. Perspectives pour l’application iOS
Le projet iOS a été amorcé avec Capacitor et la configuration de base est en place. La suite du développement et des tests sur cette plateforme fait partie des prochaines étapes.

### Prochaines actions prévues :
- Ouverture et configuration du projet dans Xcode sur un environnement macOS.
- Tests fonctionnels sur simulateur et sur un appareil iOS réel (authentification, navigation, prise de photo, etc.).
- Gestion des permissions iOS, notamment pour l’accès à la caméra et aux photos, en respectant les contraintes Apple (info.plist).
- Optimisation des performances spécifiques à iOS (animations, rendu).
- Uniformisation de l’interface pour assurer une expérience cohérente avec Android.
- Publication sur l’App Store, accompagnée d’un processus de validation Apple.

🎗️ L’objectif est de garantir une expérience fluide et native sur iOS, avec un respect strict des standards Apple tout en gardant la logique métier commune avec la version Android.
<br><br>

## 🎯 11. Conclusion

- Le développement mobile avec `Capacitor` permet une transition fluide d’un projet web vers un environnement natif. Les fonctionnalités essentielles, comme la capture de photo ou la navigation mobile, sont intégrées sans surcharge excessive.
Grâce à `Next.js` et une gestion adaptée des services API, l’expérience utilisateur est cohérente entre les plateformes. Les tests sur appareil réel et simulateur confirment la stabilité du projet.
- Cette approche garantit une solution moderne, fiable et polyvalente, parfaitement adaptée aux usages terrain tout en assurant une maintenabilité optimale du code.