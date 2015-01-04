@(Beluga)[Documentation, Technical]

## Flux d'execution de Beluga

### Accès à Beluga

Beluga ne peut être directement instancié, aussi il doit être récupéré au travers de la methode ``getInstance``. Ceci permet de n'effectuer qu'une seule fois l'initialisation du framework, lors du premier appel de la methode. Aussi, cette methode prend en paramètre une connection vers une base de données, laissant ainsi le choix au développeur de laisser, ou non, Beluga se connection à la base de donnée.

Celle-ci se compose en deux parties majeures : instanciation et initialisation.

#### Instantiation

Dans un premier temps, Beluga initialise la base de données. Si le paramètre ``Connection`` est ``null``,
Beluga ira lire dans les fichiers de configuration les données d'authentification de la base. Ceci, afin d'y rajouter les tables dont les différents modules utilisés par le développeur ont besoin.

Puis, c'est à l'API web de Beluga d'être initialisée. Celle-ci a pour objectif de redistribuer les requêtes générées par les widgets vers les modules correspondants. (cf API LINK TO PUT)

Le context du "Haxe remoting" est ensuite créé. C'est lui qui va permettre au développeur et aux modules de transmettre simplement des objets de PHP où Neko vers JavaScript.

Finallement, ce sont les ressources JavaScript et Css qui sont compilées. (cf MACRO FLUX + JavascriptBuilder and CssBuilder)

``` Beluga.hx
private function new(cnx: Connection = null)
{
    initDatabase(cnx);
    //Create beluga API
    api = new BelugaApi();
    remotingCtx = new haxe.remoting.Context();

    //Compile JS assets
    beluga.resource.JavascriptBuilder.compile();
    //Compile CSS assets
    beluga.resource.CssBuilder.compile();
}
```

#### Initialisation

La seconde phase de création de l'instance Beluga, l'initialisation, permet d'initialiser chacun des modules sans risquer les boucles infinies de dépences (que ce soit des dépendences beluga-module où module-module).
Elle permet aussi d'associer chaque instance de module à leur type, de sorte que tout comme Beluga, chacune d'elles soient accessible sans avoir à réinstancier le module (au travers de la méthode ``Beluga.getModuleInstance()``, cf AUTO DECLARATION MODULES).

``` Beluga.hx
private function initialize() {
    var modules = ModuleBuilder.createInstances();
    for (module in modules) {
        this.modules.set(Type.getClass(module), module);
    }
    for (module in modules) {
        module.initialize(this);
    }
}
```

### Methodes exposées au développeur

Le framework Beluga se veut aussi peut invasif et restrictif que possible pour le développeur. Aussi, le nombre d'appels nécessaire au bon fonctionnement de Beluga est au nombre de deux :
- Beluga.handleRequest()
- Beluga.cleanUP()

#### Gestion de requête

La methode ``handleRequest`` doit être appelée en début d'exécution du serveur et laisse la main à Beluga pour lire la dernière requête reçu (URL + paramètres + headers). Si cette URL commence par ``http://nom.du.site/beluga``, Beluga garde la main et traite la requête comme lui appartenant.

Ensuite, avant de traiter la requête, Beluga vérifie que celle-ci n'a pas été lancée par un système interne à Haxe permettant le transfert d'instances de PHP vers JavaScript ("Haxe remoting"); auquel cas il laisse à Haxe le soin de gérer la requête.
Le cas échéant, le framework fait appel au dispatcher pour rediriger les paramètres de la requête vers la bonne méthode du bon module selon la convention ``URL/nom-du-module/nom-de-la-methode#parametres``. (cf Module Api TOBEFILED WITH HYPERLINK)

Beluga laisse alors de nouveau la main au contexte développeur. Ce dernier peut alors savoir si la requête reçue lui appartenait grâce à la valeur de retour de la methode ``handleRequest``.

#### Quitter Beluga

La methode ``cleanUp`` permet à Beluga de reprendre une dernière fois la main avant la fin de l'execution du serveur. Celle-ci appelle trois methode :
- FlashData.updateTtl()
    - Cette methode met à jour les données de session dites "flash" (disponibles le temps d'une seule requête par défaut) (cf FlashData TOBEFILED WITH HYPERLINK)
- DataBase.close()
    - Cette methode ferme correctement le driver vers la base de donnée. (cd DataBase TOBEFILED WITH HYPERLINK)
- Session.close()
    - Essentielle sous ``Neko``, automatique sous ``Php``, cette methode permet la validation de la mise à jour des données de session. 
    
### Schema de flux d'exécution

![Alt text](./Execution and request handling flow in Beluga.jpg)

