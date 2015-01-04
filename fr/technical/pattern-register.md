#Pattern register

Ce chapitre a pour but de documenter un pattern qui est a plusieurs reprise utilisé dans Beluga.

##Implémentation
 Une implémentation simple est la suivante:

RegsterPattern.hx
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
        //La liste de string peut meme être utilisé dans une macro !
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
Le but de ce pattern est que l'utilisateur ait a éviter d'écrire du code supplémentaire. En temps normal le *main* aurait ressemblé a ca:
```haxe
import TestClass;

public static function main() {
    RegisterPattern.register(TestClass);
    RegisterPattern.PrintAllRegisteredClasses();
    //Utilisation de Test Classe
}
```
Imaginons qu'il y ait 25 classes de test cela ferait 25lignes de code a placer dans le main. Alors qu'avec ce pattern pour chaque nouvelle classe pas d'ajout de code dans le Main.

##Utilisation dans Beluga

###Instance de module
Le meilleurs éxemple de l'application de ce pattern est la déclaration d'un Module au prés de Beluga.

Lorsqu'un utilisateur écrit pour la première fois "beluga.getModuleInstance(MonModule)", Beluga ne créé pas une nouvelle instance de module! Beluga l'a déja créé a son instanciation car le module s'est enregistré au prés de lui via:
```haxe
@build(Beluga.registerModule())
class MonModule{
    //Code
}
```

Le module était aussi donc prêt a resevoir des triggers de la part de d'un autre module même si il n'est pas manipulé directement par l'utlisateur.

En réalité c'est un peu plus compliqué que ca, Beluga délegue cette tache de gestion des modules a une classe qui s'appelle "ModuleBuilder".

###Autres utilisations
Ce pattern est aussi utilisé dans les cas suivant:
- Déclaration des models de module a Beluga
- Déclaration des classes javascript a Beluga
- Déclaration des fichiers Css a Beluga