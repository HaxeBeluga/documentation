Module - Notification
=====================

Le module de __notification__ vous permet de créer et de gérer des notifications facilement. Il dépend du module de __compte__ fourni par Beluga donc vous ne pourrez pas vous servir du module de __notification__ sans lui.

Ce module fournit un certain nombre de méthodes pour l'intégrer facilement dans votre projet.

Voici la liste des méthodes fournies par ce module :

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

##Signaux

Ce module peut renvoyer les signaux suivants :

* defaultNotification
* createSuccess
* createFail
* deleteSuccess
* deleteFail
* print

##Erreurs

En cas d'échec, veuillez vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module de notification :

 * __MissingLogin__ : Vous devez être connecté.
 * __MissingTitle__ : Il manque le titre.
 * __MissingMessage__ : Il manque le message.
 * __IdNotFound__ : La notification n'a pas été trouvée.
 * __None__ : Aucune erreur détectée.

##Description des méthodes

Par exemple, la méthode `delete` peut renvoyer le signal `deleteSuccess` ou `deleteFail`. Ensuite, il vous suffit d'effectuer l'action que vous souhaitez selon le résultat retourné. N'oubliez pas de vérifier le code d'erreur pour savoir ce qui n'a pas fonctionné en cas d'échec.

```Haxe
public function print(args : {id : Int}) : Void
```

Cette méthode prend en paramètre l'identifiant de la notification. Elle renvoie le signal `print`. Ensuite il vous suffit d'utiliser le widget Print.

```Haxe
public function create(args : {
		title : String,
		text : String,
		user_id : Int
	}) : Void
```

Cette méthode crée une nouvelle notification en recevant en paramètre son titre, sa description et l'identifiant de l'utilisateur à qui elle est destinée. Elle renvoie le signal `createSuccess` ou `createFail`.

```Haxe
public function delete(args : {id : Int}) : Void
```

La méthode `delete` prend en paramètre l'identifiant de la notification que vous souhaitez supprimer. Elle renvoie le signal `deleteSuccess` ou `deleteFail`.

```Haxe
public function getNotifications() : Array<NotificationModel>
```

Cette méthode retourne la liste des notifications de l'utilisateur courant.

```Haxe
public function getNotification(notif_id: Int, user_id: Int) : NotificationModel
```

Cette méthode retourne la notification référencée par l'identifiant passé en paramètre si elle appartient à celui-ci. Sinon, elle retourne *null*.

```Haxe
public function canPrint(notif_id: Int) : Bool
```

Cette méthode renvoie true si la notification référencée par l'identifiant passé en paramètre appartient bien à l'utilisateur courant.