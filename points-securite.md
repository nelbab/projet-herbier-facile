# 🔒 Points sur la sécurité de l'application 🌷

## 📑 1. Sécurisation des données

### a. Utilisation de l'ORM Prisma

L'utilisation des <b>ORM (Object-Relational Mapping) comme Prisma ORM</b> est un excellent choix pour éviter les injections SQL car il génère des requêtes SQL préparées (ou paramétrées) automatiquement.

- ORM est un programme informatique qui se place entre un back-end et une base de données relationnelle.
- Celui-ci sécurise les échanges entre le back-end et la base de données en n'exposant pas les requêtes SQL.
- Prisma ORM permet de créer la base de données et les tables du projet avec le schema prisma.

### b. Yup et formik

<b>Yup</b> est un constructeur de schéma pour l'analyse et la validation des valeurs pendant l'exécution. <br />
- Définissez un schéma, transformez une valeur pour qu'elle corresponde, affirmez la structure d'une valeur existante, ou les deux.<br /> 
- Les schémas Yup sont extrêmement expressifs et permettent de modéliser des validations complexes et interdépendantes, ainsi que des transformations de valeurs.
- Schéma pour exclure les caratères < et > :<br />
``` 
text: Yup.string()
    .matches(/^[^<>]*$/, "Les caractères '<' et '>' sont interdits")
    .required("Ce champ est requis"),
``` 

- exemple de schéma pour contrôler un numéro de téléphone français sans espace en version national ou internationnal :<br />
``` 
phone: Yup.string()
    .matches(^\+33[1-9]\d{8}$|^0[1-9]\d{8}$, "Le numéro de téléphone n'est pas valide")
    .required("Le numéro de téléphone est requis"),
``` 

La bibliothèque <b>Formik</b> est une bibliothèque populaire de gestion de formulaires pour React.<br />
- Formik est conçu pour gérer des formulaires avec une validation complexe ou simple.<br />
- Formik supporte la validation synchrone et asynchrone au niveau du formulaire et du champ.<br /> 
- Le hook personnalisé useFormik aide à simplifier le processus de création et de gestion de formulaires dans les applications React en gérant l'état du formulaire, la validation et la soumission du formulaire.<br />

### c. Hachage Bcrypt

<b>Bcrypt</b> est une technique de hachage utilisée pour protéger les mots de passe contre les attaques des hackers en stockant les mots de passe sous un format haché.<br />
- Il transforme le mot de passe d'un utilisateur en une chaîne de caractères de longueur fixe au sein d'une fonction de <b>hachage unidirectionnelle</b>, ce qui garantit qu'il ne peut pas être inversé pour retrouver le mot de passe d'origine.
- Lorsque l'utilisateur se connecte, bcrypt ré-hache le mot de passe et compare cette nouvelle valeur à celle stockée dans la base de données pour vérifier leur correspondance.<br />

### d. Cryptage des données sensibles

- utilisation de la librairie <b>crypto-js</b>.
- J'ai crypté le access_token avant de l'enregistrer dans le cookie et le refresh_token avant de l'enregistrer dans la base de données.

### c. Dto

Création de <b>DTos</b> pour valider les données passées dans <b>Prisma</b>.
<br><br>

## 👥 2. Sécurisation des sessions

### a. JWS token 

Les <b>JWS token</b> permettent une protection des connexions. <br />
- Ils sont constitués de 3 parties : l'entête, le payload et la signature. <br />
- Le payload contient les informations à transmettre comme l'id du user ou la date d'expiration.
- Le refresh_token, stocké dans la table user, permet aux utilisateurs de générer un nouvel access_token sans devoir se reconnecter à chaque expiration de l'access_token tant que le refresh_token est valide.
- Utilisation de la librairie <b>jsonwebtoken</b>.

### b. Cookie

- L'utilisation des cookies permettera le bon fonctionnement de l'application.
- Les données du cookie sont supprimées à la déconnexion ou à la fermeture du navigateur, ce qui assure une meilleure sécurité.
- Les cookies sont protégés avec les paramètres "httpOnly: true" et "secure: true".
- Utilisation des cookies de <b>next/headers</b>.

### c. Middleware

- J'ai créé un <b>middleware de limitation de débit d'API</b> en limitant le nombre de requêtes par fenêtre de temps.
- J'ai aussi créé un <b>middleware pour contrôler les routes</b> de mon application. Il y a trois catégories de routes :
  - Publique
  - User et Admin
  - Admin
- Le <b>middleware</b> me permet de gérer les <b>tokens</b>. Contrôle de l'existance et de la validité du token access.
<br><br>

## 🌍 3. Sécurisation de l'application avec le https

Une fois que l'application sera finie et opérationnelle, le déploiement se fera sur un serveur debian avec l'utilisation d'un <b>certificat de sécurité TLS</b> pour avoir un accès de l'application en https.<br>
J'ai activé <b>HTTPS</b> sur mon hébergeur AWS, mon application web est bien configuré pour utiliser HTTPS de manière optimale. AWS fournit une interface simple pour activer un <b>certificat SSL/TLS</b>. <br>
J'ai activé la redirection de tout le trafic HTTP vers HTTPS.
- Cela garanti que les données échangées seront chiffrées, ce qui protège contre les interceptions ou attaques potentielles.<br>
- Ce qui permet de chiffrer les requêtes http `POST` notamment.
<br><br>

## 🎯 4. Conclusion

Article très intéréssant sur ce sujet :

https://curity.medium.com/best-practices-for-storing-access-tokens-in-the-browser-6b3d515d9814

Au vu de cet article sur la sécurité de navigation sur un site ou une application, je vais utilisé les cookies en association avec les tokens JWT, le hachage du mot de passe et du refresh_token et le cyptage des données sensibles.
