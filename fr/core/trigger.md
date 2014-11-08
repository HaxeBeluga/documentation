# Trigger

Les triggers se mettent en place en trois phases :

```haxe
import beluga.core.trigger.Trigger;

//1-Declaration
var t = new Trigger<String>();

//2-Enregistrement
t.add(function (str : String) {
	trace("Test1" + str);
});
t.add(function (str : String) {
	trace("Test2" + str);
});

//3-Dispatch
t.dispatch("motdetest");
```

```
Output:
Main.hx:46: Test1motdetest
Main.hx:49: Test2motdetest
```

Ils fonctionnent aussi avec des méthodes statiques :

```haxe
t.add(Sys.print);
```

Ou avec des méthodes d’instance :

```haxe
var moninstance = new MaClass();
t.add(moninstance.mafonction);
```

Le trigger prend en paramètre template le type de données qu’il dispatch. Dans le cas où il dispatch plusieurs arguments, il suffit de faire un objet anonyme :

```haxe
typedef MonTypeTrigger {arg1:String, arg2 : Int};
var trigger = new Trigger<MonTypeTrigger>();
t.add(function (args : MonTypeTrigger) {
     //process data
});
t.dispatch({arg1: “Test”, arg2:42});
```

Dans le cas où il ne dispatch aucun argument, un type de trigger spécial existe (“beluga.core.trigger.TriggerVoid”) car Haxe ne supporte pas le type "Void" comme type de paramètre.

## Implémentation

### Déclaration

Chaque module dans Beluga doit donc déclarer ses triggers :

```haxe
class MonModuleImpl {
     var trigger1 = new Trigger<String>();
     var trigger2 = new TriggerVoid();
}
```

Mais pour une question de clarté et de namespace, nous préférerons les mettre dans une classe a part.

```haxe
class MonModuleTrigger {
     var trigger1 = new Trigger<String>();
     var trigger2 = new TriggerVoid();
}
class MonModuleImpl {
     var triggers = new MonModuleTrigger();
}
```

### Enregistrement

*La phase d’enregistrement auprès des autres modules ne doit surtout pas se faire dans le constructeur de module car les autres instances de module ne sont peut-être pas encore prêtes.*

Une méthode suchargeable “initialize” est prévu a cet effet. Elle est appelée après que tous les autres modules aient été instanciés.

```haxe
class MonModuleImpl extends ModuleImpl {

public function initialize(beluga : Beluga) : Void {
    var autreModule = Beluga.getModuleInstance(MonAutreModule);
    autreModule.trigger.trigger42.add(this.mafonction);
}

}
```
### Diffusion

Voilà ! Il vous est maintenant possible de dispatch un trigger n’importe oú.
