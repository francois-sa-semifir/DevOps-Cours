# Argo Autopilot

## Instalation d'argocd-autopilot

/!\ Pensez à reset votre cluster Kubernetes depuis les paramètres de docker desktop et le réinstaller
/!\ A la fin de l'installation pensez à sauvegarder votre mot de passe admin qui apparait dans votre terminal (avant dernière ligne)

- WINDOWS :

  ```bash
  Scoop install main/argocd-autopilot
  ```

  ```bash
  $env:GIT_REPO=“<votre_adresse_de_repo_pour_l'installation>”
  ```

  ```bash
  $env:GIT_TOKEN=“<votre_fine_grained_token_de_ce_repo>”
  ```

  ```bash
  argocd-autopilot repo bootstrap
  ```

  ```bash
  kubectl port-forward -n argocd svc/argocd-server 8080:80
  ```

- MAC :

  ```bash
  brew install argocd-autopilot
  ```

  ```bash
  export GIT_REPO=“<votre_adresse_de_repo_pour_l'installation>”
  ```

  ```bash
  export GIT_TOKEN=“<votre_fine_grained_token_de_ce_repo>”
  ```

  ```bash
  argocd-autopilot repo bootstrap
  ```

  ```bash
  kubectl port-forward -n argocd svc/argocd-server 8080:80
  ```

----

## Connexion à d'argocd-autopilot

Depuis OpenLens refaite un port forwarding comme pour ArgoCD classique et cliquer sur le lien (passer outre l'avertisement de connexion en HTTP de bvotre navigateur)

----

## Création d'un projet et d'un déploiement test avec argocd-autopilot

création du projet

  ```bash
-argocd-autopilot project create testing
```

création du déploiement dans le projet

```bash
argocd-autopilot app create hello-world --app github.com/argoproj-labs/argocd-autopilot/examples/demo-app/ -p testing --wait-timeout 2m
```
