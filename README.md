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

## Home

Le composant home contient :
- les menus
- la commande, listant les menus ajoutés grâce au bouton +
- les détails des menus, affichés grâce au bouton Détails (affModal)
- le bouton +, pour ajouter un menu à la commande

## Footer

Le composant footer contient seulement un lien vers les mentions légales. Il apparaît en bas de n'importe quelle page de l'application.

## RGPD

Le composant rgpd contient la page où sont écrites les mentions légales.
