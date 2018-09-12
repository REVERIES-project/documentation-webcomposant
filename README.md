# Création et utilisation des web composants pour MOGGLE et game player

## Création des composants
### Installer polymer-cli

polymer-cli est un outil en ligne de commande pour simplifier la création de composants Polymer. 

Il vous faudra installer la version 1.0.0 (qui n'est pas la dernière version), pour cela 
'npm install -g polymer-cli#1.0.0'

### Initialiser le modèle du composant

Créer un dossier nommé comme le futur composant. Pour rappel les composants web doivent avoir un tiret dans leurs noms. 

`$ mkdir my-component`
`$ cd my-component`
`$ polymer init`

La dernière commande déclenche une série d'interaction vous permettant de nommer le composant, de lui donner une description, etc.

Après quoi le dossier est peuplé par des fichiers constituants le squellete du composant.

### Réaliser l'implémentation

### Publier le composant sur github sous https://github.com/REVERIES-project

Contacter Pierre-Yves pour les droits d'accès en écriture sur ce projet. 

### Tagger le composant avec un numéro de version (nécéssaire pour bower)

Les tags correspondent aux versions successives du composant. Par defaut, Bower utilisera la version correspondant au dernier tag.

`$ git tag -a v0.9.0 -m "0.9.0"`

### Réaliser une page de documentation/démo pour le web composant

Polymer permet d'automatiser ce processus; je recommande d'utiliser le script gp.sh pour éviter les complications. 

Utilisation : une fois le composant sur github, créer un dossier temp. Depuis ce dossier, executer 
`sh gp.sh REVERIES-project my-component`

## Intégration des composants créés dans MOGGLE et game-player



L'objectif de la création de composant packager par Bower est d'employer ces composants en production. 

Pour faire fonctionner MOGGLE il est nécéssaire de disposer d'une version 3.6.X de MongoDB
`$ echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.6 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list`

`$ sudo apt update`

`$ sudo apt-get install -y mongodb-org`

Pour tester l'installation de mongodb, lancer le démon 
`sudo service mongod start`
Puis lancer la ligne de commande mongo
`mongo`

Vous aurez aussi besoin du gestionnaire de processus PM2, l'installation est plus simple
`npm install pm2@latest -g`
Tester avec la commande `pm2`



Pour cela il est nécéssaire de  : 
* Faire un checkout de la dernière version de MOGGLE 
 * `git clone https://github.com/gick/reveries-authoring`

* Installer les dépendances pour la partie serveur 
 * `cd reveries-authoring`
 * `npm install`

* Modifier le fichier bower.json pour référencer le nouveau composant
 * `nouveau-composant": "REVERIES-project/nouveau-composant`
 * `bower install`

* Au sein du code, remplacer les références à nouveau-composant par des références à la version bower de ce composant

* Tester la nouvelle version
 * `pm2 start ecosystem.config.js`

* Si tout fonctionne bien, supprimer le fichier de l'ancien composant et réaliser une pull request avec la nouvelle version



