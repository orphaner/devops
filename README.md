# Démarrage des VM's
Nous avons créé un Vagrantfile qui permet de lancer 5 VM.
Démarrer les VM's à l'aide de la commande ```vagrant up```.


# Installation consul
Afin de provisionner automatiquement nos machines, nous allons utiliser l'outil Ansible.

## Configuration de l'inventaire ansible
Grâce au provisionneur ansible de vagrant, l'inventaire est généré : ```.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory```
Nous allons néanmoins le modifier pour utiliser l'IP du réseau privée plutôt que l'IP nattée.

Remplir l'inventaire de dév et vérifier la connectivité à l'aide de la commande ```ansible -i inventories/dev all -m ping```


## Serveur consul
On va commencer par installer 3 instances de consul en mode serveur avec les caractéristiques suivantes :
* ui activée 
* le retry-join sera activé et on s'assurera de se prémunir contre le split-brain

Indications :
* Compléter le fragment de playbook ```consul.yml``` afin d'utiliser le rôle consul. Les variables en place sont correctes.
* Le rôle contient quelques erreurs d'exécution qu'il conviendra d'analyser et de corriger. 

Questions :
* à l'aide de la commande ```consul members``` vérifier que les 3 noeuds serveurs communiquement bien
* vérifier sur 1 serveur les ports ouverts par consul ainsi que les binds avec la commande ```netstat```
* recommencer mais à distance en utilisant la commande ```ansible``` et le module ```command```
* vérifier le bon fonctionnement de l'API REST via un curl (en local ou à distance ?)
* vérifier dans un navigateur que l'ui est fonctionnelle
* plutôt que de télécharger l'archive de consul dans le playbook, quelle solution plus pérenne proposer ?

## Agents locaux
Nous allons ensuite installer 2 instances de consul en mode client :
* le client rejoindra directement le cluster au démarrage
* le bind de l'API REST sera effectué sur l'IP 127.0.0.1


# Déploiement d'une application spring boot
Nous allons maintenant déployer une application java développée en spring boot. 
Celle-ci démarre sur le port 8080 et s'enregistre automatiquement sur le consul d'IP 127.0.0.1
