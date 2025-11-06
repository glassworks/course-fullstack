# Docker

Dans cette section, nous allons déployer une base de données MariaDB sur notre serveur à l'aide de Docker. Nous verrons ensuite comment la sécuriser.

Vous constaterez que la configuration Docker que nous avons mise en place sur notre serveur ressemble finalement à celle que nous utilisons en développement. C'est une bonne chose, car plus notre environnement de développement est proche de notre environnement de production, plus il est facile de corriger les bogues.

## Installer Docker sur votre Serveur

Nous faisons un déploiement de MariaDB avec Docker. Jusqu'au présent, nous avons installé Docker sur un PC type Desktop, en utilisant Docker Desktop. 

Pour installer docker sur une instance Linux, il y aura quelques démarches à faire. Vous pouvez consulter la documentation officielle ici : [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

Par exemple, sur Ubuntu, les étapes sont les suivantes (attention, à faire avec **sudo** ou en tant que **root**) :


```bash
# Désinstaller les anciennes versions de docker
sudo apt-get remove docker docker-engine docker.io containerd runc

# Mettre à jour les indexes des packages
sudo apt-get update

# Installer les packages tiers nécessaires pour ajouter Docker parmi nos indexes
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
# Télécharger la clé publique de Docker qui va vérifier l'authenticité
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Installer le dépot Docker parmi les sources connues de notre distribution
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.gpg
    
# Remettre à jour nos indexes
sudo apt-get update

# Installer Docker 
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Une fois installé, vous pouvez vérifier que le processus fonctionne correctement avec :

```bash
systemctl status docker
```

## Accorder accès au groupe Docker

Certains de vos utilisateurs Linux auront le droit à contrôler les processus Docker, sans passer par `sudo`.

Pour leur donner ce droit, ajoutez les utilisateurs concernés au groupe `docker` :


```bash
usermod -aG docker [nom d'utilisateur]
```

{% hint style="warning" %}
Attention !

Seulement les utilisateurs privilégiés devront posséder ce droit.
{% endhint %}


## Créer un utilisateur dédié à votre application

Il est courant de créer un utilisateur spécial dédié à votre application. Cet utilisateur n'aura pas de droits sudo, mais pourra, par exemple, contrôler Docker.

Veuillez créer un nouvel utilisateur `myinvoice`.

Veuillez configurer le compte `myinvoice` de manière à ce que tous vos collègues puissent se connecter en tant qu'utilisateur `myinvoice`.

L'utilisateur `myinvoice` devrait être autorisé à contrôler Docker, mais pas à installer ou supprimer des paquets du système d'exploitation.

{% hint style="info" %}

Pourquoi procédons-nous ainsi ?

Afin de limiter la portée de toute attaque pouvant provenir de notre API. Si un pirate informatique identifie une faille dans le moteur NodeJS et parvient à l'exploiter, l'étendue des dommages sera limitée aux droits d'accès de l'utilisateur sous lequel le processus API s'exécute.

Il est donc très risqué d'exécuter votre API sous l'utilisateur root. Il est préférable de créer un utilisateur à portée limitée, verrouillé dans son propre répertoire « home » et incapable d'effectuer des tâches d'administration sur le serveur.

{% endhint %}




MySQL (et MariaDB) contient par défaut un script qui permet d’affecter des règles de sécurité de base

* Désactiver les connexions anonymes
* Assurer des utilisateurs admin/root ne peuvent connexion uniquement par la machine locale
* Assurer que l’utilisateur `root` a un mot de passe (et qu’il est suffisamment sécurisé)
* Supprimer la base de données de test (parfois installé par défaut)

```sh
docker exec -it [Container ID] mysql_secure_installation
```