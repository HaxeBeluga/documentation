# Gestion d'erreurs

## Des widgets autonomes

Grâce à son système de routage d'url web interne, __Beluga__ est capable de faire fonctionner de manière complètement autonome ces widgets.

Néanmoins, ces widgets peuvent lancer des triggers, afin de notifier les autre modules ou bien le développeur, d'un changement venant d'être effectué au sein du module ou de tout type de comportement dont le développeur pourrait être informé.

## Transmission des erreurs

Lorsqu'une action a lieu au sein d'un module de __Beluga__, très souvent, un trigger est lancé afin de notifier l'utilisateur. Dans certains cas, un même trigger peut être lancé pour différentes raisons. Par exemple, dans le cas du module de __ticket__, la fonction `addlabel` peut lancer le trigger `addlabelFail` dans le cas où l'utilisateur courant n'est pas connecté, ou encore dans le cas où le label existe déjà.

Afin de spécifier l'erreur exacte, une énumeration (TicketErrorKind) est utilisée. Dans le cas présent : `TicketUserNotLogged` et `TicketLabelAlreadyExist`.

Ainsi l'utilisateur pourra, au moment où il reçoit le trigger `addLabelFail`, décider d'un traitement différent en fonction du type d'erreur.

Exemple:

```Haxe
// Cette fonction écoute le trigger 'addLabelFail'
// et sera appelée dans le cas d'une erreur au sein de l'action 'addLabel'
public function catchAddLabelFail(args: { error: TicketErrorKind }) {
	switch (args.error) { // vérification du type d'erreur
		case TicketUserNotLogged: Sys.print("L'utilisateur n'est pas connecté");
		case TicketLabelAlreadyExist(label_name): Sys.print("Le label" + label_name + " existe déjà");
		case _: Sys.print("Une autre erreur inconnue");
	}
}
```

Grâce au système de pattern matching de Haxe, il est possible de déconstruire le variant reçu en erreur et ainsi d'accéder à des informations supplémentaires en fonction des cas.
Dans le cas présent, le nom du label déjà existant est spécifié en paramètre du variant `TicketLabelAlreadyExit`.

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