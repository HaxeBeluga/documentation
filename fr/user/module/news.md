Module - Information
====================

Le module d'__information__ vous permet de créer et de gérer des news facilement. Si vous voulez poster / éditer / éditer un article ou un commentaire, vous devrez utiliser le module de __compte__ fourni par Beluga.

Ce module fournit un certain nombre de fonctions pour l'intégrer facilement dans votre projet.

### Fonctions

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

*public function create(args : {title : String, text : String}) : Void*

Cette fonction vous permet de créer une news. Elle prend en paramètre le titre de l'article et son texte. Vous devez être connecté pour pouvoir utiliser cette méthode.

*public function edit(args : {news_id : Int, title : String, text : String}) : Void*

La fonction `edit` vous permet de modifier une news. Elle prend trois paramètres : l'identifiant de la news que vous souhaitez éditer, le nouveau titre et le nouveau texte. Vous devez être connecté pour pouvoir utiliser cette méthode.

*public function addComment(args : {news_id : Int, text : String}) : Void*

La fonction `addComment` permet d'ajouter un commentaire sur une news. Elle prend deux paramètres : l'identifiant de la news sur laquelle vous souhaitez ajouter le commentaire et le texte du commentaire. Vous devez être connecté pour pouvoir utiliser cette méthode.

*public function deleteComment(args : {news_id : Int, comment_id : Int}) : Void*

La fonction `deleteComment` permet de supprimer un commentaire. Elle prend deux paramètres : l'identifiant de la news du commentaire et celui du commentaire. Pour pouvoir utiliser cette méthode, vous devez être connecté et être le créateur de la news ou le créateur du commentaire, ou encore être un administrateur.

*public function delete(args : {news_id : Int}) : Void*

La fonction `delete` permet de supprimer une news. Elle prend en paramètre l'identifiant de la news que vous souhaitez supprimer. Vous devez être connecté et être le créateur de la news, ou être un administrateur.

*public function getAllNews() : Array<NewsModel>;*

Cette fonction renvoie la liste de toutes les news créées (qui peuvent bien évidemment être vides).

*public function getNewsFromUser(args : {user_id : Int}) : Array<NewsModel>;*

Cette fonction renvoie la liste de toutes les news (qui peuvent bien évidemment être vides) créées par l'utilisateur référencé par l'identifiant.

*public function getComments(args : {news_id : Int}) : Array<CommentModel>;*

Cette fonction retourne la liste des commentaires (qui peuvent bien évidemment être vides) de la news référencée par l'identifiant.

*public function canEdit(news_id: Int, user_id: Int) : Bool*

Cette fonction renvoie *true* si l'utilisateur donné peut éditer la news donnée. Donc si l'utilisateur est le créateur de la news ou un administrateur, la méthode renverra *true*.

*public function canPrint(news_id: Int) : Bool*

La fonction `canPrint` retourne *true* si la news existe.

### Erreurs

En cas d'échec, veuillez vérifier le code d'erreur pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module d'__information__ :

 * __MissingLogin__ : Vous devez être connecté.
 * __NewsNotFound__ : La news demandée n'a pas été trouvée.
 * __CommentNotFound__ : Le commentaire demandé n'a pas été trouvé.
 * __NotAllowed__ : Vous ne pouvez pas effectuer cette action.
 * __MissingMessage__ : Il manque le message.
 * __MissingTitle__ : Il manque le titre.
 * __None__ : Aucune erreur détectée.

### A propos des évènements

Ces fonctions lancent toutes des évènements en cas de succès ou d'échec. Ces évènements sont facilement reconnaissables et suivent un même patron : le nom de l'action + un suffixe. Par exemple, les évènements dans le cas de la fonction `create` seront *create__Fail__* et *create__Success__*.