Module - Account
================

Le module d'__acompte__ vous permet de gérer des comptes facilement.

Ce module fournit un certain nombre de méthodes pour l'intégrer facilement dans votre projet.

Voici la liste des méthodes fournies par ce module :

```Haxe
public function subscribe(args : {
    login : String,
    password : String,
    password_conf : String,
    email : String
}) : Void
public function login(args : {
    login : String,
    password : String
}) : Void
public function deleteUser(args : {id : Int}) : Void
public function getUser(userId : SId) : User
public function getSponsor(userId : SId) : User
public function getDisconnectedUsers() : Array<User>
public function getUsers2(): List<User>
public function getFriends(user_id: Int) : Array<User>
public function getNotFriends(user_id: Int) : Array<User>
public function getBlackListed(user_id: Int) : Array<User>
public function showUser(args: { id: Int}): Void
public function logout() : Void
public function getLoggedUser() : User
public function edit(user_id: Int, email : String) : Void
public function ban(user_id: Int) : Void
public function unban(user_id: Int) : Void
public function friend(user_id: Int, friend_id: Int) : Void
public function unfriend(user_id: Int, friend_id: Int) : Void
public function blacklist(user_id: Int, friend_id: Int) : Void
public function unblacklist(user_id: Int, friend_id: Int) : Void
```

##Signaux

Ce module peut renvoyer les signaux suivants :

 * loginFail
 * loginSuccess
 * afterLogout
 * subscribeFail
 * subscribeSuccess
 * deleteFail
 * deleteSuccess
 * editFail
 * editSuccess
 * banFail
 * banSuccess
 * unbanFail
 * unbanSuccess
 * friendFail
 * friendSuccess
 * unfriendFail
 * unfriendSuccess
 * blacklistFail
 * blacklistSuccess
 * unblacklistFail
 * unblacklistSuccess

##Description des méthodes

```Haxe
public function subscribe(args : {
    login : String,
    password : String,
    password_conf : String,
    email : String
}) : Void
```

La méthode *subscribe* permet de créer un nouvel utilisateur. Elle prend en paramètre le login, le mot de passe, la confirmation du mot de passe et l'email. Elle renvoie le signal `subscribeFail` ou le signal `subscribeSubscribe`.

```Haxe
public function login(args : {
    login : String,
    password : String
}) : Void
```

Cette méthode permet de connecter un utilisateur. Elle prend en paramètre un login et un mot de passe. Elle renvoie le signal `loginFail` ou le signal `loginSuccess`.

```Haxe
public function deleteUser(args : {id : Int}) : Void
```

La méthode *deleteUser* permet de supprimer l'utilisateur référencé par l'identifiant passé en paramètre.

```Haxe
public function getUser(userId : SId) : User
```

Cette méthode retourne l'utilisateur référencé par l'identifiant passé en paramètre ou *null* si aucun n'est trouvé.

```Haxe
public function getSponsor(userId : SId) : User
```

Cette méthode retourne le sponsor de l'utilisateur référencé par l'identifiant passé en paramètre.

```Haxe
public function getDisconnectedUsers() : Array<User>
```

Cette méthode retourne la liste des autres utilisateurs (donc pas celui qui est courant).

```Haxe
public function getFriends(user_id: Int) : Array<User>
```

Cette méthode retourne la liste des amis de l'utilisateur référencé par l'identifiant passé en paramètre.

```Haxe
public function getNotFriends(user_id: Int) : Array<User>
```

Cette méthode retourne la liste des utilisateurs qui ne sont pas amis avec l'utilisateur référencé par l'identifiant passé en paramètre.

```Haxe
public function getBlackListed(user_id: Int) : Array<User>
```

Cette méthode retourne la liste des utilisateurs qui ont été blacklistés par l'utilisateur référencé par l'identifiant passé en paramètre.

```Haxe
public function logout() : Void
```

Cette méthode permet de déconnecter l'utilisateur courant. Elle retourne le signal `afterLogout`.

```Haxe
public function getLoggedUser() : User
```

Retourne l'utilisateur courant ou null si aucun utilisateur n'est connecté.

```Haxe
public function edit(user_id: Int, email : String) : Void
```

Cette méthode permet d'éditer le compte de l'utilisateur référencé par l'identifiant passé en paramètre. Elle renvoie le signal `editSuccess` ou le signal `editFail`.

```Haxe
public function ban(user_id: Int) : Void
public function unban(user_id: Int) : Void
```

Ces deux méthodes permettent de bannir ou de débannir un utilisateur. Uniquement utilisable par un administrateur.

```Haxe
public function friend(user_id: Int, friend_id: Int) : Void
public function unfriend(user_id: Int, friend_id: Int) : Void
```

Ces deux méthodes permettent d'ajouter ou d'enlever un utilisateur de sa liste d'amis.

```Haxe
public function blacklist(user_id: Int, friend_id: Int) : Void
public function unblacklist(user_id: Int, friend_id: Int) : Void
```

Ces deux méthodes permettent d'ajouter ou d'enlever un utilisateur de sa blacklist.