# Javascript #

## A quoi ça sert ? ##

Le **Javascript** permet d'éxécuter du code sur le client. C'est à dire rendre dynamique les pages web. Dans les modules de Beluga, le Javascript est utilisé afin de pouvoir mettre à jour l'état des *widgets* (Fragments de page web) sans avoir à rafraîchir la page web.

## Comment s'en servir ? ##

Tout d'abord, il faut prendre en considération le fait que le code Javascript est développé en Haxe et non pas en Javascript, Haxe se chargeant de la traduction du code. Ceci nous permet de faire communiquer directement le code serveur et le code client puisqu'ils parlent la même langue.

Le code Haxe devant être compilé en Javascript doit ensuite être placé dans un dossier `"js/"` à la racine du module. Lorsque le module sera compilé, le compilateur parcourira le dossier contenant le Javascript à la recherche de toutes les classes contenant une méthode prototypée telle que `public static function init()`. Cette méthode constituera un des points d'entrée du programme Javascript final.

Une fois tous les modules compilés et tous les points d'entrées réunis. Une compilation Haxe est lancée vers Javascript. Le programme Javascript ainsi créé sera nommé `beluga.js` et se contentera d'appeler à tour de rôle toutes les fonctions `init` ainsi trouvées.

De cette manière, chaque fichier Javascript sera executé au chargement d'une page. Ils pourront indépendamment décider de s'endormir si leur *widget* n'est pas présent sur la page ou au contraire lancer leur routine de traitement et communication.


### Exemple de déclaration de classe Javascript ###

    package beluga.module.account.js;

	class Javascript {
	
	    // Every files containing this method inside a js folder will be compiled to beluga javascript
	    public static function init()
	    {
	        //Insert your js here
	    }
	
	}

## Limitations ##

Le code étant développé en Haxe, les dernières technologies Javascript ne sont pas disponibles à l'utilisation.
