Gestion d'erreurs
=================

## Des widgets autonomes

Grâce à son système de routage d'url web interne, __Beluga__ est capable de faire fonctionner de manière complètement autonome ces widgets.

Néanmoins, ces widgets peuvent lancer des évènements afin de notifier les autre modules, ou encore le développeur d'une action venant d'être effectue, d'un changement au sein du module, ou de tout type de comportement dont le développeur pourrait être informé.

## Transmission des erreurs

Lorsqu'une action au sein d'un module de __beluga__, très souvent un évènement est lancé afin de notifier l'utilisateur. Dans certains car, un meme évènement peut être lancé pour différentes raison. Par example dans le cas du module de __ticket__, la fonction `addlabel`, peut lancer l'évènement `addlabelFail`, dans le cas ou l'utilisateur courant n'est pas connecté, ou encore dans le cas ou le message l'étiquette existe deja. 

Afin de spécifier l'erreur exacte, une énumeration (TicketErrorKind) est utilisée. Dans le cas présent : `TicketUserNotLogged` et `TicketLabelAlreadyExist`.

Ainsi l'utilisateur pourra, au moment ou il reçoit l'évènement addLabelFail, decider d'un traitement different en fonction du type d'erreur.

Exemple:

```Haxe
// Cette fonction écoute l'évènement 'addLabelFail'
// et sera appelé dans le cas d'une erreur au sein de l'action 'addLabel'
public function catchAddLabelFail(args: { error: TicketErrorKind }) {
	switch (args.error) { // vérification du type d'erreur
		case TicketUserNotLogged: Sys.print("L'utilisateur n'est pas connecté");
		case TicketLabelAlreadyExist(label_name): Sys.print("Le label" + label_name + " existe déjà");
		case _: Sys.print("Une autre erreur inconnue");
	}
}
```

Grace au system de filtrage par motif de Haxe, il est possible de déconstruire, le variant reçu en erreur, et ainsi d'accéder a des information supplémentaire en fonction des cas, dans le cas present, le nom de d'étiquette deja existant est spécifié en paramètre du variant `TicketLabelAlreadyExit`.

## Convention sur les énumerations d'erreurs

Par convention, les noms des énumerations sont constitués du nom du module, suivis du suffixe `ErrorKind`. Dans le cas du module de __ticket__, cela produit *Ticket__ErrorKind__*.
Les noms de variants sont constitués du nom du module afin d'éviter des conflits dans le cas d'erreurs similaires dans plusieurs modules, suivi de l'erreur. Par exemple : *Ticket__UserNotLogged__*.

Les modules _devraient_ aussi fournir une méthode permettant de transformer ce code en une erreur lisible par un humain. Par exemple :
```haxe
    private function getErrorString(error: ModuleErrorKind): String {
        return switch (error) {
            case ErrorTrigger1: BelugaI18n.getKey(i18n, "erreur1");
    }
```