Module - Sondage
================

Le module de __sondage__ vous permet de créer et de gérer des sondages facilement. Il dépend du module de __compte__ fourni par Beluga.

Ce module fournit un certain nombre de fonctions pour l'intégrer facilement dans votre projet.

### Fonctions

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

*public function canVote(survey_id : Int) : Bool*

La fonction `canVote` retourne *false* s'il n'y a pas d'utilisateur courant connecté ou si l'utilisateur courant a déjà voté pour le sondage référencé par l'identifiant passé en paramètre.

```Haxe
public function create(args : {
    title : String,
    description : String,
    choices : Array<String>
}) : Void
```

Cette fonction crée un nouveau sondage. Elle prend en paramètre un titre, une description et les choix.

```Haxe
public function vote(args : {
	survey_id : Int,
	option : Int
}) : Void
```

La fonction `vote` prend en paramètre l'identifiant du sondage et celui du choix sélectionné.

*public function getSurvey(survey_id: Int) : SurveyModel*

Cette fonction renvoie le sondage correspondant à l'identifiant passé en paramètre. Elle retourne *null* si le sondage n'a pas été trouvé.

*public function getSurveysList() : Array<SurveyData>*

Cette fonction retourne tous les sondages créés par l'utilisateur courant.

*public function redirect() : Void*

Cette fonction renvoie le signal `redirect`.

*public function delete(args : {survey_id : Int}) : Void*

La fonction `delete` supprime le sondage référencé par l'identifiant passé en paramètre.

*public function getChoices(args : {survey_id : Int}) : Array<Choice>*

Cette fonction retourne la liste des choix du sondage référencé par l'identifiant passé en paramètre. Si la liste retournée est vide, vous devriez vérifier si le sondage existe.

*public function getResults(args : {survey_id : Int}) : Array<Dynamic>*

Cette fonction retourne un tableau contenant les statistiques du sondage référencé par l'identifiant passé en paramètre.

*public function print(survey_id : Int): Void*

*public function getActualSurveyId() : Int*

Ces deux fonctions sont appelées seulement en interne par le module de __sondage__.

### Erreurs

En cas d'échec, veuillez vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste complète des erreurs du module de __sondage__ :

 * __MissingLogin__ : Vous devez être connecté.
 * __NotAllowed__ : Vous ne pouvez pas faire cette action.
 * __MissingDescription__ : Il manque la description.
 * __MissingTitle__ : Il manque le titre.
 * __MissingChoices__ : Deux choix au minimum sont requis.
 * __NotFound__ : Le sondage demandé n'existe pas.
 * __AlreadyVoted__ : Vous avez déjà voté pour ce sondage.
 * __None__ : Aucune erreur détectée.

### A propos des évènements

Ces fonctions lancent toutes des évènements en cas de succès ou d'échec. Ces évènements sont facilement reconnaissables et suivent un même patron : le nom de l'action + un suffixe. Par exemple, les évènements dans le cas de la fonction `delete` seront *delete__Fail__* et *delete__Success__*.