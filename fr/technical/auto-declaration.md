#Auto déclaration de module

Le système d'auto-déclaration de module a été créé afin que l'utilisateur n'ait pas à instancier à la main chacun des modules qu'il souhaite utiliser, mais aussi afin qu'aucun fichier de configuration supplémentaire ne soit nécessaire pour l'enregistrer auprès de Beluga.

Ce système est implémenté dans la classe ModuleBuilder.

##Déclaration

Chaque module héritant de la classe Module se voit donc déclaré grâce à l'autobuild ModuleBuilder.registerModule().

beluga/module/Module.hx:
```haxe
@:autoBuild(beluga.metadata.SessionFlashData.build())
@:autoBuild(beluga.module.ModuleBuilder.registerModule()) // enregistre le module auprès de Beluga
@:autoBuild(beluga.resource.CssBuilder.readCssMetadata())
class Module
{
```

Cela signifie que dès qu'un module est importé dans un fichier source haxe, celui-ci est automatiquement déclaré auprès du coeur de Beluga.

Grâce à cette déclaration, les modules sont alors automatiquement instanciés et initialisés à partir du moment où l'on écrit *ModuleBuilder.createInstances(MonModule)*.
Ainsi, imaginons qu'un Module A dépende d'un autre Module B. L'auto-déclaration aurait pour effet d'inclure automatiquement la dépendance Module B du par la ligne *ModuleBuilder.createInstances(Module1)* utilisée dans Module A.

##Récupération et initialisation des modules
Ensuite Beluga récupère un tableau d'instances des modules via *ModuleBuilder.createInstances();*.

Les modules sont alors associés à leur type pour rendre leur accès possible (sans devoir les ré-instancier) lors de l'appel à *Beluga.getModuleInstance();*. Chaque module étant maintenant instancié, la fonction "initialize" de chaque module est appelée. Cette dissociation de l'instanciation et de l'initialisation évite les risques d'appels infinis entre modules dépendants.

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

