# Repertoires de données

## Présentation

Afin d'abstraire un maximum la __couche__ données au sein des modules de __Beluga__ une classe répertoire
est crée pour chaque modèle de donnée.

Cette classe va permettre au déveleppeur d'abstraire le type de base de données utilisé en amont ( e.g SQL, SQLlite, fichier texte, etc),
ainsi que de supprimer toute logique liée à la base de données du code métier. Il est ainsi plus aisé de maintenir le code métier et de le tester
sans problematiques liées à la gestions des données.

### Interface Repository

Afin d'aider à la creation des répertoires, __Beluga__ met à la disposition des développeur une interface 
proposant les méthodes de base pour la création d'un répertoire: [interface Repository](https://github.com/HaxeBeluga/beluga/blob/master/core_src/beluga/module/Repository.hx).
Cette interface dispose de trois méthodes primordiale pour la gestions des modèles:

* `save` - Afin de sauvegarder un modèle
* `delete` - Pour supprimer un modèle
* `update` - Dans le but de mettre à jour un modèle exitant dèja dans la base de donnée.

### Classe SpodRepository

Dans le but de faciliter plus encore le travail du développeur, __Beluga__ propose une implémentation de cette interface
utilisant __SPOD Macro__: [SpodRepository](https://github.com/HaxeBeluga/beluga/blob/master/core_src/beluga/module/SpodRepository.hx).

Ainsi si il le souhaite le développeur peut utiliser cette classe pour abstraire l'utilisation de __SPOD Macro__
au sein de son code, créer une nouvelle classe de répertoire pour son modèle n'utilisant pas __SPOD__, ou encore surcharger 
la classe `SpodRepository` afin de lui apporter de nouvelles methodes si nécessaire.

Les modules de __Beluga__ par exemple vont utiliser la troisième méthode.

### Exemple du module Wallet

Si l'on prend l'exemple du module `Wallet`, celui ci dispose d'une classe `WalletRepository` permettant 
de réaliser les actions base de données du porte-feuille [WalletRepository](https://github.com/HaxeBeluga/beluga/blob/master/module_src/beluga/module/wallet/repository/WalletRepository.hx).

Celle ci surcharge la classe `SpodRepository`, ce qui lui donne donc accès aux méthodes `save`, `delete`, `update` utilisant 
__SPOD Macro__, et implémente aussi d'autre fonctionnalités tel que la méthode `getUserWallet` qui permet d'obtenir 
le porte-feuille d'un utilisateur.

