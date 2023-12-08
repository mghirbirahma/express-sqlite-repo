# Projet Express SQLite

## Description

Ce projet implémente un pipeline automatisé pour extraire le code source d'une application web à partir d'une image Docker, puis le transférer vers un dépôt GitHub. L'application web utilise Express et SQLite.

## Exécution du Pipeline

### Prérequis

- Docker installé sur votre machine
- Un jeton d'accès GitHub pour les opérations d'écriture dans le dépôt

### Étapes pour l'exécution

1. **Clonez ce dépôt :**

    ```bash
    git clone https://github.com/mghirbirahma/express-sqlite-repo.git
    cd express-sqlite-repo
    ```

2. **Exécutez le script d'extraction :**

    ```bash
    ./extraction.sh
    ```

    Ce script crée un conteneur temporaire à partir de l'image Docker `mghirbirahma/express-sqlite-app`, extrait le code source du répertoire `/app` du conteneur, puis le copie dans le répertoire local `code_source`.

3. **Ajoutez, commitez et poussez les changements vers GitHub :**

    ```bash
    git add .
    git commit -m "Ajout du code source extrait depuis l'image Docker"
    git push origin master
    ```

4. **Extraire l'image depuis Docker Hub, créer un conteneur local, puis le supprimer :**

    ```bash
    # Extraire l'image depuis Docker Hub
    docker pull mghirbirahma/express-sqlite-app

    # Créer un conteneur local
    docker run -it --name local-container mghirbirahma/express-sqlite-app

    # Copier le code source ou faire d'autres opérations si nécessaire

    # Supprimer le conteneur local
    docker rm local-container
    ```

5. **Cloner le dépôt GitHub localement :**

    ```bash
    git clone https://github.com/mghirbirahma/express-sqlite-repo.git
    ```

## Structure du Code Source

- **/app** : Contient le code source de l'application web.
- **/scripts** : Contient le script d'extraction (`extraction.sh`).

## Détails du Pipeline

### Étape d'Extraction

Le script `extraction.sh` effectue les opérations suivantes :

```bash
#!/bin/bash

# Nom de l'image sur Docker Hub
DOCKER_IMAGE=mghirbirahma/express-sqlite-app

# Nom du conteneur temporaire
CONTAINER_NAME=express-sqlite-container

# Création d'un conteneur temporaire
docker create --name $CONTAINER_NAME $DOCKER_IMAGE

# Copie du code source depuis le conteneur
docker cp $CONTAINER_NAME:/app ./code_source

# Suppression du conteneur temporaire
docker rm $CONTAINER_NAME

Transfert vers GitHub
Les commandes suivantes sont utilisées pour transférer le code source extrait vers le dépôt GitHub :

git add .
git commit -m "Ajout du code source extrait depuis l'image Docker"
git push origin master


Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une pull request pour proposer des améliorations ou corriger des problèmes.

Licence
Ce projet est sous licence MIT.


Assurez-vous de personnaliser ces informations en fonction de votre propre projet. Cela inclut les commandes spécifiques pour extraire l'image depuis Docker Hub, créer un conteneur local, le supprimer, et cloner le dépôt GitHub.
