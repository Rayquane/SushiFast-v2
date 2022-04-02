# SushiFast-v2

## Installation

- Créer un projet Angular à l’aide de la commande ```ng new nomduprojet``` avec « yes » pour le rooting et « css » comme format de stylesheet
- Installer Bulma à l’aide de la commande ```npm install bulma```
- Télécharger les fichiers du dépôt et les copier dans la racine
- A la racine du projet, exécuter la commande ```ng serve``` pour lancer le serveur
- Exécuter ensuite, toujours à la racine, la commande ```json-server --watch backend/database.json``` pour lancer l’API

## Header

Le composant header est une barre de navigation. Il apparaît en haut de n'importe quelle page de l'application. Cette barre de navigation contient :
- le lien vers l'accueil de l'application
- le lien vers le panier de l'application

Code de header.component.html (vue)

![screenshot](https://user-images.githubusercontent.com/78152375/161381844-a94f0b23-6c2d-41ab-a645-c91a69bd7953.PNG)

## Home

Le composant home contient :
- les menus
- la commande, listant les menus ajoutés grâce au bouton +
- les détails des menus, affichés grâce au bouton Détails (affModal)
- le bouton +, pour ajouter un menu à la commande

## Footer

Le composant footer contient seulement un lien vers les mentions légales. Il apparaît en bas de n'importe quelle page de l'application.

Mentions légales sur la page

![screenshot](https://user-images.githubusercontent.com/78152375/161381838-c4209c3a-f6b8-489f-a918-599a3fdfbedb.PNG)

Code du footer.component.html (vue)

![screenshot](https://user-images.githubusercontent.com/78152375/161381843-f0f88ab4-0400-4a54-a787-82aadee9a35d.PNG)

## RGPD

Le composant rgpd contient la page où sont écrites les mentions légales.

Extrait de la page

![screenshot](https://user-images.githubusercontent.com/78152375/161385663-6bf58df6-7424-4425-90d3-16c8e66f352e.PNG)
