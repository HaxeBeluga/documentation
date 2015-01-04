#ORM - Spod Macro

Pour sa couche persistence Beluga utilise l'ORM spod macro qui est la librairie la plus standard pour utilisé les bases de données. Il est donc fortement conseillé de connaitre [spod macro](http://old.haxe.org/manual/spod) avant de lire cette documentation.

La base de donnée est représenté par la classe *Database*, elle fait partie des attributs de *Beluga* et est instancié au même moment que *Beluga*. 

Beluga.hx:81
```haxe
db = new Database(cnx);
```

##Enregistrer un model
Chaque module souhaitant enregistrer des objets en persistence doit avoir sa classe model portant le build *@:build(beluga.Database.registerModel())* en plus d'hériter de Object de spod macro.

Exemple avec l'objet *User*
```haxe
@:build(beluga.Database.registerModel())
class User extends Object {
```

Tout les models sont donc repertoriés dans la classe Database, Beluga est donc au courant de l'ensemble des models éxistant a l'éxécution.

Database.hx:23
```haxe
private static var moduleClassTypeList : Array<ClassType> = new Array<ClassType>();
```

##Génération des tables
Lors de l'instanciation, Beluga se connecte a la base de donnée avec les informations de beluga.xml et automatiquement va vérifier si les tables pour chacun des models éxistent, si non il les créé.

La fonction éxécutant cet tache est *Database.initRegisteredModelTable()* et éxécuté a l'instanciation de Database et donc de Beluga.
