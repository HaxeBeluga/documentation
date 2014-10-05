# Gestion d'erreurs

## Des widgets autonomes

Grace a son système de routage d'url web interne, __beluga__ est capable de faire fonctionner de manière complètement autonome ces widgets.

Néanmoins, ces widgets peuvent lancer des triggers afin de notifier les autre modules, ou encore le développeur d'une action venant d'être effectue, d'un changement au sein du module, ou de tout type de comportement dont le développeur pourrait être informé.

## Transmission des erreurs

Lorsqu'une action au sein d'un module de __beluga__, très souvent un trigger est lancé afin de notifier l'utilisateur. Dans certains car, un meme trigger peut être lancé pour différentes raison. Par example dans le cas du module de __ticket__, la fonction `addlabel`, peut lancer le trigger `addlabelFail`, dans le cas ou l'utilisateur courant n'est pas connecté, ou encore dans le cas ou le message le label existe deja. 

Afin de specifier l'erreur exacte, une enumeration (TicketErrorKind) est utilisé afin de specifier l'erreur exacte qui s'est produite. Dans le cas present `TicketUserNotLogged` et `TicketLabelAlreadyExist`.

Ainsi l'utilisateur pourra, au moment ou il reçoit le trigger addLabelFail, decider d'un traitement different en fonction du type d'erreur.

Example:

```Haxe
// Cette fonction écoute le trigger 'addLabelFail'
// et sera appelé dans le cas d'une erreur au sein de l'action 'addLabel'
public function catchAddLabelFail(args: { error: TicketErrorKind }) {
	switch (args.error) { // verification du type d'erreur
		case TicketUserNotLogged: Sys.print("L'utilisateur n'est pas connecté");
		case TicketLabelAlreadyExist(label_name): Sys.print("Le label" + label_name + " existe deja");
		case _: Sys.print("Une autre erreur inconnue");
	}
}
```

Grace au system de pattern matching de Haxe, il est possible de déconstruire, le variant reçu en erreur, et ainsi d'accéder a des information supplémentaire en fonction des cas, dans le cas present, le nom de du label deja existant est spécifié en paramètre du variant `TicketLabelAlreadyExit`.

## Convention sur les enumerations d'erreurs

Par convention les nom des enumerations sont constitué du nom du module, suivis du suffix `ErrorKind`, dans le cas du module de __ticket__ cela produit *Ticket__ErrorKind__*. Les noms de variants sont constitués du nom du module, ceci afin d'éviter des conflits dans le cas d'erreur similaires dans deux modules, suivi de l'erreur, par example *Ticket__UserNotLogged__*.

Les modules _devraient_ aussi fournir une méthod permettant de transformer ce code en une erreur lisible par un humain. Par exemple:
```haxe
    private function getErrorString(error: ModuleErrorKind): String {
        return switch (error) {
            case ErrorTrigger1: BelugaI18n.getKey(i18n, "erreur1");
    }
```