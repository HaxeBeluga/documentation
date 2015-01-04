#Localisation

Beluga implémente son propre système de localisation.

##Utilisation simple
Tout d'abord il faut créer un dossier contenant tous les fichiers de localisation quelque part dans l'arborescence de Beluga.
Le dossier et son contenu doivent ressembler à ca :
```
local
|-- en_US.json
`-- fr_FR.json
```
Chaque fichier est un fichier au format .json et ne doit contenir qu'une seule langue.
Le contenu d'un fichier est comme ceci :

```json
{
    "key": "Valeur",
        "password": "Mot de passe",
        "alreadyLogged": "Vous êtes déja connecté"
}
```

Récupérer une valeur et changer de langue le code source se fait ainsi :
```haxe
i18n = BelugaI18n.loadI18nFolder("path/to/local/");
Sys.println(i18n.password); //Affiche "Mot de passe"
BelugaI18n.curLang = "en_US";
Sys.println(i18n.password); //Affiche maintenant "Password"
```

##Héritage
Il est possible de hiérarchiser plusieurs dossiers de local. Imaginons les deux fichiers suivants :

*local_father/fr_FR.json*
```json
{
    "family": "On est de la famille des Locals",
        "hello": "Bonjour je suis le père !"
}
```

*local_child/fr_FR.json*
```json
{
    "hello": "Bonjour je suis le fils !"
}
```

Nous pouvons maintenant coder ainsi :
```haxe
father = BelugaI18n.loadI18nFolder("local_father");
child = BelugaI18n.loadI18nFolder("local_child", father);

    Sys.println(father.hello) //Affiche "Bonjour je suis le père !"
Sys.println(father.family)//Affiche "On est de la famille des Locals"

    Sys.println(child.hello) //Affiche "Bonjour je suis le fils !"
Sys.println(child.family)//Affiche "On est de la famille des Locals"
```

##Application dans un Module Beluga
Beluga a 3 niveaux de local :
* les locals globales à Beluga : Beluga.i18n
* les locals spécifiques au module : MonModule.i18n
* les locals spécifiques au widget : MonWidget.i18n

Bien évidemment, *MonWidget.i18n* hérite de *MonModule.i18n* qui, lui-même, hérite de *Beluga.i18n*.