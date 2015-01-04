Module - Mail
=============

Le module d'__e-mail__ vous permet de créer et de gérer des mails facilement. Il dépend du module __compte__ fourni par Beluga.

Ce module fournit un certain nombre de méthodes pour l'intégrer facilement dans votre projet.

Voici la liste des méthodes fournies par ce module :

```
public function createDefaultContext() : Void
public function setActualMail(mail_id : Int) : Void
public function getActualMail() : MailModel
public function canPrint() : Bool
public function getSentMails() : Array<MailModel>
public function getMail(id : Int) : MailModel
public function getDraftMails() : Array<MailModel>
public function sendMail(args : {receiver : String, subject : String, message : String}) : Void
```

##Signaux

Ce module peut renvoyer les signaux suivants :
 * sendFail
 * sendSuccess

##Erreurs

En cas d'échec, vous n'avez qu'à vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module d'__e-mail__ :
 * __MissingLogin__ : Vous devez être connecté.
 * __MailNotSent__ : Une erreur s'est produite pendant l'envoi du mail.
 * __OnlyPHP__ : Le seul langage supporté par ce module est le PHP. N'importe quel autre langage échouera et renverra cette erreur.
 * __MissingReceiver__ : Le destinataire est manquant.
 * __MissingSubject__ : L'objet du mail est manquant.
 * __MissingMessage__ : Le message est manquant.
 * __UnknownId__ : L'identifiant reçu n'existe pas dans la base de données.
 * __None__ : Aucune erreur détectée.

##Description des méthodes

```Haxe
public function sendMail(args : {receiver : String, subject : String, message : String}) : Void
```

Cette méthode prend en paramètre l'adresse mail du destinataire, l'objet du mail, ainsi que le message. Elle renvoie le signal `sendSuccess` ou le signal `sendFail`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function getSentMails() : Array<MailModel>;
```

Cette méthode retourne la liste des mails envoyés de l'utilisateur courant (qui peut bien évidemment être vide).

```Haxe
public function getMail(id : Int) : MailModel;
```

Cette méthode retourne le mail lié à cet identifiant ou *null* s'il ne peut pas être trouvé.

```Haxe
public function getDraftMails() : Array<MailModel>;
```

Cette méthode retourne la liste des brouillons de l'utilisateur courant (qui peut bien évidemment être vide).

```Haxe
public function createDefaultContext() : Void
public function setActualMail(mail_id : Int) : Void
public function getActualMail() : MailModel
public function canPrint() : Bool
```

Ces quatre méthodes sont utilisées par le module de mail. Utiliser l'une d'entre elles peut créer un comportement non-défini.