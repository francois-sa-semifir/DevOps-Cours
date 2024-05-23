---
title: "01 - DevOps - Mise en place"
theme: "solarized"
revealOptions:
  transition: "slide"
  slideNumber: false
  touch: true
sources: 
  - 
  - 
author: 
  - "Francois Salmon"
---

<head>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css">
</head>

<style type="text/css">
  body{
    position: relative;
    height: 100vh;
  }

  body:before{
    content: ' ';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: url(https://raw.githubusercontent.com/tamo-semifir/gcp-assets/main/logo_semifir.png) no-repeat center fixed;
    background-size: 75vh 45vw;
    opacity: 0.2
  }

  code {
    color: #EB5757;
    background-color: rgba(135,131,120,0.15);
    border-radius: 10px;
    font-size: 90%;
  }
</style>

# Setup

![Setup](/assets/Setup.png) <!-- .element width="25%" align="left"-->
![semifir](/assets/logo_semifir.png) <!-- .element width="19%" align="right" -->

---

## Plan

- Installation des extensions vscode
- Installation du WSL
- Installation de Docker Desktop
- Activation de Kubernetes via Docker
- Kubectl et k9s
- Installation d'OpenLens
- Création du repo Github
- TD - Flask / Mongo

---

## Installation des extensions vscode

- Docker
- GitHub actions
- Indent-rainbow
- Kubernetes
- Markdown Preview Enhanced
- Python
- YAML

---

## Installation du WSL

![Korben](/assets/Korben.webp) <!-- .element width="35%" -->

[WSL](https://korben.info/installer-wsl2-windows-linux.html)

Notes:
<https://korben.info/installer-wsl2-windows-linux.html>

---

## Installation de Docker Desktop

![Docker](/assets/Docker.svg) <!-- .element width="35%" -->

[Docker](https://www.docker.com/products/docker-desktop/)

Notes:
<https://www.docker.com/products/docker-desktop/>

---

## Activation de Kubernetes via Docker

![Kub in Docker](/assets/paramètrage/Settings_Kub_in_Docker.png) <!-- .element width="58%" -->

![Kubernets](/assets/Kubernets.svg) <!-- .element width="5%" -->

---

## Kubectl et k9s

- Prérequis : Installation de [scoop](https://scoop.sh/)

- Dans un terminal PowerShell :

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

Notes:
<https://scoop.sh/>

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

----

- Installer [kubeclt](https://scoop.sh/#/apps?q=kubectl&id=17eabfd9d69e0947625d6ae59e55e43af3d51663) la CLI de Kubernetes

```bash
  scoop bucket add main
  scoop install main/kubectl
```

Notes:
<https://scoop.sh/#/apps?q=kubectl&id=17eabfd9d69e0947625d6ae59e55e43af3d51663>

```bash
  scoop bucket add main
  scoop install main/kubectl
```

- MAC : (NB : ici `kubectl` s'appelle `kubernetes-cli`)
  - <https://formulae.brew.sh/formula/kubernetes-cli#default>

```bash
  brew install kubernetes-cli
```

----

- Installer [k9s](https://scoop.sh/#/apps?q=k9s&id=395ddffa078b80f536e081b96533c098a3da719b) un gestionnaire de cluster Kubernetes en ligne de commande

```bash
scoop install main/k9s
```

Notes:
<https://scoop.sh/#/apps?q=k9s&id=395ddffa078b80f536e081b96533c098a3da719b>

```bash
scoop install main/k9s
```

---

## Installation d'OpenLens (Via Scoop)

- Installer [OpenLens](https://scoop.sh/#/apps?q=openlens&id=7a01ac6633e4bda71fd7944b5182df4f890eab9c) interface graphique pour gérer les cluster Kubernetes

```bash
  scoop bucket add extras
  scoop install extras/openlens
```

Notes:
<https://scoop.sh/#/apps?q=openlens&id=7a01ac6633e4bda71fd7944b5182df4f890eab9c>

```bash
  scoop bucket add extras
  scoop install extras/openlens
```

- MAC :
  - <https://formulae.brew.sh/cask/openlens#default>

```bash
  brew install --cask openlens
```

---

## Installation d'OpenLens (Alternative)

Installer [OpenLens](https://github.com/MuhammedKalkan/OpenLens/releases)

- pour Windows choisir la release `OpenLens.Setup.6.5.2-366.exe`

- pour Mac choisir la release `OpenLens-6.5.2-366-mac.zip`

---

## Création du repo Github

- Assurez-vous que vous ayez un compte `Github` **et** une `connexion SSH` entre votre machine et votre compte

  - Générer une clef SSH [ici](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

  - Lier sa clef à son compte Github [ici](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

- Se créer un repo Github pour la réalisation des TD, appelez-le par exemple `DevOps` et générer un fichier `README.md`

---

## Installatio de Git (si non présent)

- Installer Git sur votre machine [ici](https://git-scm.com/downloads)

- Configurer un `username` et un `email` pour signer vos futurs `commit`

  - Tuto [ici](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Param%C3%A9trage-%C3%A0-la-premi%C3%A8re-utilisation-de-Git) dan la partie `votre identité` de la page

---

## TD - Flask / Mongo

[par ici](./demo/01.1_DevOps_TD_Flask_Mongo.md)

---

## La suite

[Docker](02_DevOps_Docker.md)

![Docker](/assets/Docker.svg) <!-- .element width="35%" -->
