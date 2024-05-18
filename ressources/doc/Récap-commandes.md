# Récapitulatifs des commandes

- Pour WINDOWS nous privilégierons le gestionnaire paquets SCOOP pour certaines installations
(<https://scoop.sh/#/>)

- Pour MAC nous passerons par HOMEBREW FORMULAE (<https://formulae.brew.sh/>)

----

## Installation de l'environnement

1 - Installer Kubernetes via docker depuis les paramètres de docker desktop

2 - Installer `kubeclt` la CLI de Kubernetes

- WINDOWS :
  - <https://scoop.sh/#/apps?q=kubectl&id=17eabfd9d69e0947625d6ae59e55e43af3d51663>

```bash
  scoop bucket add main
  scoop install main/kubectl
```

- MAC : (NB : ici `kubectl` s'appelle `kubernetes-cli`)
  - <https://formulae.brew.sh/formula/kubernetes-cli#default>

```bash
  brew install kubernetes-cli
```

3 - Installer `OpenLens` votre interface graphique pour gérer les cluster Kubernetes

- WINDOWS :
  - <https://scoop.sh/#/apps?q=openlens&id=7a01ac6633e4bda71fd7944b5182df4f890eab9c>

```bash
  scoop bucket add extras
  scoop install extras/openlens
```

- MAC :
  - <https://formulae.brew.sh/cask/openlens#default>

```bash
  brew install --cask openlens
```

----

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
Workloads --> Pods --> filtre sur le Namespace:argocd --> cliquer sur argocd-server-xxxxx
--> scroll jusque "ports" et activer le `port fowarding` sur le 8080/TCP

2 - Se connecter:

une fois le port forwarding activer cliquer sur le 8080/TCP pour accéder à l'interface utilisateur.

/!\ votre connection sera en `HTTP` votre navigateur vous bloquera, choississez l'option pour passer outre et se accèder tout de même à la page malgré l'avertissement.

Le user par défaut est : `admin`

Pour obtenir le mot de passe entrer une des commandes suivantes:

NB : sauvegardez le !!!

- WINDOWS :

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | %{[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_))}
```

- MAC :

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o=jsonpath="{.data.password}" | base64 --decode
```

----

## Créer une connection entre argoCD et votre repo github

1 - Aller dans les `developpeur settings` de votre compte Github :

- Création d’un fine-grained token
- Ciblez le repos seulement accessible
- Remplissez l’ensemble des permissions, pour les besoins du support mettre toutes les autorisations au max (read and write ou read-only)

- /!\ votre token une fois généré ne sera visible qu'à ce moment sauvegardez le si nécessaire

2 - Pour de la création de votre connexion au repo (settings --> repositories) :

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
