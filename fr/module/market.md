Module - Market
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

Ces trois fonctions sont gérées par le web dispatcher de Beluga. Elles lancent respectivement les triggers :

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

Cette fonction permet d'ajouter un produit au panier de l'utilisateur à l'aide de l'identifiant en base de données du produit. Si le produit existe, alors le produit est ajouté, néanmoins si l'utilisateur n'est pas identifié ou si le produit n'existe pas, un trigger d'erreur est lancé.

*public function removeProductInCart(args: { id: Int }): Void* :

Cette fonction permet de supprimer un produit au panier de l'utilisateur à l'aide de l'identifiant en base de donnée du produit. Si le produit existe et est present dans le panier, alors celui-ci est supprimé, néanmoins si l'utilisateur n'est pas identifié ou si le produit n'existe pas, un trigger d'erreur est lancé.

*public function checkoutCart(): Void* :

Cette fonction permet de valider l'achat des produits contenus dans le panier de l'utilisateur. Lors de l'appel, il est vérifié si l'utilisateur est bien identifié, puis si les fonds disponibles dans le porte-feuille de l'utilisateur sont suffisants. Dans ce cas, le panier est acheté et un trigger de succès est lancé, contenant la liste des produits achetés par l'utilisateur et la somme totale du panier. Dans le cas contraire, un trigger d'erreur est lancé.

### A propos des triggers

Ces fonctions lancent toutes des triggers en cas de succès ou d'échec. Ces triggers sont facilement reconnaissables et suivent un même patron : le nom de l'action + un suffixe. Par exemple, les triggers dans le cas de la fonction `addFunds` seront *checkoutCart__Fail__* et *checkoutCart__Success__*.

### Fonctions utilitaires

```Haxe
public function getProductList(): List<Product>;
public function getProductFromId(id: Int): Option<Product>;
``

Ces fonctions permettent d'obtenir des informations à propos du panier courant d'un utilisateur ou encore d'un produit.
Dans le cas de `getProductList`, il est vérifié tout d'abord qu'un utilisateur est bien connecté sur le site, puis que celui-ci possède bien un panier. Dans ce cas, la liste des produits au sein du panier est retournée. Dans le cas contraire, un trigger d'erreur est lancé.
En ce qui concerne `getProductFromId`, cette fonction permet d'obtenir un produit par son identifiant.
