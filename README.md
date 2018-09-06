# Création et utilisation des web composants pour MOGGLE et game player


## Installer polymer-cli

polymer-cli est un outil en ligne de commande pour simplifier la création de composants Polymer. 

Il vous faudra installer la version 1.0.0 (qui n'est pas la dernière version), pour cela, depuis une Debian 8 ou un Ubuntu Xenial, installer node v8.x

`$ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
$ sudo apt-get install -y nodejs`

Une fois node installé, 
`$ sudo npm install -g polymer-cli@1.0.0 --unsafe-perm'`

## Initialiser le modèle du composant

Créer un dossier nommé comme le futur composant. Pour rappel les composants web doivent avoir un tiret dans leurs noms. 

```
$ mkdir my-component
$ cd my-component
$ polymer init
```

La dernière commande déclenche une série d'interaction vous permettant de nommer le composant, de lui donner une description, etc.

Après quoi le dossier est peuplé par des fichiers constituants le squellete du composant.

## Réaliser l'implémentation

TODO : définir un template à suivre pour les web comp

## Publier le composant

Le composant sera publié sous https://github.com/REVERIES-project

Contacter Pierre-Yves pour les droits d'accès en écriture sur ce projet. 

## Réaliser une page de documentation/démo pour le web composant

Polymer permet d'automatiser ce processus; je recommande d'utiliser le script gp.sh pour éviter les complications. 

Utilisation : une fois le composant sur github, créer un dossier temp. Depuis ce dossier, executer 

`$ sh gp.sh REVERIES-project my-component`





