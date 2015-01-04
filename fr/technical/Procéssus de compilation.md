#Procéssus de compilation

En haxe il y a plusieurs phases de compilation dont Beluga tir partie.
Nous décrirons pour chaque étape les actions qui sont éffectuées par beluga.

[OnGenerate] --> [Build] --> [Macro] --> [OnAfterGenerate] --> [Fichier de build]

##OnGenerate
Sont toutes les fonctions appelées au début de la génération
Aucune fonction Beluga n'est appelé lors de cette phase

##Build
Cette phase sert a générer certains types

| Fonctions | Description |
|-----------------------------------------------------------------------------------------------|
|ModuleBulder.registerModule()	    | Déclaration de tous les modules au prés de Beluga         |
|SessionFlashData.build()		    | Génération des attributs session et flashdata             |
|Database.registerModel()		    | Déclaration model                                         |
|CssBuilder.readCssMetadata()	    | Décaration des fichers et dossiers contenant le Css       |
|JavascriptBuilder.buildScript()	| Déclaration des classes Haxe a compiler en Javascript     |
|ConfigLoader.build()               | Chargement du fichier de config beluga.xml                |
|ValidateMacro.build()              | Génération des fonctions de validation de formulaire      |

##Macro
Les fonctions macro sont ensuite appelées

| Fonctions | Description |
|-----------------------------------------------------------------------------------------------|
|ResourceManager.register()     | Copie des fichiers de ressources                              |
|JavascriptBuilder.compile()    | Génération du fichier beluga.js                               |
|CssBuilder.compile()           | Génération du fichier beluga.css                              |
|Config.autoCreateFile()        | Génération fichiers de configuration pour chaque module       |
|BelugaI18n.loadI18nFolder()    | Chargement des fichiers d'i18n                                |

##OnAfterGenerate
Sont des fonctions appelées aprés cette phase de Génération
Aucune fonction Beluga n'est appelée lors de cette phase
