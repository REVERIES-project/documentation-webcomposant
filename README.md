# Création de web components pour MOGGLE

Cette page décrit le processus à suivre pour l'implémentation de composants réutilisables pour MOGGLE. Toutes les étapes ne sont pas indispensables, il est cependant recommandé de les suivre pour la maintenance du code.

## Configuration initiale 

[Configurer le poste de dev](https://github.com/REVERIES-project/documentation-webcomposant/wiki/Configuration-pour-le-d%C3%A9veloppement)

### Implémentation du composant

L'implémentation est réalisée à partir du template généré par polymer-cli. Commencer par créer un répertoire portant le nom du composant, le nom doit contenir un tiret -, par exemple `my-component` (non indispensable pour Polymer mais la présence du tiret est obligatoire dans la norme W3C).

`$ mkdir my-component`
`$ cd my-component`



Lancer ensuite polymer-cli et choisir l'option *polymer-1-element - A simple Polymer 1.0 element template*

`$ polymer init`

Les options par défaut sont suffisantes, confirmer avec la touche Enter. Un template minimal de composant est généré, le fichier *my-component.html* est ici le plus important, c'est lui que l'on modifiera pour obtenir le comportement, l'apparence et l'interface exposée par le composant.

Le composant peut être testé localement via la commande :

`$ polymer serve`

Executé depuis le répertoire racine *my-component*.

Si le composant requiert des dépendances, ces dernières seront installé via Bower. 

### Publier le composant sur github sous https://github.com/REVERIES-project

Contacter Pierre-Yves pour les droits d'accès en écriture sur ce projet. 

### Tagger le composant avec un numéro de version (nécéssaire pour bower)

Les tags correspondent aux versions successives du composant. Par defaut, Bower utilisera la version correspondant au dernier tag.

`$ git tag -a v0.9.0 -m "0.9.0"`

Publier ensuite le tag sur github :

`$ git push --tags`

Une fois publié, les tags apparaissent dans l'interface github en utilisant le bouton dropdown "Branch : master", la liste des tags publiés apparait à coté de la liste des branches.

Vous pouvez accedez au tag courant (utile lors de mise à jour successive) via 

`$ git tag`


### Réaliser une page de documentation/démo pour le web composant

Polymer permet d'automatiser ce processus; je recommande d'utiliser le script gp.sh pour éviter les complications. 

Ce script est situé dans le repository documentation-webcomposant que vous consultez.

Récupérer le script et le rendre executable:

`$ git clone https://github.com/REVERIES-project/documentation-webcomposant.git`

`$ cd documentation-webcomposant`

`$ sudo chmod u+x gp.sh`


**Utilisation** : une fois le composant sur github, créer un dossier temp. Depuis ce dossier, executer :

`../pathToGp/gp.sh REVERIES-project my-component`

Il vous sera demandé vos identifiants et une page *gh-page* (spécifique à github) sera créée avec la démo du composant.

L'URL de cette page est du type : https://reveries-project.github.io/my-component

## Intégration des composants créés dans MOGGLE et game-player


### Execution de MOGGLE en localhost


Pour cela il est nécéssaire de  : 

* Lancer le démon mongod si ce n'est pas le cas 
 * `$ sudo service mongod start`

* Faire un checkout de la dernière version de MOGGLE 
 * `$ git clone https://github.com/gick/reveries-authoring`

* Installer les dépendances pour la partie serveur 
 * `$ cd reveries-authoring`
 * `$ npm install`

* Installer les dépendances pour la partie client 
 * `$ cd authoring-client`
 * `$ bower install`


* Modifier le fichier bower.json pour référencer le nouveau composant
 * `my-component": "REVERIES-project/my-component`
 * `bower update`

* Si le nouveau composant est une version Bower d'un composant existant
 * Supprimer le fichier *my-component.html* présent sous le répertoire *reveries-authoring/authoring-client/src*. 
 * Dans le répertoire *reveries-authoring/authoring-client/src*, chercher et remplacer les imports html de l'ancienne version par ceux de la version Bower. 
  * Faire une recherche pour *my-component* dans l'ensemble des fichiers *reveries-authoring/authoring-client/src*
  * Pour chaque import de la forme `<link rel="import" href=".../my-component.html">`, remplacer l'import sous la forme `<link rel="import" href="../polymer/polymer.html"><link rel="import" href="../bower-components/my-component/my-component.html">`
* Tester la nouvelle version
 * `pm2 start ecosystem.config.js`

* Si tout fonctionne bien, supprimer le fichier de l'ancien composant et réaliser une pull request avec la nouvelle version



