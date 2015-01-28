Module - Compte
================

Le module de __compte__ vous permet de gérer des comptes facilement.

Ce module fournit un certain nombre de méthodes pour l'intégrer facilement dans votre projet.

### Fonctions

```Haxe
public function subscribe(args : {
    login : String,
    password : String,
    password_conf : String,
    email : String
}) : Void
```

Cette fonction permet de créer un nouvel utilisateur. Elle prend en paramètre le login, le mot de passe, la confirmation du mot de passe et l'email.

```Haxe
public function login(args : {
    login : String,
    password : String
}) : Void
```

Cette fonction permet de connecter un utilisateur. Elle prend en paramètre un login et un mot de passe.

*public function deleteUser(args : {id : Int}) : Void*

Cette fonction permet de supprimer l'utilisateur référencé par l'identifiant passé en paramètre.

*public function getUser(userId : SId) : User*

Cette fonction retourne l'utilisateur référencé par l'identifiant passé en paramètre ou *null* si aucun n'est trouvé.

*public function getSponsor(userId : SId) : User*

Cette fonction retourne le sponsor de l'utilisateur référencé par l'identifiant passé en paramètre.

*public function getDisconnectedUsers() : Array<User>*

Cette fonction retourne la liste des autres utilisateurs (donc pas celui qui est courant).

*public function getFriends(user_id: Int) : Array<User>*

Cette fonction retourne la liste des amis de l'utilisateur référencé par l'identifiant passé en paramètre.

*public function getNotFriends(user_id: Int) : Array<User>*

Cette fonction retourne la liste des utilisateurs qui ne sont pas amis avec l'utilisateur référencé par l'identifiant passé en paramètre.

*public function getBlackListed(user_id: Int) : Array<User>*

Cette fonction retourne la liste des utilisateurs qui ont été blacklistés par l'utilisateur référencé par l'identifiant passé en paramètre.

*public function logout() : Void*

Cette fonction permet de déconnecter l'utilisateur courant.

*public function getLoggedUser() : User*

Cette fonction retourne l'utilisateur courant ou *null* si aucun utilisateur n'est connecté.

*public function edit(user_id: Int, email : String) : Void*

Cette fonction permet d'éditer le compte de l'utilisateur référencé par l'identifiant passé en paramètre.

*public function ban(user_id: Int) : Void*

*public function unban(user_id: Int) : Void*

Ces deux fonctions permettent de bannir ou de débannir un utilisateur. Uniquement utilisable par un administrateur.

*public function friend(user_id: Int, friend_id: Int) : Void*

*public function unfriend(user_id: Int, friend_id: Int) : Void*

Ces deux fonctions permettent d'ajouter ou d'enlever un utilisateur de sa liste d'amis.

*public function blacklist(user_id: Int, friend_id: Int) : Void*

*public function unblacklist(user_id: Int, friend_id: Int) : Void*

Ces deux fonctions permettent d'ajouter ou d'enlever un utilisateur de sa blacklist.

### A propos des évènements

Ces fonctions lancent toutes des évènements en cas de succès ou d'échec. Ces évènements sont facilement reconnaissables et suivent un même patron : le nom de l'action + un suffixe. Par exemple, les évènements dans le cas de la fonction `login` seront *login__Fail__* et *login__Success__*.