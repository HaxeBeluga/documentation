# Comment debuter

## Première utilisation

### Pre-requis
L'installation de __beluga__ nécessite les programmes suivants sur votre ordinateur:
* haxe 3.1.3
* mysql
* php
* apache
* git

Actuellement __beluga__ supporte les bases de données MySQL, cependant il peut compiler aussi bien sur _neko_ que _PHP_, ce document utilisera _PHP_ afin d'en simplifier les instructions.

### Installation de Haxe
Dans un premier temps, télechargez la distribution `Haxe` pour votre système depuis le site officiel: [http://haxe.org/download/].

### Installation de _beluga_

Il est possible d'installer __beluga__ à l'aide de l'outils haxelib, disponible avec la distribution __Haxe__, cette simple ligne de commande permet d'installer __beluga__ sur votre système. 
```Shell
> haxelib git beluga https://github.com/HaxeBeluga/Beluga
```

### Génèrer un nouveau projet
Afin de créer un nouveau projet, il vous suffi d'utiliser un des outils proposés avec __beluga__, pour cela la ligne de commande suffit:
```Shell
> haxelib run beluga setup_project TestProject
```

Différents fichiers sont générés:
```
TestProject
|
│───.htaccess : un fichier htaccess par défaut permettant la réécriture d'URL
│───beluga.xml : Le fichier de configuration de beluga
│───TestSetupProject.hxml : Le fichier permettant la compilation d'un projet Haxe.
│
└───src
     |───Main.hx : Point d'entrée du projet.
```

### Configuration du projet
Il est nécessaire d'éditer le fichier de configuration `config/database.xml` de votre projet, celui ci permet de configurer votre base de donnée:
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
Rendez vous dans le dossier TestProject, puis compilez le projet à l'aide de la commande suivant:
```Shell
> haxe TestSetupProject.hxml
```

- Déplacez le fichier `.htaccess` dans le dossier `bin`
- Déplacez les fichier générés contenus dans le dossier `bin` à la racine du `document root` de votre serveur apache.
- N'oubliez pas d'activer le module d'`url rewriting` de votre serveur apache.


Vous pouvez à présent accéder à votre site de test qui devrait afficher un formulaire d'inscription.