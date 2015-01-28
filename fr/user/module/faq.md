Module - FAQ
============

Le module de __foire aux questions__ (FAQ) vous permet de créer et de gérer des FAQs facilement. Si vous souhaitez faire de l'administration ou de l'édition sur des catégories et / ou des FAQs, vous aurez besoin du module de __compte__ fourni par Beluga.

Ce module vous donne accès à un certain nombre de fonctions pour facilement l'intégrer dans votre projet.

### Fonctions

```Haxe
public function redirectEditFAQ() : Bool
public function getCurrentCategory() : CategoryModel
public function createFAQ(args : {
    question : String,
    answer : String,
    category_id : Int
}) : Void
public function createCategory(args : {name : String, parent: Int}) : Void
public function deleteFAQ(args : {question_id : Int, category_id : Int}) : Void
public function deleteCategory(args : {category_id : Int, parent_id: Int}) : Void
public function editCategory(args : {category_id: Int, name : String}) : Void
public function editFAQ(args : {faq_id: Int, question : String, answer : String}) : Void
public function getAllCategories() : Array<CategoryModel>
```

*public function redirectEditFAQ() : Bool*

Cette fonction est utilisée pour vérifier si la FAQ existe déjà. Elle va changer dans une prochaine version.

*public function getCurrentCategory() : CategoryModel*

Cette fonction retourne la catégorie courante ou *null* s'il n'y en a pas.

```Haxe
public function createFAQ(args : {
    question : String,
    answer : String,
    category_id : Int
}) : Void
```

La fonction *createFAQ* prend la question, la réponse et la catégorie dans laquelle elle sera créée en paramètre. Si cette méthode échoue, veuillez vérifier le code d'erreur retourné.

*public function createCategory(args : {name : String, parent: Int}) : Void*

La fonction *createCategory* prend un nom et l'identifiant du parent (ou -1 si le parent est la catégorie root) comme paramètres. Si elle échoue, veuillez vérifier le code d'erreur retourné.

*public function deleteFAQ(args : {question_id : Int, category_id : Int}) : Void*

La fonction *deleteFAQ* prend l'identifiant de la FAQ à supprimer et la catégorie dans laquelle elle se trouve. Elle renvoie le signal `deleteFail` ou le signal `deleteSuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

*public function deleteCategory(args : {category_id : Int, parent_id: Int}) : Void*

La fonction *deleteCategory* prend l'identifiant de la catégorie à supprimer ainsi que l'identifiant de son parent. Si elle échoue, veuillez vérifier le code d'erreur retourné.

*public function editCategory(args : {category_id: Int, name : String}) : Void*

La fonction *editCategory* prend en paramètre l'identifiant de la catégorie que l'on veut éditer ainsi que le nouveau nom que l'on souhaite lui attribuer. Si elle échoue, veuillez vérifier le code d'erreur retourné.

*public function editFAQ(args : {faq_id: Int, question : String, answer : String}) : Void*

La méthode *editFAQ* prend en paramètre l'identifiant de la FAQ à éditer, la nouvelle question et la nouvelle réponse. Elle renvoie le signal `editFail` ou le signal `editSuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

*public function getAllCategories() : Array<CategoryModel>*

La fonction *getAllCategories* renvoie la liste des catégories existantes. Elle peut bien évidemment renvoyer un tableau vide.

### Erreurs

En cas d'échec dans l'exécution d'une méthode, vous n'avez qu'à vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste des erreurs du module de __foire aux questions__ :

 * __UnknownCategory__ : La catégorie n'existe pas.
 * __MissingQuestion__ : Il manque la question.
 * __MissingLogin__ : Vous devez être connecté.
 * __MissingAnswer__ : La réponse est manquante.
 * __MissingName__ : Le nom est manquant.
 * __EntryAlreadyExists__ : Cette FAQ existe déjà.
 * __CategoryAlreadyExists__ : Cette catégorie existe déjà.
 * __IdNotFound__ : La FAQ demandée n'existe pas.
 * __None__ : Aucune erreur détectée.

### A propos des évènements

Ces fonctions lancent toutes des évènements en cas de succès ou d'échec. Ces évènements sont facilement reconnaissables et suivent un même patron : le nom de l'action + un suffixe. Par exemple, les évènements dans le cas de la fonction `deleteCategory` seront *deleteCategory__Fail__* et *deleteCategory__Success__*.
