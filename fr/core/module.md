# Module

Ici, nous allons voir en détail tout ce qui couvre les modules de Beluga de façon générale. En premier, nous verons qu'est-ce qu'ils _sont_ et _comment_ ils sont organisés. Ensuite, nous nous pencherons sur la façon dont ils s'intègre à Beluga. Une fois ceci en main, nous apprendrons comment rajouter vos propres modules.

## Concept

Les modules de beluga sont la partie contenant les fonctionnalités proposées à l'utilisateur. Celles-ci étant regroupées en modules de par leur dépendences. ex: la fonctionnalité `enregistrer utilisateur` et `connecter utilisateur` sont réunies au sein du module `account`.
Ce découpage en module permet aux dévelopeur de n'embarquer que le code contenant les fonctionnalitées qu'il désire utiliser, et donc d'ajuster le poids de Beluga par rapport à l'utilisation qui en est faite.

## Structure

Dans Beluga, nous avons choisis de rendre le plus facile possible aux collaborateurs d'ajouter de nouveaux modules. Pour cette raison, nous suivons le paradigme de _convention over configuration_. Concrètement, cela signifie que certains dossiers, fichiers et functions sont nécessaire pour que Beluga soit en mesure de détecter et d'utiliser automatiquement les différentes fonctionalités des modules.
De plus, nous suivons une convention de nommage très stricte permettant de facilement pouvoir naviguer d'un module à l'autre. Afin de mieux illustrer la différence entre les conventions _simples_ et celles _nécessaires_, ces dernières seront précédées d'un mot en __gras__. 

Le seul défaut de cette approche est qu'elle rend plus dure, au premier abord, de trouver pourquoi votre module n'est pas entièrement reconnu par Beluga. Pour cette raison, nous avons créé un script d'auto-génération d'un module (cf: Ajouter votre propre module).

### Filesystem

Les modules se trouvent sous le dossier `beluga/module`. Ils __doivent__ respecter l'architecture dossier minimale suivante afin d'être correctement reconnus et chargés par Beluga:

``` 
module_root/
│
│─── api/          : API used by Beluga dispatcher
│─── js/           : Javascript files
│─── locale/       : JSon files for localization 
│─── view/         : All files related to the html output
     │─── css/
     │─── locale/
     └─── tpl/
└─── widget/       : Widgets class files
```
Les autres dossiers couremment utilisés, tels que `exception` et `model`, sont purement présent dans un soucis d'organisation et d'esthétique.

### Détails du contenu des dossiers

#### Racine du module

À la racine du module, __doivent__ être exposées sont interface (simplement nommée avec le nom du module) et son implémentation (nom du module + "Impl"). Ces deux fichiers **doivent** respectivement étendre `Module` et `ModuleImpl`.
ex:

```
    interface Account extends Module {}
    [...]
    class AccountImpl extends ModuleImpl {}
```
Un module *devrait* aussi fournir deux classes contenantes:
- nom du module + "Triggers": contient tous les triggers succeptible d'être soulevés.
- nom du module + "Widgets": contient tous les widgets.

Ces deux classes sont ensuite exposées au développeur depuis l'interface du module. ex:
```haxe
interface Account extends Module {
    public var triggers : AccountTrigger;
    public var widgets : AccountWidget;
}
[...]
```
Ensuite, les triggers et widgets peuvent être facilement, et logiquement, accédés par la ligne suivante:

```haxe
beluga.getModuleInstance(Account).widgets.loginForm
```

#### API

Dans le dossier `api`, il **doit** se trouver un fichier de classe contenant une api pour le dispatcher web de Beluga (nommé nom du module + "Api"). Puisque *c'est* un fichier de web api, les fonctions de routages __doivent__ commencer par "do" (voir la docummentation officielle [Haxe Web Disptacher](http://old.haxe.org/manual/dispatch#why-actions-are-prefixed-with-do)).

#### Js

(intégrer en fonction de la documentation de jimmy)

#### Locale

(intégrer en fonction de la documentation d'Alexis)

#### View

Dans le dossier `view` sont contenues toutes les ressources relatives aux différents widgets fournis par le module.
- `css`: contient tous les fichiers CSS.
- `locale`: contient tous les fichiers de language (conernant uniquement les widgets)
- `tpl`: contient tous les fichiers template (.mtt) décrivant le html à produire

#### Widget

(intégrer en fonction de la documentation d'Alexis)

## Mecanismes

### Triggers

(intégrer en fonction de la documentation d'Alexis)

### Erreurs

Les erreurs rencontrées internalement des modules sont toutes gérées de la même façon. Celles-ci sont remontées à l'utilisateur en utilisant le système de triggers et celui de langage. Une fois capturé, le trigger fournis un code correspondant à l'erreur rencontrée. Ce code est issue d'une énumération _couremment_ nommée: nom du module + "Error" + "Kind".
Les modules _devraient_ aussi fournir une méthod permettant de transformer ce code en une erreur lisible par un humain. Par exemple:
```haxe
    private function getErrorString(error: ModuleErrorKind): String {
        return switch (error) {
            case ErrorTrigger1: BelugaI18n.getKey(i18n, "erreur1");
    }
```
De cette façon, le développeur peut, s'il le souhaite, directement, et facilement, intégrer cette erreur dans son site. Ou bien redéfinir lui même le comportement à effectuer pour gérer l'erreur.

## Ajouter votre propre module

Beluga contient un binaire (nommé run.n) permettant son intégration dans l'outil `Haxelib`. Celui-ci propose, entre autre, de générer un module contenant l'architecture minimale et fonctionnelle.
Cet outil peut-être utilisé depuis la commande suivante:
> haxelib run beluga create_module "nom_du_module"

Ceci génère alors un module suivant les conventions expliquées précédemment et directement dans le dossier `beluga/module` de votre installation de la bibliothèque Beluga.