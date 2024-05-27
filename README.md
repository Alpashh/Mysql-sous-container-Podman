# MySQL-sous-container-Podman

Petit tuto pour installer et utiliser MySQL sous container Podman :

## Prérequis

- Assurez-vous que Podman est installé sur votre système. Vous pouvez suivre les instructions d'installation de Podman pour votre système d'exploitation [ici](https://podman.io/getting-started/installation).

## Étapes

### 1. Installer Podman et MySQL

Pour installer MySQL en utilisant Podman, exécutez la commande suivante :

```sh
podman run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest
```

### 2. Vérifier que le conteneur MySQL est en cours d'exécution

Pour vérifier que le conteneur MySQL est en cours d'exécution, utilisez la commande suivante :

```
podman ps
```

Cette commande liste les conteneurs en cours d'exécution et vous devriez voir votre conteneur MySQL dans la liste.

### 3. Se connecter à MySQL à partir du conteneur

Vous pouvez vous connecter à MySQL directement depuis le conteneur en utilisant la commande suivante :

```
podman exec -it mysql mysql -uroot -p
```

Vous serez invité à entrer le mot de passe root que vous avez défini (my-secret-pw).

### 4. Connexion MySQL à partir de l'hôte

Si vous voulez vous connecter à MySQL depuis votre hôte (la machine sur laquelle Podman est installé), vous devrez exposer le port MySQL. Pour ce faire, arrêtez le conteneur existant et relancez-le en exposant le port :

```
podman stop mysql
podman rm mysql
podman run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql:latest
```

Maintenant, vous pouvez vous connecter à MySQL depuis votre hôte en utilisant un client MySQL ou la ligne de commande :

```
mysql -h 127.0.0.1 -P 3306 -uroot -p
```
