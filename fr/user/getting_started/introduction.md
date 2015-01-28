Comment débuter
===============

## Première utilisation

### Pré-requis

L'installation de __Beluga__ nécessite les programmes suivants sur votre ordinateur :

* haxe 3.1.3
* mysql
* php
* apache
* git

Actuellement, __Beluga__ supporte les bases de données MySQL, cependant il peut compiler aussi bien sur _neko_ que _PHP_. Ce document utilisera _PHP_ afin d'en simplifier les instructions.

### Installation de Haxe

Dans un premier temps, télechargez la distribution `Haxe` pour votre système depuis le site officiel: [http://haxe.org/download/].

Téléchargez aussi un serveur "Apache", une base de données MySQL et PHP en les prenant à part ou en téléchargeant un pack contenant les trois outils mais il doit être adapté à votre système d'exploitation (WAMP pour Windoxs, LAMA pour Linux, MAMP pour MacOSX ...).

Enfin, téléchargez git : [http://git-scm.com/downloads].


### Installation de _Beluga_

Il est possible d'installer __Beluga__ à l'aide de l'outil "Haxelib", disponible avec la distribution __Haxe__. Cette simple ligne de commande permet d'installer __Beluga__ sur votre système :

```Shell
> haxelib git beluga https://github.com/HaxeBeluga/Beluga
```

### Générer un nouveau projet

Afin de créer un nouveau projet, il vous suffit de suivre les étapes suivantes.

Allez dans `beluga/haxelib/` et tapez la ligne de commande suivante :

```Shell
> haxe beluga.hxml
```

Cela a pour effet de générer un fichier `run.n`.

Dirigez-vous ensuite dans le dossier `beluga/module_src/` et faites :

```Shell
> haxelib dev beluga .
```

Enfin, tapez (de préférence à la racine du projet) la commande pour créer le projet :

```Shell
> haxelib run beluga setup_project TestProject
```

Différents fichiers sont générés :

```
TestProject
|
│───.htaccess : un fichier htaccess par défaut permettant la réécriture d'URL
│───beluga.xml : Le fichier de configuration de beluga
│───TestSetupProject.hxml : Le fichier permettant la compilation d'un projet Haxe
│
└───src
     |───Main.hx : Point d'entrée du projet.
```

### Configuration du projet

Il est nécessaire d'éditer le fichier de configuration `beluga/test/config/database.xml` de votre projet. Celui-ci permet de configurer votre base de données :

```xml
<database>
	<host>localhost</host>
	<!-- <port></port> -->
	<user>root</user>
	<pass></pass>
	<database>belugaTest</database>
</database>
```

Dans MySQL, créez une base de donnée nommée `belugaTest`

### Lancer le projet

Allez dans le dossier `beluga/core_src/` et tapez :

```Shell
> haxelib dev beluga-core .
```

Rendez-vous ensute dans le dossier TestProject, puis compilez le projet à l'aide de la commande suivante :

```Shell
> haxe TestSetupProject.hxml
```

- Déplacez le fichier `.htaccess` dans le dossier `bin`
- Déplacez les fichiers générés contenus dans le dossier `bin` à la racine du `document root` de votre serveur Apache.
- N'oubliez pas d'activer le module d'`url rewriting` de votre serveur apache.


Vous pouvez à présent accéder à votre site de test qui devrait afficher un formulaire d'inscription.