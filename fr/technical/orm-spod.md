#ORM - Spod Macro

Pour sa couche persistence, Beluga utilise l'ORM spod macro qui est la bibliothèque la plus utilisé pour les bases de données. Il est donc fortement conseillé de connaître [spod macro](http://old.haxe.org/manual/spod) avant de lire cette documentation.

La base de données est représentée par la classe *Database*. Elle fait partie des attributs de *Beluga* et est instanciée au même moment que *Beluga*. 

Beluga.hx:81
```haxe
db = new Database(cnx);
```

##Enregistrer un modèle
Chaque module souhaitant enregistrer des objets en persistence doit avoir sa classe modèle portant le la macro `build` *@:build(beluga.Database.registerModel())* en plus d'hériter de la classe Object de spod macro.

Exemple avec l'objet *User*:
```haxe
@:build(beluga.Database.registerModel())
class User extends Object {
```

Tous les modèles sont répertoriés dans la classe Database. Par conséquent, Beluga est donc au courant de l'ensemble des modèles existant à l'exécution.

Database.hx:23
```haxe
private static var moduleClassTypeList : Array<ClassType> = new Array<ClassType>();
```

##Génération des tables
Lors de l'instanciation, Beluga se connecte à la base de données, soit avec les informations dans beluga.xml si présentent, sinon grâce à une connection fournie. Et va automatiquement vérifier si les tables pour chacun des modèles existent. Si ce n'est pas le cas, il les crée.

La fonction *Database.initRegisteredModelTable()* qui est responsable de cela est exécutée à l'instanciation de Database, et donc de Beluga.
