Module - FAQ
============

Le module de __foire aux questions__ vous permet de créer et de gérer des faqs facilement. Si vous souhaitez faire de l'administration ou de l'édition sur des catégories et / ou des faqs, vous aurez besoin du module de __compte__ fourni par Beluga.

Ce module vous donne accès à un certain nombre de méthodes pour facilement l'intégrer dans votre projet.

Voici les méthodes fournies par ce module :

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

##Signaux

Ce module peut renvoyer les signaux suivants :

 * defaultPage
 * deleteFail
 * deleteSuccess
 * createFail
 * createSuccess
 * editFail
 * editSuccess
 * createCategoryFail
 * createCategorySuccess
 * deleteCategoryFail
 * deleteCategorySuccess
 * editCategoryFail
 * editCategorySuccess
 * redirectCreateFAQ
 * redirectCreateCategory
 * print
 * redirectEditCategory
 * redirectEditFAQ
 * edit
 * create
 * delete

##Erreurs

En cas d'échec dans l'exécution d'une méthode, vous n'avez qu'à vérifier le code d'erreur retourné pour savoir ce qui n'a pas fonctionné. Voici la liste des erreurs du module de __foire aux questions__ :

 * __UnknownCategory__ : La catégorie n'existe pas.
 * __MissingQuestion__ : Il manque la question.
 * __MissingLogin__ : Vous devez être connecté.
 * __MissingAnswer__ : La réponse est manquante.
 * __MissingName__ : Le nom est manquant.
 * __EntryAlreadyExists__ : Cette faq existe déjà.
 * __CategoryAlreadyExists__ : Cette catégorie existe déjà.
 * __IdNotFound__ : La faq demandée n'existe pas.
 * __None__ : Aucune erreur détectée.

##Description des méthodes

Par exemple, la méthode *createFaq* renvoie le signal `createSuccess` ou le signal `createFail`. Ensuite, vous n'avez qu'à effectuer l'action souhaitée en fonction du résultat obtenu.

```Haxe
public function redirectEditFAQ() : Bool
```

Cette méthode est utilisée pour vérifier si la faq existe déjà. Cette méthode va changer dans une prochaine version.

```Haxe
public function getCurrentCategory() : CategoryModel
```

Cette méthode retourne la catégorie courante ou *null* s'il n'y en a pas.

```Haxe
public function createFAQ(args : {
    question : String,
    answer : String,
    category_id : Int
}) : Void
```

La méthode *createFAQ* prend la question, la réponse et la catégorie dans laquelle elle sera créée en paramètre. Elle renvoie le signal `createSucess` ou le signal `createFail`. Si cette méthode échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function createCategory(args : {name : String, parent: Int}) : Void
```

La méthode *createCategory* prend un nom et l'identifiant du parent (ou -1 si le parent est la catégorie root) comme paramètres. Elle renvoie le signal `createCategoryFail` ou le signal `createCategorySuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function deleteFAQ(args : {question_id : Int, category_id : Int}) : Void
```

La méthode *deleteFAQ* prend l'identifiant de la FAQ à supprimer et la catégorie dans laquelle elle se trouve. Elle renvoie le signal `deleteFail` ou le signal `deleteSuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function deleteCategory(args : {category_id : Int, parent_id: Int}) : Void
```

La méthode *deleteCategory* prend l'identifiant de la catégorie à supprimer ainsi que l'identifiant de son parent. Elle renvoie le signal `deleteCategoryFail` ou le signal `deleteCategorySuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function editCategory(args : {category_id: Int, name : String}) : Void
```

La méthode *editCategory* prend en paramètre l'identifiant de la catégorie que l'on veut éditer ainsi que le nouveau nom que l'on souhaite lui attribuer. Elle renvoie le signal `editCategoryFail` ou le signal `editCategorySuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function editFAQ(args : {faq_id: Int, question : String, answer : String}) : Void
```

La méthode *editFAQ* prend en paramètre l'identifiant de la FAQ à éditer, la nouvelle question et la nouvelle réponse. Elle renvoie le signal `editFail` ou le signal `editSuccess`. Si elle échoue, veuillez vérifier le code d'erreur retourné.

```Haxe
public function getAllCategories() : Array<CategoryModel>
```

La méthode *getAllCategories* renvoie la liste des catégories existantes. Elle peut bien évidemment renvoyer un tableau vide.