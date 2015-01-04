Module - Marché
===============

Le module de __marché__ vous permet de facilement vendre des articles sur votre site internet.

Afin d'utiliser le module de __marché__, vous devez inclure le module de __compte__ disponible au sein de beluga. En effet, le __marché__ fonctionne étroitement avec le module de compte afin de vérifier l'identité de l'utilisateur courant, ainsi qu'avec le module de __porte-feuille__ qui vous permet de profiter de sa notion de monnaie réelle ou fictive ainsi que des différentes devises au sein de votre marché.

Ce module offre plusieurs fonctionnalités, outils et widgets, afin de facilement intégrer un __marché__ au sein de votre site.

### Widgets

```Haxe
public function display(): Void;
public function admin(): Void;
public function cart(): Void;
```

C'est trois fonctions sont gérées par le diffuseur d'évènement web de beluga. Elles lancent respectivement les évènements:

* `display`
* `admin`
* `cart`

qui permettent d'informer le développeur qu'un utilisateur du site internet souhaite accéder à l'un des différents widgets précedents.

Le widget `display` va permettre d'afficher les différents articles disponibles au sein du marché.
Le widget `cart` quant à lui, permet l'affichage du panier de l'utilisateur courant.
Enfin, le widget `admin` va permettre d'afficher la partie `back-office` du marché et ainsi gérer le prix et l'ajout de produits.
Ces widgets font appel en interne au module de compte afin de s'assurer que l'utilisateur courant est bien authentifié sur le site.

### Fonctions

```Haxe
public function addProductToCart(args: { id: Int }): Void;
public function removeProductInCart(args: { id: Int }): Void;
public function checkoutCart(): Void;
```

Ces trois fonctions peuvent être aussi bien utilisées par l'utilisateur que par le web dispatcher interne à Beluga.

*public function addProductToCart(args: { id: Int }): Void* :

Cette fonction permet d'ajouter un produit au panier de l'utilisateur, a l'aide de l'identifiant en base de donnée du produit. Si le produit existe, alors le produit est ajouté, néanmoins si l'utilisateur n'est pas identifié ou si le produit n'existe pas, un évènement d'erreur et lancé.

*public function removeProductInCart(args: { id: Int }): Void* :

Cette fonction permet de supprimer un produit au panier de l'utilisateur, a l'aide de l'identifiant en base de donnée du produit. Si le produit existe est present dans le panier alors celui ci est supprimé, néanmoins si l'utilisateur n'est pas identifié ou si le produit n'existe pas, un évènement d'erreur et lancé.

*public function checkoutCart(): Void* :

Cette fonction permet de valider l'achat des produits contenus dans le panier de l'utilisateur. Lors de l'appel, il est vérifié si l'utilisateur est bien identifié, puis si les fond disponibles dans le porte-feuille de l'utilisateur sont suffisant. Dans ce cas le panier est acheté et un évènement de succès et lancé contenant la liste des produits achetés par l'utilisateur, et la somme totale du panier. Dans le cas contraire un évènement d'erreur est lancé.

### A propos des évènements

Ces fonction lancent toutes des évènements en cas de succès ou d'échec, ces évènements son facilement reconnaissables 
et suivent un meme patron: le nom de l'action + un suffix. Par example les évènements dans le cas de la fonction 
`addFunds` seront *checkoutCart__Fail__* et *checkoutCart__Success__*

### Fonctions utilitaires

```Haxe
public function getProductList(): List<Product>;
public function getProductFromId(id: Int): Option<Product>;
``

Ces fonctions permettent d'obtenir des informations a propos du panier courant d'un utilisateur, ou encore a propos d'un produit.
Dans le cas de `getProductList`, il est vérifié tout d'abord qu'un utilisateur est bien connecté sur le site, puis que celui ci posséde bien un panier. Dans ce cas la liste des produits au sein du panier est retournée. Dans le cas contraire un évènement d'erreur est lancé.

En ce qui concerne `getProductFromId`, cette fonction permet d'obtenir un produit par son identifiant.
