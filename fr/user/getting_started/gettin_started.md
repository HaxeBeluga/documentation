# Comment débuter

## Première utilisation

### Pré-requis
L'installation de __beluga__ nécessite les programmes suivants sur votre ordinateur:
* haxe 3.1.3
* mysql
* php
* apache
* git

--> *Voir le fichier "clone.md" situé dans le même répertoire que ce fichier pour savoir comment installer ces programmes, si besoin*

Actuellement, __Beluga__ supporte les bases de données MySQL, cependant il peut compiler aussi bien sur _neko_ que _PHP_. Ce document utilisera _PHP_ afin d'en simplifier les instructions.

### Installation de Haxe
Dans un premier temps, télechargez la distribution `Haxe` pour votre système depuis le site officiel: [http://haxe.org/download/].

### Installation de _Beluga_

Il est possible d'installer __Beluga__ à l'aide de l'outils "Haxelib", disponible avec la distribution __Haxe__. Cette simple ligne de commande permet d'installer __Beluga__ sur votre système :
```Shell
> haxelib git beluga https://github.com/HaxeBeluga/Beluga
```

### Générer un nouveau projet
Afin de créer un nouveau projet, il vous suffit d'utiliser un des outils proposés avec __Beluga__. Pour cela, tapez cette ligne de commande :
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
Il est nécessaire d'éditer le fichier de configuration `config/database.xml` de votre projet. Celui-ci permet de configurer votre base de données :
```
<database>
	<host>localhost</host>
	<!-- <port></port> -->
	<user>root</user>
	<pass></pass>
	<database>beluga_test</database>
</database>
```

Dans MySQL, créez une base de donnée nommée `beluga_test`

### Lancer le projet
Rendez-vous dans le dossier TestProject, puis compilez le projet à l'aide de la commande suivante :
```Shell
> haxe TestSetupProject.hxml
```

- Déplacez le fichier `.htaccess` dans le dossier `bin`
- Déplacez les fichier générés contenus dans le dossier `bin` à la racine du `document root` de votre serveur apache.
- N'oubliez pas d'activer le module d'`url rewriting` de votre serveur apache.


Vous pouvez à présent accéder à votre site de test qui devrait afficher un formulaire d'inscription.