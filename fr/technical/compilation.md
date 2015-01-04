Procéssus de compilation
========================

En Haxe, il y a plusieurs phases de compilation dont Beluga tir partie.
Nous décrirons pour chaque étape les actions qui sont éffectuées par Beluga.

[OnGenerate] --> [Build] --> [Macro] --> [OnAfterGenerate] --> [Fichier de build]

## OnGenerate
Ce sont les fonctions appelées au début de la génération du code.
Aucune fonction de Beluga n'est appelée lors de cette phase.

## Build
Cette phase sert a générer certains types

| Fonctions | Description |
|-----------------------------------------------------------------------------------------------|
|ModuleBulder.registerModule()	    | Déclaration de tous les modules auprés de Beluga         |
|SessionFlashData.build()		    | Génération des attributs de session et flashdata             |
|Database.registerModel()		    | Déclaration  des modèles                                         |
|CssBuilder.readCssMetadata()	    | Déclaration des fichers et dossiers contenant le CSS      |
|JavascriptBuilder.buildScript()	| Déclaration des classes Haxe à compiler en Javascript     |
|ConfigLoader.build()               | Chargement du fichier de configuration "beluga.xml"                |
|ValidateMacro.build()              | Génération des fonctions de validation de formulaire      |

## Macro
Les fonctions macro sont ensuite appelées

| Fonctions | Description |
|-----------------------------------------------------------------------------------------------|
|ResourceManager.register()     | Copie des fichiers de ressources                              |
|JavascriptBuilder.compile()    | Génération du fichier "beluga.js"                               |
|CssBuilder.compile()           | Génération du fichier "beluga.css"                              |
|Config.autoCreateFile()        | Génération fichiers de configuration pour chaque module       |
|BelugaI18n.loadI18nFolder()    | Chargement des fichiers de traductions (i18n)                                |

##OnAfterGenerate
Ce sont des fonctions appelées aprés la phase de génération.
Aucune fonction de Beluga n'est appelée lors de cette phase.
