# SushiFast-v2

## Installation

- Créer un projet Angular à l’aide de la commande ```ng new nomduprojet``` avec « yes » pour le rooting et « css » comme format de stylesheet
- Installer Bulma à l’aide de la commande ```npm install bulma```
- Télécharger les fichiers du dépôt et les copier dans la racine
- A la racine du projet, exécuter la commande ```ng serve``` pour lancer le serveur
- Exécuter ensuite, toujours à la racine, la commande ```json-server --watch backend/database.json``` pour lancer l’API

## Header

Le composant header est une barre de navigation. Il apparaît en haut de n'importe quelle page de l'application. Cette barre de navigation contient :
- le titre de l'application
- le lien vers l'accueil de l'application
- le lien vers le panier de l'application

Header sur l'application

![screenshot](https://user-images.githubusercontent.com/78152375/161386049-ebd55934-204e-4901-8836-11aab82757a1.PNG)

Code de header.component.html (vue)

![screenshot](https://user-images.githubusercontent.com/78152375/161381844-a94f0b23-6c2d-41ab-a645-c91a69bd7953.PNG)

## Home

Le composant home contient :
- les menus
- la commande, listant les menus ajoutés grâce au bouton +
- les détails des menus, affichés grâce au bouton Détails (affModal)
- le bouton +, pour ajouter un menu à la commande

Image des menus sur la page

![screenshot](https://user-images.githubusercontent.com/78152375/161388084-81c9aedc-b1a2-4829-a6f2-2149b0f0ffbd.PNG)

Image du tableau de la commande

![screenshot](https://user-images.githubusercontent.com/78152375/161388091-3cddc109-1398-40cf-bc33-0f348eccb707.PNG)

Image des détails lorsque l'on appuie sur le bouton "Détails"

![screenshot](https://user-images.githubusercontent.com/78152375/161388097-f55566db-6982-436a-8194-3ece9ee790a5.PNG)

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

## Affichage des menus

Les menus sont affichables grâce à une interface exportée.

```typescript
//Extrait de boxes.service.ts

export interface Boxes {
  id: number;
  name: string;
  piece: number;
  prix: number;
  saveur: string;
  }
  ```

Et grâce à l'utilisation de l'API.

```typescript
//Extrait de boxes.service.ts

// Interrogation de l'API pour afficher les menus
  getBoxes(): Observable<any> {
    return this.http.get<any>(urlrest + '/boxes').pipe(
    catchError(this.handleError)
    );
  }
  ```
  
  Ils sont ensuite affichés dans la vue.
  
  ```html
<!--Extrait de home.component.html-->

 <!--  Affichage des menus -->
        <div class="Box">
            <div class="p-5 " *ngFor="let boxe of Boxes ; let index = index"  >
                <div class="p-3" class="bg-light border border-primary">
                    <a ><img class="Menu" src="assets/images_boxes/{{boxe.image}}.webp"/></a>
                </div>
              <!-- Nom du menu -->
                <div class="p-3" > 
                    <span class=Itemitle> {{boxe.nom}}</span>
                </div>
              <!-- Prix du menu -->
                <div class="p-3" > 
                    <span class=Itemitle> {{boxe.prix}}€ | {{boxe.pieces}} pièces</span>
                </div>
```
  
  ## Affichage de la commande
  
  Ici aussi, une interface est exportée.
  
  ```typescript
  //Extrait de ligne-commande.service.ts
  
  //La classe contient les informations retournées par une requête.

export class LigneCommande {
    constructor(
        public id: number,
        public nomPlateau: String,
        public quantite: number,
        public prix: number
        
    )
    {}
   
}
```

Elle est ensuite utilisée pour la vue du composant Home.
```html
<section class="section">
    <div class="container">
        <div fxFlex.gt-xs="30%">
            <h1 class="title is-3">Commande</h1>
            <table class="table is-striped center">
                <thead>
                    <tr>
                        <th>Plateau</th>
                        <th>Prix</th>
                        <th>Quantité</th>
                    </tr>
                </thead>
                <tbody>
                    <tr *ngFor="let elem of commande; let index = index">
                        <td>{{elem.nomPlateau}}</td>
                        <td>{{elem.prix}}€</td>
                        <td>{{elem.quantite}}</td>
                    </tr>
                </tbody>
            </table>
            <div style="font-weight:bold;">Total commande : {{ totalCommande() }}€</div>
        </div>
```

## Bouton +

Le bouton + permet de rajouter un menu à la commande. On utilise alors la fonction plus.

```typescript
plus(index: number) {
    
    this.commande = JSON.parse(localStorage.getItem('SushiCommande') || '[]');
    let ajout = false;
    this.commande.forEach(elem=> {
      if (elem.id ==  this.Boxes[index].id) {
        elem.quantite++;
        ajout = true;
      }
    });

    if (!ajout) {
      let uneLigne = new LigneCommande(this.Boxes[index].id, this.Boxes[index].nom,1, this.Boxes[index].prix);
      this.commande.push(uneLigne);
      console.log("Plus :" + index + this.Boxes[index].nom);
    }

    let tabItems = JSON.stringify(this.commande);
    localStorage.setItem('SushiCommande', tabItems);
    
  }
```


## Affichage des détails

L'affichage des détails sur les menus se fait grâce à la fonction affModal.

```typescript
//Extrait de home.component.ts

 //Fonction pour afficher les détails de chaque menu
  affModal(i: number) {
    if (this.showModal) {
      this.showModal = false;
    } else {
      console.log("Modal indice :" + i);    
      console.log("Modal nom plateau :" + this.Boxes[i].nom);
      this.boxe = this.Boxes[i];
      this.showModal = true;
    }
  }
  ```
  La fonction affModal est ensuite utilisée dans la vue, en appuyant sur le bouton Détails.
  
  ```html
 <!-- Détails du plateau quand affModal est activé -->
  <div class="modal is-active" *ngIf="showModal">
        <div class="modal-background"></div>
            <div class="modal-content">
                <h1 class="title is-3" style="color:azure;">{{boxe.nom}}</h1>
                <img src="assets/images_boxes/{{boxe.image}}.webp" /><br />
                <h3 style="color:yellow;">Nombre de pièces :</h3> <p style="color: white ;">{{boxe.pieces}}</p>
                <h3 style="color:yellow;">Saveurs :</h3> <p style="color: white ;">{{boxe.saveurs}} </p>
                <h3 style="color:yellow;">Compositions :</h3>
                <p style="color: white ;" *ngFor="let boxe of boxe.composition " >{{boxe.nom}}, {{boxe.quantite}}</p>
                <br />
              <!-- Bouton pour fermer les détails -->
                <button class="button is-primary" (click)="affModal(0)">Fermer</button>
            </div>
        </div>
   </div> 
```

