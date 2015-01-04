# Module

Ici, nous allons voir en détails tout ce qui couvre les modules de Beluga de façon générale. En premier, nous verrons ce qu'ils _sont_ et _comment_ ils sont organisés. Ensuite, nous nous pencherons sur la façon dont ils s'intègrent à Beluga. Une fois ceci en main, nous apprendrons comment rajouter vos propres modules.

## Concept

Les modules de beluga sont la partie contenant les fonctionnalités proposées à l'utilisateur. Celles-ci étant regroupées en modules de par leurs dépendances (exemple : les fonctionnalités `enregistrer utilisateur` et `connecter utilisateur` sont réunies au sein du module `account`).
Ce découpage en modules permet aux développeurs de n'embarquer que le code contenant les fonctionnalités qu'il désire utiliser, et donc ajuster le poids de Beluga par rapport à l'utilisation qui en est faite.

## Structure

Dans Beluga, nous avons choisi de rendre le plus facile possible l'ajout de nouveaux modules aux collaborateurs. Pour cette raison, nous suivons le paradigme de _convention over configuration_. Concrètement, cela signifie que certains dossiers, fichiers et fonctions sont nécessaires pour que Beluga soit en mesure de détecter et d'utiliser automatiquement les différentes fonctionalités des modules.
De plus, nous suivons une convention de nommage très stricte permettant de facilement pouvoir naviguer d'un module à l'autre. Afin de mieux illustrer la différence entre les conventions _simples_ et celles _nécessaires_, ces dernières seront précédées d'un mot en __gras__. 

Le seul défaut de cette approche est qu'elle rend plus dure, au premier abord, de trouver pourquoi un module n'est pas entièrement reconnu par Beluga. Pour cette raison, nous avons créé un script d'auto-génération d'un module (cf: Ajouter votre propre module).

### Filesystem

Les modules se trouvent sous le dossier `beluga/module`. Ils __doivent__ respecter l'architecture dossier minimale suivante afin d'être correctement reconnus et chargés par Beluga :

``` 
module_root/
│
│─── api/          : interface de programmation utilisé par le diffuseur d'évènement de Beluga
│─── js/           : fichiers Javascript
│─── locale/       : fichiers JSON contenant les traductions
│─── view/         : fichiers HTML relatifs à la vue
     │─── css/
     │─── locale/
     └─── tpl/
└─── widget/       : Widgets class files
```
Les autres dossiers couramment utilisés, tels que `exception` et `model`, sont purement présents dans un soucis d'organisation et d'esthétique.

### Détails du contenu des dossiers

#### Racine du module

À la racine du module, les fichiers __devant__ être exposés sont *l'interface* (simplement nommée avec le nom du module) et *l'implémentation* (nom du module + "Impl"). Ces deux fichiers **doivent** respectivement étendre `Module` et `ModuleImpl`.
Exemple :

```
    interface Account extends Module {}
    [...]
    class AccountImpl extends ModuleImpl {}
```
Un module *devrait* aussi fournir deux classes contenantes:
- nom du module + "Triggers": contient tous les évènements succeptible d'être soulevés.
- nom du module + "Widgets": contient tous les widgets.

Ces deux classes sont ensuite exposées au développeur depuis l'interface du module. Exemple :
```haxe
interface Account extends Module {
    public var triggers : AccountTrigger;
    public var widgets : AccountWidget;
}
[...]
```

Ensuite, les évènements et widgets peuvent être facilement, et logiquement, accédés par la ligne suivante:

```haxe
beluga.getModuleInstance(Account).widgets.loginForm
```

#### interface de programmation

Dans le dossier `api`, il **doit** se trouver un fichier de classe contenant une interface de programmation pour le diffuseur d'évènement web de Beluga (nommé nom du module + "Api"). Puisque *c'est* un fichier d'interface de programmation web, les fonctions de routages __doivent__ commencer par "do" (voir la docummentation officielle [Haxe Web Disptacher](http://old.haxe.org/manual/dispatch#why-actions-are-prefixed-with-do)).

#### JavaScript

Voir section __JavaScript__.

#### Locale

Voir section __Localisation__.

#### View

Dans le dossier `view` sont contenues toutes les ressources relatives aux différents widgets fournis par le module.
- `css`: contient tous les fichiers CSS.
- `locale`: contient tous les fichiers de langage (conernant uniquement les widgets).
- `tpl`: contient tous les fichiers template (.mtt) décrivant le html à produire.

#### Widget

Voir section __Widget__.

## Mécanismes

### Évènements

Voir section __Évènements__.

## Ajouter votre propre module

Beluga contient un binaire (nommé run.n) permettant son intégration dans l'outil `Haxelib`. Celui-ci propose, entre autres, de générer un module contenant l'architecture minimale et fonctionnelle.
Cet outil peut-être utilisé depuis la commande suivante:
> haxelib run beluga create_module "nom_du_module"

Ceci génère alors un module suivant les conventions expliquées précédemment et directement dans le dossier `beluga/module` de votre installation de la bibliothèque Beluga.