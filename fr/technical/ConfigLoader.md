ConfigLoader
=============
-------------

La configuration dans Beluga est une composante essentielle au bon fonctionnement du Framework.

Le ConfigLoader **ne** se charge **pas** des configurations inhérentes aux modules mais uniquement de la configuration générale du Framework.

Ainsi, elle permet de configurer les éléments suivants

* L'accès à la base de donnée
* L'url de base du site (souvent `/`)
* Des configurations personnalisés

Fonctionnement général du ConfigLoader
--------------------------------------

Le ConfigLoader commence tout d'abord par charger le fichier `beluga.xml` qui doit se trouver à la racine du projet compilé.

Ensuite, une première lecture de ce fichier va être effectué à la recherche de la balise `include` et ce, afin de charger tous les fichiers de configuration.

Enfin, la configuration est chargée dans une variable `config` accessible via `ConfigLoader.config`. Il est par ailleurs possible de vérifier que la configuration à bien été chargée via `ConfigLoader.isReady`

Il est important de noter que tout ce processus est effectué **durant** la compilation du projet. La configuration ne sera donc pas éditable post-compilation.

Fichiers de configuration
-

Le fichier de base doit s'appler `beluga.xml`, celui que nous fournissons à titre d'exemple se contente de charger les autres fichiers de configuration afin de mieux organiser son projet

> **Exemple**
>     
	<include path="config/database.xml" />
	<include path="config/url.xml" />
	<include path="config/myconfig.xml" />

Les fichiers de configuration doivent respecter le format XML. Il n'est cependant pas nécessaire d'y mettre un header.

Balises
-

Liste des balises supportés

| Balise | Paramètres | Description |
| ------ | ---------- | ----------- |
| `include` | `path` | Cette balise permet de charger un autre fichier de configuration |
| toutes | `if` | Il s'agit d'un paramètre particulier applicable sur toutes les balises. Il convient de mettre la plateforme ciblé sur laquelle la balise sera applicable. (`neko` ou `php` en l'occurence) |

Il est possible d'assigner n'importe quelle variable à l'objet configuration ensuite.

> **Exemple**
>
	<url>
		<base value="Toto" />
	</url>

Dans l'exemple ci-dessus, la valeur `Toto` sera accessible dans le code via `ConfigLoader.config.url.base`

Configuration minimale
-

Il y a à un certain nombre de variables qui **doivent** êre remplies afin d'obtenir un projet fonctionnel, ainsi, la configuration minimale pour obtenir un projet fonctionnel est la suivante

	<url>
		<base value="" />
	</url>
	<database>
		<host>localhost</host>
		<!-- <port></port> -->
		<user>root</user>
		<pass></pass>
		<database>belugaTest</database>
		<!-- <socket></socket> -->
	</database>

Les variables port et socket étant optionnelles mais supportées par la base de donnée. Toutes les autres valeurs qui seront ajoutées dans la configuration seront inutilisées par Beluga mais néanmoins accessibles par les modules ou l'utilisateur de Beluga