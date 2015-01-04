#Pattern register

Ce chapitre à pour but de documenter un pattern (ou un motif) qui est utilisé à plusieurs reprises dans Beluga.

##Implémentation
Une implémentation simple est la suivante:

RegisterPattern.hx
```haxe
class RegisterPattern {

    var mydata : List<String>;
    
    //Cette fonction est appelé via un autobuild
    macro public static function register() : Array<Field> {
        myData.push(Context.getLocalClass().get().name);
    }

    public static function PrintAllRegisteredClasses() {
        //Afficher le liste "mydata"
    }
    
    macro public static function MaMacro() {
        //La liste de string peut même être utilisé dans une macro !
    }
}
```

TestClass.hx
```haxe
@:build(RegisterPattern.register())
class TestClass{};
```

Main.hx:
```haxe
import TestClass;

public static function main() {
    RegisterPattern.PrintAllRegisteredClasses(); //Affiche TestClass
    //Utilisation de Test Classe
}
```

##Les Avantages
Le but de ce pattern est que l'utilisateur n'ait pas besoin d'écrire du code supplémentaire. En temps normal, le `main` aurait ressemblé à ça:
```haxe
import TestClass;

public static function main() {
    RegisterPattern.register(TestClass);
    RegisterPattern.PrintAllRegisteredClasses();
    //Utilisation de Test Classe
}
```
Imaginons qu'il y ait 25 classes de test: cela ferait 25 lignes de code à placer dans le `main` alors qu'avec ce pattern pour chaque nouvelle classe, pas d'ajout de code dans le main.

##Utilisation dans Beluga

###Instance de module
Le meilleur exemple de l'application de ce pattern est la déclaration d'un Module auprès de Beluga.

Lorsqu'un utilisateur écrit pour la première fois `beluga.getModuleInstance(MonModule)`, Beluga ne créé pas de nouvelle instance du module car Beluga l'a déja créée dans sa propre instanciation. Le module s'étant précédemment enregistré auprès de lui via:
```haxe
@build(Beluga.registerModule())
class MonModule{
    //Code
}
```

De plus, le module était donc prêt à recevoir des signaux de la part d'un autre module même s'il n'est pas manipulé directement par l'utlisateur.

En réalité c'est un peu plus compliqué que ça: Beluga délègue cette tâche de gestion des modules à une classe qui s'appelle `ModuleBuilder`.

###Autres utilisations
Ce pattern est aussi utilisé dans les cas suivant:
- Déclaration des modèles de module à Beluga.
- Déclaration des classes javascript à Beluga.
- Déclaration des fichiers Css à Beluga.
