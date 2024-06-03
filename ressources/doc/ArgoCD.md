# ArgoCD

## Instancier un pod via kubectl

```bash
kubectl apply –f <emplacement_fichier>\<nom_de_fichier>
```

----

## Installation d'ArgoCD

via Kubectl depuis votre terminal

- WINDOWS :

```bash
kubectl create namespace argocd 
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

- MAC :

  - <https://formulae.brew.sh/formula/argocd#default>
  
```bash
brew install argocd
```

----

## Connection à argoCD

1 - Activer le port forwarding:

Depuis openLens (catalogue puis cliquer sur votre cluster pour l'instancier):
Workloads --> Pods --> filtre sur le `Namespace:argocd` --> cliquer sur `argocd-server-xxxxx` --> scroll jusque "ports" et activer le `port fowarding` sur le 8080/TCP

Ou en version ligne de commande

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:8080
```

2 - Se connecter:

une fois le port forwarding activer cliquer sur le 8080/TCP pour accéder à l'interface utilisateur.

/!\ votre connection sera en `HTTP` votre navigateur vous bloquera, choississez l'option pour passer outre et se accèder tout de même à la page malgré l'avertissement.

Le user par défaut est : `admin`

### Mot de passe Admin principal

- Depuis OpenLens :

Depuis OpenLens (catalogue puis cliquer sur votre cluster pour l'instancier):
Config --> Secrets --> filtre sur `All namespaces` ou `Namespace:argocd` --> cliquer sur `argocd-initial-admin-secret` --> récupérer le mot de passe

- En ligne de commande :

  - WINDOWS :
  
    - version Bash

    ```bash
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
    ```

    - version Powershell

    ```Powershell
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | %{[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_))}
    ```

  - MAC :

  ```bash
  kubectl -n argocd get secret argocd-initial-admin-secret -o=jsonpath="{.data.password}" | base64 --decode
  ```

----

## Créer une connection entre argoCD et votre repo github

1 - Dans votre compte Github :

- Aller dans les `settings` de votre compte
- Puis `Developper Settings` (<https://github.com/settings/apps>) --> `Personnal access tokens` --> `fine-grained token` --> Generate new token

- Choisissez un nom, une expiration
- Dans la partie `Repository access`, la 3eme options et cibler le nom de votre repository de travail

- Puis dans `Permissions` --> `Repository permissions`rRemplissez l’ensemble des permissions, pour les besoins du support mettre toutes les autorisations au max (read and write ou read-only)

  !\ votre token une fois généré il ne sera visible qu'à ce moment `sauvegardez le si nécessaire`

2 - Depuis ArgoCD

Création d'une connexion au repo (`settings` --> `repositories`) :

- Sélectionnez la méthode https (puis ajoutez l'URL de votre repo)
- Mettez votre nom de compte Github
- A la place du mot de passe saisissez le token

--> argoCD peut maintenant lire les fichiers de déploiements (manifiests) de votre repo Github

----

## Créer une pipeline CD avec ArgoCD

Dépendant de l'emplacement de votre fichier remplissez le `PATH`

-> remplissez avec juste `.` si votre fichier de déploiement est situé à la racine
-> sinon indiquez le chemin ./emplacement_1/emplacement_2/...

/!\ Si votre manifest est dans un répertoire pensez à cocher la fonction `Directory Recurse` afin d'indiquer à ArgoCd qu'il doit lire un fichier dans un répertoire.

General :
  Application Name : un nom en minuscule

Project Name : default

Sync Policy : Manual ou Automatic

Destination:

- <https://kubernetes.default.svc> --> noeud par défaut
- Namespace : à définir

----

## Installation d'ArgoCD-CLI

- WINDOWS :

```bash
scopp add main # si vous n'avez pas encore installé le bucket main
scoop install main/argocd
```

- MAC :

Déjà fait `:)`

----

## Connection à ArgoCD depuis d'ArgoCD-CLI

```bash
argocd login localhost:<port_présent_dans_l'URL_de_votre_navigateur>
```

- Ex:

```bash
argocd login localhost:8080 # Connexion au serveur argocd avec votre identifiant et mot de passe admin
```

----

## Setup d'un mdp de compte utilisateur depuis d'ArgoCD-CLI

```bash
argocd account update-password --account <nom_du_rôle>
```

----

## Ajout de rôle à compte utilisateur depuis d'ArgoCD-CLI

```bash
argocd proj role add-group <nom-du_groupe> <nom_du_compte> <nom_du_rôle>
```

- Ex:

```bash
argocd proj role add-group pipelinecicd developpeur developpeur
```

----

## Commandes Utiles ArgoCD

```bash
# Liste des applications
argocd app list

# Détail d'une application
argocd app get <nom_application>

# Liste des projets
argocd proj list

# Détail d'un projet
argocd proj get <nom_projet>
```
