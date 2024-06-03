---
title: "02 - DevOps - Docker"
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
    border-radius: 50px;
    font-size: 65%;
    font-weight: bolder
  }
</style>

# Docker

![Docker](/assets/Docker.svg) <!-- .element width="35%" align="left"-->
![semifir](/assets/logo_semifir.png) <!-- .element width="19%" align="right" -->

---

## Historique et Évolution des Technologies de Conteneurisation

----

### Contexte pré-conteneurisation : virtualisation traditionnelle

- Avant l'avènement de la conteneurisation, la virtualisation traditionnelle était dominante.

- Elle impliquait l'utilisation de machines virtuelles (VM) pour exécuter des applications sur des serveurs physiques.

- Chaque VM incluait un système d'exploitation complet, ce qui pouvait entrainer une surcharge significative des ressources système.

----

### Émergence des technologies de conteneurisation

1. **Chroot** : Cette fonctionnalité Unix permettait de changer le répertoire racine pour un processus, offrant une forme primitive d'isolation.

2. **LXC (Linux Containers)** : LXC a introduit une virtualisation légère en utilisant les cgroups et les namespaces du kernel Linux pour isoler les processus et les ressources.

----

3. **Cgroups et namespaces du kernel Linux** : Ces fonctionnalités du kernel Linux ont permis une isolation efficace des ressources système, ouvrant la voie à des technologies de conteneurisation plus avancées.

----

4. **Docker et l'avènement de la conteneurisation moderne** : Docker, lancé en 2013, a popularisé la conteneurisation en simplifiant le processus de création, de distribution et de gestion des conteneurs. Il a introduit un écosystème robuste et des outils conviviaux pour les développeurs et les opérationnels.

---

## Les Bases de la Conteneurisation

----

### Qu'est-ce qu'un conteneur ?

- Un conteneur est une unité d'exécution logicielle légère qui encapsule une application et toutes ses dépendances, y compris les bibliothèques et les variables d'environnement requises pour son fonctionnement.

----

### Différences entre la virtualisation et la conteneurisation

- La virtualisation crée des machines virtuelles distinctes avec leur propre système d'exploitation, tandis que la conteneurisation partage le noyau du système hôte et isole les processus et les ressources au niveau de l'application.

----

### Avantages de la conteneurisation

- Utilisation plus efficace des ressources système
- Démarrage rapide des applications
- Isolation des dépendances logicielles
- Portabilité entre les environnements de développement, de test et de production

---

## Lexique Docker

----

### Image

- Une image Docker est un modèle de lecture seule utilisé pour créer des conteneurs.

- Elle contient le système de fichiers de l'application, ainsi que tous les paramètres et dépendances nécessaires à son exécution.

----

### Conteneur

- Un conteneur Docker est une instance en cours d'exécution d'une image Docker.

- Il encapsule l'application et ses dépendances, offrant un environnement isolé et portable.

----

### Docker Engine

- Docker Engine est le moteur qui gère la création, l'exécution et la gestion des conteneurs Docker.

- Il comprend un démon de service et un ensemble d'API pour interagir avec les conteneurs.

----

### Dockerfile

- Un Dockerfile est un fichier de configuration utilisé pour décrire les étapes nécessaires à la construction d'une image Docker.

- Il contient des instructions pour installer des dépendances, copier des fichiers, et configurer l'environnement de l'application.

----

### Docker Compose

- Docker Compose est un outil permettant de définir et de gérer des applications multi-conteneurs.

- Il utilise un fichier de configuration YAML pour spécifier les services, les réseaux et les volumes nécessaires à l'application.

----

### Docker Hub

- Docker Hub est un registre de conteneurs public où les utilisateurs peuvent partager, découvrir et télécharger des images Docker.

- Il offre également des fonctionnalités de gestion des versions et des déploiements automatisés.

---

## Composition d'un Conteneur

----

### Couches d'une image Docker

- Une image Docker est composée de couches empilées les unes sur les autres.

- Chaque couche représente une instruction dans le Dockerfile et peut être partagée entre plusieurs images.

----

### Système de fichiers en couches

- Le système de fichiers en couches d'une image Docker permet une gestion efficace des modifications et des mises à jour.

- Les couches sont en lecture seule et les modifications sont stockées dans une couche de conteneur temporaire.

----

### Surcouche de conteneur

- Lorsqu'un conteneur est lancé à partir d'une image, une surcouche de conteneur en écriture est ajoutée au-dessus des couches de l'image.

- Cela permet au conteneur de stocker les modifications apportées au système de fichiers pendant son exécution.

---

## Fonctionnement

----

### Utilisation des namespaces et cgroups Linux

- Les conteneurs Docker utilisent les namespaces Linux pour isoler les processus, les utilisateurs, les réseaux et d'autres ressources système.

- Les cgroups sont utilisés pour limiter et contrôler l'accès aux ressources matérielles.

----

### Isolation des ressources

- Chaque conteneur Docker dispose de ses propres ressources isolées, telles que l'espace de noms réseau, les variables d'environnement et les systèmes de fichiers, garantissant une séparation complète avec les autres conteneurs et le système hôte.

----

### Communication avec le système hôte

- Les conteneurs Docker peuvent communiquer avec le système hôte via des interfaces réseau et des points de montage partagés.

- Cette communication est contrôlée et isolée pour empêcher les conteneurs d'interférer avec le fonctionnement du système hôte.

---

## Communication entre Conteneurs

----

### Docker Network : concepts et types de réseaux

- Docker prend en charge différents types de réseaux, tels que le pont, l'hôte et le sur-réseau, pour permettre la communication entre les conteneurs.

- Chaque réseau fournit un niveau d'isolation et de performance spécifique.

----

### Liaisons entre conteneurs

- Les conteneurs Docker peuvent être liés entre eux pour établir des communications directes via des adresses IP ou des noms de conteneurs.

- Cette fonctionnalité facilite le déploiement d'applications multi-conteneurs.

----

### Exposition de ports et accès aux services

- Les ports des conteneurs peuvent être exposés et publiés pour permettre l'accès aux services à partir du système hôte ou d'autres conteneurs.

- Cela facilite l'interaction entre les différents composants d'une application distribuée.

---

## Fonctionnement de Docker

----

### Architecture de Docker Engine

- Docker Engine est composé d'un démon de service et d'une API RESTful qui interagit avec les clients Docker.

- Le daemon gère la création, l'exécution et la gestion des conteneurs, tandis que l'API permet le contrôle et la surveillance à distance.

----

### Cycle de vie d'un conteneur Docker

- Le cycle de vie d'un conteneur Docker comprend les étapes de création, de démarrage, d'arrêt, de redémarrage et de suppression.

- Chaque étape peut être contrôlée à l'aide des commandes Docker appropriées.

----

### Gestion des images et des conteneurs

- Docker offre des commandes pour gérer les images et les conteneurs, y compris la construction, le téléchargement, la mise à jour, le démarrage, l'arrêt et la suppression.

- Ces commandes permettent aux utilisateurs de contrôler facilement l'environnement de leurs applications.

---

## Docker Hub

----

### Plateforme de partage d'images Docker

- Docker Hub est un registre de conteneurs public où les développeurs peuvent partager, découvrir et télécharger des images Docker.

- Il offre également des fonctionnalités de gestion des versions, de sécurité et de collaboration.

----

### Recherche et téléchargement d'images

- Les utilisateurs peuvent rechercher des images Docker sur Docker Hub en utilisant des mots-clés et des balises spécifiques.

- Ils peuvent ensuite télécharger les images et les utiliser pour leurs propres projets.

----

### Publication et partage d'images personnalisées

- Les développeurs peuvent publier et partager leurs propres images Docker sur Docker Hub pour permettre à d'autres utilisateurs de les utiliser.

- Cela facilite la distribution et le partage des logiciels et des infrastructures.

---

## Firecracker et les Micro VM

<https://firecracker-microvm.github.io/>
<https://katacontainers.io/>

----

### Firecracker : technologie de virtualisation de conteneurs légère

- Firecracker est une technologie de virtualisation de conteneurs légère conçue pour les charges de travail cloud-native.

- Elle utilise la virtualisation basée sur les noyaux KVM pour créer des micro-VM isolées et sécurisées.

----

### Avantages par rapport à la virtualisation traditionnelle

- Firecracker offre un démarrage rapide, une empreinte mémoire réduite et une isolation efficace des ressources par rapport à la virtualisation traditionnelle.

- Cela en fait un choix idéal pour les environnements de conteneurisation hautement évolutifs.

----

### Utilisation conjointe avec Docker pour des scénarios spécifiques

- Docker peut être utilisé en conjonction avec Firecracker pour des scénarios spécifiques nécessitant une isolation supplémentaire ou une sécurité renforcée.

- Firecracker offre une alternative légère à la virtualisation traditionnelle pour les charges de travail cloud-native.

---

## La suite

[Dockerfile](03_DevOps_DockerfIle.md)

![Docker](/assets/Docker.svg) <!-- .element width="35%" -->
