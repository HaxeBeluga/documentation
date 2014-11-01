Module - Survey
===============

Le module de __sondage__ vous permet de créer et de gérer des sondages facilement. Il dépend du module de __compte__ fourni par Beluga.

Ce module fournit un certain nombre de méthodes pour l'intégrer facilement dans votre projet.

Voici la liste des méthodes fournies par ce module :

```Haxe
public function canVote(survey_id : Int) : Bool
public function create(args : {
    title : String,
    description : String,
    choices : Array<String>
}) : Void
public function vote(args : {
    survey_id : Int,
    option : Int
}) : Void
public function getSurvey(survey_id: Int) : SurveyModel
public function getSurveysList() : Array<SurveyData>
public function redirect() : Void
public function delete(survey_id : Int) : Void
public function getChoices(survey_id : Int) : Array<Choice>
public function getResults(survey_id : Int) : Array<Dynamic>
public function print(survey_id : Int): Void
public function getActualSurveyId() : Int
```

##Signaux

Ce module peut renvoyer les signaux suivants :

 * redirect
 * deleteFail
 * deleteSuccess
 * printSurvey
 * createFail
 * createSuccess
 * voteFail
 * voteSuccess
 * answerNotify
 * defaultSurvey

##Erreurs

En cas d'échec, veuillez vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module survey :

 * __MissingLogin__ : Vous devez être connecté.
 * __NotAllowed__ : Vous ne pouvez pas faire cette action.
 * __MissingDescription__ : Il manque la description.
 * __MissingTitle__ : Il manque le titre.
 * __MissingChoices__ : Deux choix au minimum sont requis.
 * __NotFound__ : Le sondage demandé n'existe pas.
 * __AlreadyVoted__ : Vous avez déjà voté pour ce sondage.
 * __None__ : Aucune erreur détectée.

##Description des méthodes

Par exemple, la méthode `vote` renverra le signal `voteSuccess` ou `voteFail`. Ensuite, il vous suffit d'effectuer l'action que vous souhaitez selon le résultat retourné. N'oubliez pas de vérifier le code d'erreur pour savoir ce qui n'a pas fonctionné en cas d'échec.

```Haxe
public function canVote(survey_id : Int) : Bool
```

La méthode `canVote` retourne false s'il n'y a pas d'utilisateur courant connecté ou si l'utilisateur courant a déjà voté pour le sondage référencé par l'identifiant passé en paramètre.

```Haxe
public function create(args : {
    title : String,
    description : String,
    choices : Array<String>
}) : Void
```

Cette méthode crée un nouveau sondage. Elle prend en paramètre un titre, une description et les choix. Elle renvoie le signal `createFail` ou `createSuccess`.

```Haxe
public function vote(args : {
	survey_id : Int,
	option : Int
}) : Void
```

La méthode `vote` prend en paramètre l'identifiant du sondage et celui du choix sélectionné. Elle renvoie le signal `voteSuccess` ou `voteFail`.

```Haxe
public function getSurvey(survey_id: Int) : SurveyModel
```

Cette méthode renvoie le sondage correspondant à l'identifiant passé en paramètre. Elle retourne *null* si le sondage n'a pas été trouvé.

```Haxe
public function getSurveysList() : Array<SurveyData>
```

Cette méthode retourne tous les sondages créés par l'utilisateur courant.

```Haxe
public function redirect() : Void
```

Cette méthode renvoie le signal `redirect`.

```Haxe
public function delete(args : {survey_id : Int}) : Void
```

La méthode `delete` supprime le sondage référencé par l'identifiant passé en paramètre. Elle renvoie le signal `deleteFail` ou `deleteSuccess`.

```Haxe
public function getChoices(args : {survey_id : Int}) : Array<Choice>
```

Cette méthode retourne la liste des choix du sondage référencé par l'identifiant passé en paramètre. Si la liste retournée est vide, vous devriez vérifier si le sondage existe.

```Haxe
public function getResults(args : {survey_id : Int}) : Array<Dynamic>
```

Cette méthode retourne un tableau contenant les statistiques du sondage référencé par l'identifiant passé en paramètre.

```Haxe
public function print(survey_id : Int): Void
public function getActualSurveyId() : Int
```

Ces deux méthodes sont appelées seulement en interne par le module __survey__.