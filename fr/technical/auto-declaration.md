#Auto déclaration de module

Le système d'auto déclaration de module a été créé afin que, l'utilisateur n'ai pas a instancier chacun des modules qu'il souhaite utiliser a la main, et qu'aucun fichier de config ne soit néscessaire pour tous les déclarer.

Ce systeme a été implémenté dans la classe ModuleBuilder

##Déclaration

Chaque module héritant de la classe Module se voit donc déclaré grace a l'autobuild ModuleBuilder.registerModule().

beluga/module/Module.hx:
```haxe
@:autoBuild(beluga.metadata.SessionFlashData.build())
@:autoBuild(beluga.module.ModuleBuilder.registerModule())
@:autoBuild(beluga.resource.CssBuilder.readCssMetadata())
class Module
{
```

Cela signifie qu'aprés qu'un module ai été importé dans un fichier haxe il est automatiquement déclaré au prés du coeur de Beluga.

Les Modules sont donc automatiquement instanciés et initialisés a partir du moment ou on écrit *ModuleBuilder.createInstances(MonModule)*
Imaginons que Module1 dépend de Module2, l'autodéclaration a pour éffet d'inclure automatiquement la dépendance Module2 si on écrit *ModuleBuilder.createInstances(Module1)*

##Récupération et initialisation des modules
Ensuite Beluga récupere un tableau d'instance de modules via *ModuleBuilder.createInstances();*

Ensuite les modules sont associés a leur type pour pouvoir être retrouvé lors de l'appel a *Beluga.getModuleInstance();* et chaque module étant maintenant instancié on appel la fonction "initialize" de chaque module.

beluga/Beluga.hx:89
```haxe
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

