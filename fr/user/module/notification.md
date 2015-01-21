Module - Notification
=====================

Le module de __notification__ vous permet de créer et de gérer des notifications facilement. Il dépend du module de __compte__ fourni par Beluga donc vous ne pourrez pas vous servir du module de __notification__ sans lui.

Ce module fournit un certain nombre de fonctions pour l'intégrer facilement dans votre projet.

### Fonctions

```Haxe
public function print(args : {id : Int}) : Void
public function create(args : {
    title : String,
    text : String,
    user_id : Int
}) : Void
public function delete(args : {id : Int}) : Void
public function getNotifications() : Array<NotificationModel>
public function getNotification(notif_id: Int, user_id: Int) : NotificationModel
public function canPrint(notif_id: Int) : Bool
```

*public function print(args : {id : Int}) : Void*

Cette fonction prend en paramètre l'identifiant de la notification. Elle renvoie le signal `print`. Ensuite il vous suffit d'utiliser le widget Print.

```Haxe
public function create(args : {
		title : String,
		text : String,
		user_id : Int
	}) : Void
```

Cette fonction crée une nouvelle notification en recevant en paramètres son titre, sa description et l'identifiant de l'utilisateur à qui elle est destinée.

*public function delete(args : {id : Int}) : Void*

La fonction `delete` prend en paramètre l'identifiant de la notification que vous souhaitez supprimer.

*public function getNotifications() : Array<NotificationModel>*

Cette fonction retourne la liste des notifications de l'utilisateur courant.

*public function getNotification(notif_id: Int, user_id: Int) : NotificationModel*

Cette fonction retourne la notification référencée par l'identifiant passé en paramètre si elle appartient à celui-ci. Sinon, elle retourne *null*.

*public function canPrint(notif_id: Int) : Bool*

Cette fonction renvoie *true* si la notification référencée par l'identifiant passé en paramètre appartient bien à l'utilisateur courant.

### Erreurs

En cas d'échec, veuillez vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module de notification :

 * __MissingLogin__ : Vous devez être connecté.
 * __MissingTitle__ : Il manque le titre.
 * __MissingMessage__ : Il manque le message.
 * __IdNotFound__ : La notification n'a pas été trouvée.
 * __None__ : Aucune erreur détectée.

### A propos des évènements

Ces fonctions lancent toutes des évènements en cas de succès ou d'échec. Ces évènements sont facilement reconnaissables et suivent un même patron : le nom de l'action + un suffixe. Par exemple, les évènements dans le cas de la fonction `delete` seront *delete__Fail__* et *delete__Success__*.