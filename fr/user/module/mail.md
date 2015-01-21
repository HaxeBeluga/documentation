Module - Mail
=============

Le module d'__e-mail__ vous permet de créer et de gérer des mails facilement. Il dépend du module __compte__ fourni par Beluga.

Ce module fournit un certain nombre de fonctions pour l'intégrer facilement dans votre projet.

### Fonctions

```Haxe
public function createDefaultContext() : Void
public function setActualMail(mail_id : Int) : Void
public function getActualMail() : MailModel
public function canPrint() : Bool
public function getSentMails() : Array<MailModel>
public function getMail(id : Int) : MailModel
public function getDraftMails() : Array<MailModel>
public function sendMail(args : {receiver : String, subject : String, message : String}) : Void
```

*public function sendMail(args : {receiver : String, subject : String, message : String}) : Void*

Cette fonction prend en paramètres l'adresse mail du destinataire, l'objet du mail, ainsi que le message. Elle renvoie le signal `sendSuccess` ou le signal `sendFail`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

*public function getSentMails() : Array<MailModel>;*

Cette fonction retourne la liste des mails envoyés de l'utilisateur courant (qui peut bien évidemment être vide).

*public function getMail(id : Int) : MailModel;*

Cette fonction retourne le mail lié à cet identifiant ou *null* s'il ne peut pas être trouvé.

*public function getDraftMails() : Array<MailModel>;*

Cette fonction retourne la liste des brouillons de l'utilisateur courant (qui peut bien évidemment être vide).

```Haxe
public function createDefaultContext() : Void
public function setActualMail(mail_id : Int) : Void
public function getActualMail() : MailModel
public function canPrint() : Bool
```

Ces quatre fonctions sont utilisées par le module de __mail__. Utiliser l'une d'entre elles peut créer un comportement non-défini.

### Erreurs

En cas d'échec, vous n'avez qu'à vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module d'__e-mail__ :
 * __MissingLogin__ : Vous devez être connecté.
 * __MailNotSent__ : Une erreur s'est produite pendant l'envoi du mail.
 * __OnlyPHP__ : Le seul langage supporté par ce module est le PHP. N'importe quel autre langage échouera et renverra cette erreur.
 * __MissingReceiver__ : Le destinataire est manquant.
 * __MissingSubject__ : L'objet du mail est manquant.
 * __MissingMessage__ : Le message est manquant.
 * __UnknownId__ : L'identifiant reçu n'existe pas dans la base de données.
 * __None__ : Aucune erreur détectée.