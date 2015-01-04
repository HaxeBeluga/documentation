Processus de compilation
========================

En Haxe, il y a plusieurs phases de compilation dont Beluga tire partie.
Nous allons décrire, pour chacune de ces étapes, les différentes actions qui sont effectuées par Beluga.

[OnGenerate] --> [Build] --> [Macro] --> [OnAfterGenerate] --> [Fichier de build]

## OnGenerate
Ce sont les fonctions appelées au début de la génération du code Haxe.
Aucune fonction de Beluga n'est appelée lors de cette phase.

## Build
Cette phase sert a générer certains types

| Methode | Description |
| --------- | ---------------------------------------------------------------------------------- |
|ModuleBulder.registerModule()	    | Déclaration de tous les modules auprès de Beluga         |
|SessionFlashData.build()		    | Génération des attributs de session et flashdata             |
|Database.registerModel()		    | Déclaration des modèles                                         |
|CssBuilder.readCssMetadata()	    | Déclaration des fichers et dossiers contenant le CSS      |
|JavascriptBuilder.buildScript()	| Déclaration des classes Haxe à compiler en Javascript     |
|ConfigLoader.build()               | Chargement du fichier de configuration "beluga.xml"                |
|ValidateMacro.build()              | Génération des fonctions de validation de formulaire      |

## Macro
Les methodes macro sont ensuite appelées

| Fonctions | Description |
|----------- | ----------------------------------------------------------------------------------- |
|ResourceManager.register()     | Copie des fichiers de ressources                              |
|JavascriptBuilder.compile()    | Génération du fichier "beluga.js"                               |
|CssBuilder.compile()           | Génération du fichier "beluga.css"                              |
|Config.autoCreateFile()        | Génération des fichiers de configuration pour chaque module       |
|BelugaI18n.loadI18nFolder()    | Chargement des fichiers de traductions (i18n)                                |

## OnAfterGenerate
Ce sont des fonctions appelées après la phase de génération.
Aucune fonction de Beluga n'est appelée lors de cette phase.
