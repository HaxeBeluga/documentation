Module - Porte-feuille
======================

Le module de __porte-feuille__ vous permet de gérer différentes devises au sein de votre site ainsi qu'un porte-feuille virtuel qui pourra être attribué à chacun de vos utilisateurs.

Afin d'utiliser le module de __porte-feuille__ vous devez inclure le module de __compte__ disponible au sein de Beluga. En effet, le porte-feuille fonctionne étroitement avec le module de compte afin de verifier l'identité de l'utilisateur courant.

Ce module offre plusieurs fonctionnalités : outils et widgets afin de facilement intégrer un porte-feuille au sein de votre site.

### Widgets


```Haxe
public function display(): Void
public function admin(): Void
```

Ces deux fonction sont géré par le diffuseur d'évènement web interne de Beluga, et son appelé lorsque l'utilisateur
requête la visualisation d'un des widgets proposé par le module de porte-feuille. Ces deux widget lancent 
respectivement les évènements:

* `display`
* `admin`

qui suggèrent au développeur d'afficher le widget de porte-feuille ou bien celui d'administration du porte-feuille.


### Fonctions

```Haxe
public function create(): Void
public function createCurrency(args: { name: String, rate: String }): Void;
public function removeCurrency(args: { id: Int }): Void;
public function setSiteCurrency(args: {id: Int }): Void;
public function addFunds(args: {funds: Float }): Void;
public function consumeFunds(args: {funds: Float }): Void;
```

Ces fonctions sont les principales fonctionnalités proposées par le module.

La premiere fonction permet la creation d'un nouveau porte-feuille pour l'utilisateur. Si le l'utilisateur est 
actuellement connecté (verification grace au module de compte), le porte-feuille est cree, sinon un évènement
d'erreur est lancé.


Les méthodes `createCurrency` et `removeCurrency`, permettent de respectivement créer ou supprimer une devise sur le site internet.

La fonction `setSiteCurrency` va permettre de choisir l'une des devises enregistrées pour le site comme la devise à utiliser pour les transactions.

Les fonctions `addFunds` et `consumeFunds` vont permettre d'ajouter ou de supprimer des fonds sur le porte-feuille de l'utilisateur. Une fois de plus, ces fonctionnalités sont étroitement liée au module de compte. En effet, il est fait automatiquement appel à celui-ci afin de vérifier l'identité de la personne actuellement connectée.

### A propos des évènements

Ces fonction lancent toutes des évènements en cas de succès ou d'échec, ces évènements son facilement reconnaissables 
et suivent un meme patron: le nom de l'action + un suffix. Par example les évènements dans le cas de la fonction 
`addFunds` seront *addFunds__Fail__* et *addFunds__Success__*

### Outils de conversions

D'autre fonctions sont disponibles sous formes d'outils afin de facilement réaliser des conversions sur les fonds réels de l'utilisateur dans différentes devises.
