# Connexion SSH

Nous commençons en créant une connexion sécurisée à un serveur distant à l'aide de **S**ecure **SH**ell (SSH).

Ce type de tunnel crypté est une norme industrielle et utilise un cryptage asymétrique.

Vous aurez donc besoin d'une paire de clés pour établir une connexion :

L'utilisateur qui veut se connecter :

* garde sa **clé privée** pour lui
* envoie sa **clé publique** au serveur auquel il veut accéder

L'administrateur du serveur :

* vérifie s'il souhaite accorder l'accès à l'utilisateur
* si oui, il installe la clé publique de l'utilisateur au bon endroit sur le serveur

Lorsque l'utilisateur tente de se connecter, il crypte un message à l'aide de sa clé privée. Si le serveur parvient à décrypter le message avec la clé publique correspondante, l'utilisateur est identifié, puisqu'il est le seul à posséder la clé privée.

## Générez votre propre paire de clés


Sur votre machine locale, nous allons effectuer la commande `ssh-keygen` (dans le Terminal sur Mac, ou PowerShell sur Windows) :

```bash
hetic@eabaf4e7983c:~$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/hetic/.ssh/id_ed25519): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/hetic/.ssh/id_ed25519
Your public key has been saved in /home/hetic/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:dkOqsde5rj1aZjlfZQNiYPjnX+Pg2gJez+Qmz5SfeRE hetic@eabaf4e7983c
The keys randomart image is:
+---[RSA 3072]----+
|        .o       |
|       .. .      |
|        . .o .   |
|         +... .E |
|      . S =    .+|
|       = + * o.*.|
|      o o @ Bo= o|
|       . *.*+O..+|
|        o++oB+ +.|
+----[SHA256]-----+
hetic@eabaf4e7983c:~$ ls ~/.ssh
id_ed25519  id_ed25519.pub  known_hosts
```

Ne mettez pas de mot de passe quand il vous le demande.

On voit que _sur notre machine locale_, nous avons maintenant une paire de clés dans le dossier précisé pendant `ssh-keygen` :

* `id_ed25519` : la clé privée, à protéger précieusement, et à ne jamais partager
* `id_ed25519.pub` : la clé publique, qu'on partage à l'administrateur du serveur distante

## Premier accès à votre serveur

Seul l'administrateur (une personne disposant des privilèges `root`) peut accorder l'accès `root` à un autre utilisateur.

{% hint style="success" %}

Je créerai un VPS par groupe. Par défaut, je suis l'administrateur root, mais je vous donnerai également un accès `root`.

Un membre de chaque groupe devra me fournir sa clé publique afin que je puisse configurer le VPS. Je vous communiquerai l'adresse IP du VPS.

{% endhint %}


Once the administrator has given you access and the IP address of the server, you can connect to this server :

```bash
ssh -i /chemin/vers/votre/clé/privée root@55.55.55.55
```

Il faut bien sur remplacer `/chemin/vers/votre/clé/privée` par le vrai chemin vers votre clé privée sur votre machine, et remplacer `55.55.55.55` par la vraie adresse IP de votre VPS.

## Accorder accès aux autres

Comment ai-je pu vous accorder l'accès root ?

Sur Linux, il existe un utilisateur appelé `root` qui dispose d'un répertoire « home » situé dans `/root` (il s'agit d'un répertoire spécial réservé à l'utilisateur `root`).

Pour accorder à quelqu'un l'accès en tant que `root`, je dois ajouter la clé publique de cette personne au fichier `/root/.ssh/authorized_keys`. Cette personne pourra alors également se connecter en tant que `root`.

Ceci est valable pour n'importe quel utilisateur du système. Un utilisateur nommé `kevin` aura un répertoire « home » sous `/home/kevin` (les utilisateurs normaux ont leur répertoire home sous le répertoire `/home`). Si Kevin souhaite donner l'accès à Jane, il collera la clé publique de Jane dans le fichier `/home/kevin/.ssh/authorized_keys`.

Jane pourra alors se connecter en tant que Kevin :

```bash
ssh -i /chemin/vers/la/clé/privée/de/Jane kevin@55.55.55.55
```

{% hint style="success" %}

La personne qui dispose déjà d'un accès au serveur peut ainsi accorder un accès root à tout le monde en copiant leurs clés publiques dans `/root/.ssh/authorized_keys.`. Veuillez essayer !

{% endhint %}


Comment révoquer l'accès ? Il suffit de supprimer la clé publique de cette personne de `authorized_keys`.


{% hint style="info" %}

Vous n'avez jamais utilisé le terminal Linux auparavant ? Il s'agit d'une compétence essentielle en informatique et en DevOps. Je vous encourage à l'apprendre et à vous exercer pendant ce cours.
À noter :

- [Navigation dans le système de fichiers](https://docs.glassworks.tech/unix-shell/fichiers-et-repertoires/030-fichiers/navigation)
- [Modification de fichiers](https://docs.glassworks.tech/unix-shell/fichiers-et-repertoires/030-fichiers/edition#nano-ou-pico)
 

{% endhint %}

