Module - News
=============

Le module de __nouvelles__ vous permet de créer et de gérer des news (nouvelles) facilement. Si vous voulez poster/éditer un article ou un commentaire, vous devrez utiliser le module de __compte__ fourni par Beluga.

Ce module fournit un certain nombre de méthode pour l'intégrer facilement dans votre projet.

Voici la liste des méthodes fournies par ce module :

```Haxe
public function create(args : {title : String, text : String}) : Void
public function delete(args : {news_id : Int}) : Void
public function edit(args : {news_id : Int, title : String, text : String}) : Void
public function addComment(args : {news_id : Int, text : String}) : Void
public function deleteComment(args : {news_id : Int, comment_id : Int}) : Void
public function canEdit(news_id: Int, user_id: Int) : Bool
public function canPrint(news_id: Int) : Bool
public function getAllNews() : Array<NewsModel>
public function getNewsFromUser(user_id : Int) : Array<NewsModel>
public function getComments(news_id : Int) : Array<CommentModel>
```

##Signaux

Ce module peut renvoyer les signaux suivants :

* redirect
* redirectEdit
* defaultNews
* print
* editFail
* editSuccess
* addCommentFail
* addCommentSuccess
* deleteCommentFail
* deleteCommentSuccess
* deleteFail
* deleteSuccess
* createFail
* createSuccess

##Erreurs

En cas d'échec, veuillez vérifier le code d'erreur pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module de __nouvelles__ :

 * __MissingLogin__ : Vous devez être connecté.
 * __NewsNotFound__ : La news demandée n'a pas été trouvée.
 * __CommentNotFound__ : Le commentaire demandé n'a pas été trouvé.
 * __NotAllowed__ : Vous ne pouvez pas effectuer cette action.
 * __MissingMessage__ : Il manque le message.
 * __MissingTitle__ : Il manque le titre.
 * __None__ : Aucune erreur détectée.


##Description des méthodes

Par exemple, la méthode `create` renvoie les signaux `createSuccess` et `createFail` selon si la création s'est bien déroulée ou non. Ensuite, il vous suffit d'effectuer l'action que vous souhaitez selon le résultat retourné. N'oubliez pas de vérifier le code d'erreur pour savoir ce qui n'a pas fonctionné en cas d'échec.

```Haxe
public function create(args : {title : String, text : String}) : Void
```

La méthode `create` vous permet de créer une news. Elle prend en paramètre le titre de l'article et son texte. Elle peut renvoyer le signal `createSuccess` ou `createFail`. Vous devez être connecté pour pouvoir utiliser cette méthode.

```Haxe
public function edit(args : {news_id : Int, title : String, text : String}) : Void
```

La méthode `edit` vous permet de modifier une news. Elle prend trois paramètres : l'identifiant de la news que vous souhaitez éditer, le nouveau titre et le nouveau texte. Elle renvoie le signal `editSuccess` ou `editFail`. Vous devez être connecté pour pouvoir utiliser cette méthode.

```Haxe
public function addComment(args : {news_id : Int, text : String}) : Void
```

La méthode `addComment` permet d'ajouter un commentaire sur une news. Elle prend deux paramètres : l'identifiant de la news sur laquelle vous souhaitez ajouter le commentaire et le texte du commentaire. Elle renvoie le signal `addCommentSuccess` ou `addCommentFail`. Vous devez être connecté pour pouvoir utiliser cette méthode.

```Haxe
public function deleteComment(args : {news_id : Int, comment_id : Int}) : Void
```

La méthode `deleteComment` permet de supprimer un commentaire. Elle prend deux paramètres : l'identifiant de la news du commentaire et celui du commentaire. Elle renvoie le signal `deleteCommentSuccess` ou `deleteCommentFail`. Pour pouvoir utiliser cette méthode, vous devez être connecté et être le créateur de la news ou le créateur du commentaire, ou encore être un administrateur.

```Haxe
public function delete(args : {news_id : Int}) : Void
```

La méthode `delete` permet de supprimer une news. Elle prend en paramètre l'identifiant de la news que vous souhaitez supprimer. Elle renvoie le signal `deleteFail` ou `deleteSuccess`. Vous devez être connecté et être le créateur de la news, ou être un administrateur.

```Haxe
public function getAllNews() : Array<NewsModel>;
```

Cette méthode renvoie la liste de toutes les news crées (qui peuvent bien évidemment être vides).

```Haxe
public function getNewsFromUser(args : {user_id : Int}) : Array<NewsModel>;
```

Cette méthode renvoie la liste de toutes les news (qui peuvent bien évidemment être vides) créées par l'utilisateur référencé par l'identifiant.

```Haxe
public function getComments(args : {news_id : Int}) : Array<CommentModel>;
```

Cette méthode retourne la liste des commentaires (qui peuvent bien évidemment être vides) de la news référencée par l'identifiant.

```Haxe
public function canEdit(news_id: Int, user_id: Int) : Bool
```

La méthode `canEdit` renvoie true si l'utilisateur donné peut éditer la news donnée. Donc si l'utilisateur est le créateur de la news ou un administrateur, la méthode renverra true.

```Haxe
public function canPrint(news_id: Int) : Bool
```

La méthode `canPrint` retourne true si la news existe.