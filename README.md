# Création et utilisation des web composants pour MOGGLE et game player

## Configuration initiale 

[Configurer le poste de dev](https://github.com/REVERIES-project/documentation-webcomposant/wiki/Configuration-pour-le-d%C3%A9veloppement)

### Réaliser l'implémentation

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

### Installation de l'environnement de dev
L'objectif de la création de composant packager par Bower est d'employer ces composants en production. 

Pour faire fonctionner MOGGLE il est nécéssaire de disposer d'une version 3.6.X de MongoDB

Pour ubuntu et ses variantes (mint...), il est nécessaire la clée GPG qui garantie l'authenticité du package:

`$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5`

Ajoutez ensuite le package mongoDB multiverse ubuntu à la liste des sources : 

`$ echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" \`
`| sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list`

Recharger la liste des paquets

`$ sudo apt update`

Enfin, installer mongodb :

`$ sudo apt-get install -y mongodb-org`

Pour tester l'installation de mongodb, lancer le démon 
`sudo service mongod start`
Puis lancer la ligne de commande mongo
`mongo`

Vous aurez aussi besoin du gestionnaire de processus PM2, l'installation est plus simple
`npm install pm2@latest -g`

Tester avec la commande `pm2`

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
 * `nouveau-composant": "REVERIES-project/nouveau-composant`
 * `bower update`

* Au sein du code, remplacer les références à nouveau-composant par des références à la version bower de ce composant

* Tester la nouvelle version
 * `pm2 start ecosystem.config.js`

* Si tout fonctionne bien, supprimer le fichier de l'ancien composant et réaliser une pull request avec la nouvelle version



