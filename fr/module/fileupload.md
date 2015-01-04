Module - Transfert de fichiers
==============================

Le module de __transfert de fichier__ vous permet de facilement intégrer dans votre site internet un gestionnaire de téleversement et téléchargement de fichier.

Le module de compte de beluga est nécessaire pour le bon fonctionnement de ce module, en effet une verification de l'utilisateur est réalisé avant chaque téléchargement ou televersement de fichier afin de garantir la sécurité des fichiers des utilisateurs.


Voici une liste des différentes fonctionnalités proposées par le module de transfert de fichiers.

### Widgets

```Haxe
public function display(): Void;
public function admin(): Void;
```

Ces deux fonctions sont gérées par le diffuseur d'évènement web de beluga, et permettre de signaler au développeur que l'utilisateur du site internet demande l'accès respectivement au widget d'envoie de fichier, ou au widget de gestion des envoient de fichier.

Ces deux fonctions lancent respectivement les évènements:

* `display`
* `admin`


### Fonctions disponibles

```Haxe
public function send(): Void;
public function delete(args: { id: Int }): Void;
public function addextension(args: { name: String }): Void;
public function deleteextension(args: { id: Int }): Void;
public function getUserFileList(user_id: Int): List<Dynamic>;
public function extensionIsValid(name: String): Bool;
```

*public function send(): Void* :

La fonction send, est une fonction utilisée uniquement en interne du module d'envoie de fichier.
Elle est appelée depuis le widget d'envoie de fichier, et va permettre de transférer un fichier utilisateur sur le serveur. Cette fonction est liée au module de compte afin d'authentifier l'utilisateur et d'assurer l'autorisation de son access a ce service.

*public function delete(args: { id: Int }): Void* :

La fonction delete, permet de supprimer un fichier utilisateur grace a l'id du fichier. Une verification est fait au préalable afin de verifier que la requete de suppression vient bien de l'utilisateur lui meme.

*public function addextension(args: { name: String }): Void* :

*public function deleteextension(args: { id: Int }): Void* :

Ces deux fonctions permettent de gérer les extensions de fichier autorisée pour l'envoie de fichier sur le serveur du site.

*public function getUserFileList(user_id: Int): List<{name: String, id: Int}>* :

Cette fonction permet d'obtenir la liste complete des fichier 

*public function extensionIsValid(name: String): Bool* :

Enfin cette dernière fonction permet au développer de verifier la validité d'une extension, mais aussi que celle ci n'existe pas deja dans la base de données du site internet.


### A propos du fonctionnement interne du module

Toutes ces fonction son prises en compte automatiquement par le diffuseur d'évènement web de beluga afin de rendre les widgets totalement autonome, mais peuvent aussi être appelé directement par le développeur.

Enfin chacune de ces fonctions lancent des évènements afin de notifier le développeur du succès ou échec de l'action associée.

Chacun de ces évènements prend la forme du nom de la fonction ainsi que d'un suffix permettant de specifier le résultat de l'action. par example dans le cas de l'appel a la fonction `delete`, si le suppression reussi alors l'évènement lancé sera *delete__Success__*, au contraire si la suppression echoue, l'évènement sera *delete__Fail__*.