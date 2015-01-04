#Redirection d'une requête

Pour faciliter la tâche à l'utilisateur et lui éviter de recréer un controleur qui fait correspondre une url pour chaque service, Beluga fournit un controlleur par défaut. Toutes les urls à destination de beluga commencent par "/beluga". C'est ainsi que que la fonction "Beluga.handleRequest()" vérifie si la requête est destinée à Beluga ou non.

Le controleur est créé grâce au [WebDispatcher](http://old.haxe.org/manual/dispatch) de la bibliothèque standard Haxe.

Comme chaque module doit fournir son propre controleur, aussi appelé __api__ dans le cadre du WebDispatcher. Beluga a une api générale qui redirige la requête vers le module concerné: la classe *BelugaApi*.

##Enregistrer une api module

Il faut considérer BelugaApi comme le lien entre une string et une API web dispatcher (on appelle ça une map). *BelugaApi.register("moduleApi", monApi)* permet d'associer une chaine de charactere à une API. L'api devient alors accessible par l'URL "http://localhost/beluga/monApi/...". Cette étape d'association est normalement effectué lors de l'initialisation d'un module.

##Diriger la requête vers un module
Dans le Beluga.handleRequest() si l'url commence par "/beluga", la requête est ensuite transmise à BelugaApi.doDefault() qui va aller chercher dans la map l'api correspondante. Bien sûr, une exception est levée si l'api n'est pas trouvée.

BelugaApi.hx:
```haxe
public function doDefault(apiName : String, d : Dispatch) {
    if (config.exists(apiName)) {
        var cfg = config.get(apiName);
        d.runtimeDispatch(cfg);
    }
    else
        throw new BelugaException("Can't find " + apiName + " api.");
}
```

Le module a ensuite la liberté de s'organiser comme il le souhaite, même s'il n'est pas conseillé de pouvoir enregistrer plusieurs api.
