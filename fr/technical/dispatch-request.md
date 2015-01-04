#Dispatche d'une requête

Pour faciliter la tâche a l'utilisateur et lui éviter de recréer un controlleur qui map une url pour chaque service, Beluga fouri un controlleur par défaut. Toutes les urls a destination de beluga commence par /beluga c'est comme ca que la fonction "Beluga.handleRequest()" vérifie si la requète est destinée a Beluga ou non.

Le controlleur est créé grace au [WebDispatcher](http://old.haxe.org/manual/dispatch) de la bibliothèque standard Haxe.

Comme chaque module doit fournir sont propre contoleur, aussi appelé api dans le cadre du WebDispatcher, Beluga a une api générale qui redispatch la requete vers le module concerné, cette classe est *BelugaApi*.

##Enregistrer une api module

Il faut concidérer BelugaApi comme une map entre une string et une API web dispatcher. *BelugaApi.register("moduleApi", monApi)* permet d'accocier une chaine de charactere a une API. L'api devient accésible par l'URL "http://localhost/beluga/monApi/...". Cette étape d'association est normalement éffectué lors de l'initialisation d'un module.

##Diriger la requête vers un module
Dans le Beluga.handleRequest() si l'url commence par /beluga la requete est ensuite transmise a BelugaApi.doDefault() qui va aller chercher dans la map l'api correspondante. Bien sur l'api n'est pas trouvé une exception est levée.

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

Le module ensuite a la liberté de s'organiser comme il le souhaite. Et même si se n'est pas conseillé de pouvoir enregistrer plusieurs api.
