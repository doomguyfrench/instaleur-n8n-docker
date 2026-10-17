#  Installeur n8n avec Docker

Ce projet permet d'installer automatiquement **n8n et PostgreSQL** sur un NAS Linux préalablement configuré avec mon script d'infrastructure réseau.

n8n est un outil d'automatisation de workflows permettant de connecter différents services et d'automatiser des tâches.

L'objectif est de pouvoir ajouter facilement n8n à un serveur domestique existant, sans avoir à configurer manuellement Docker Compose et PostgreSQL.

---

## :jigsaw: Prérequis

Avant de lancer l'installation, vous devez disposer de :

- Une machine Debian ou une distribution compatible avec APT.
- Une connexion Internet.
- Un utilisateur Linux disposant des droits `sudo`.
- Docker et Docker Compose installés et fonctionnels.
- Mon script de préparation du NAS déjà exécuté.

Le script a été testé sur une machine vierge après l'installation préalable de l'infrastructure NAS.

---

## :rocket: Installation

### 1. Télécharger le projet

```bash
git clone https://github.com/doomguyfrench/instaleur-n8n-docker.git
```

### 2. Entrer dans le répertoire

```bash
cd instaleur-n8n-docker
```

### 3. Lancer l'installation

```bash
chmod +x install.sh
sudo ./install.sh
```

Le script prépare automatiquement les répertoires nécessaires, génère la configuration de n8n et de PostgreSQL, puis démarre les conteneurs Docker.

---

## :globe_with_meridians: Accéder à n8n

À la fin de l'installation, l'adresse IP du NAS est affichée dans le terminal.

Accédez à l'interface depuis un navigateur :

```text
http://IP_DU_NAS:5678
```

Remplacez `IP_DU_NAS` par l'adresse IP de votre serveur.

Vous pourrez ensuite effectuer la configuration initiale de n8n.

---

## :file_folder: Organisation des fichiers

Les fichiers sont stockés dans :

```text
/home/<utilisateur>/docker/n8n/
│
├── .env
├── docker-compose.yml
│
├── postgresql/
│   └── Données de PostgreSQL
│
├── n8n_data/
│   └── Données persistantes de n8n
│
└── n8n_files/
    └── Fichiers accessibles à n8n
```

Les données sont conservées dans les répertoires montés en volumes Docker.

**Important :** ne supprimez pas ces répertoires si vous souhaitez conserver les données de votre installation.

---

## :whale: Gestion des conteneurs

Pour accéder au répertoire d'installation :

```bash
cd ~/docker/n8n
```

Afficher l'état des conteneurs :

```bash
sudo docker compose ps
```

Afficher les journaux :

```bash
sudo docker compose logs -f
```

Redémarrer les services :

```bash
sudo docker compose restart
```

Arrêter les services :

```bash
sudo docker compose down
```

---

## :electric_plug: Ports utilisés

| Service | Port | Protocole |
|---|---:|---|
| n8n | 5678 | TCP |
| PostgreSQL | 5432 | Réseau interne Docker |

Le port 5678 est utilisé pour accéder à l'interface de n8n.

PostgreSQL est utilisé par n8n pour stocker ses données.

---

## :closed_lock_with_key: Sécurité

- Ne partagez pas votre fichier `.env`, qui contient la configuration et les identifiants de la base de données.
- Évitez d'exposer directement n8n sur Internet sans configuration adaptée.
- Pour un accès distant, configurez HTTPS et les protections réseau nécessaires.
- Effectuez régulièrement des sauvegardes de n8n et de PostgreSQL.

---

## :scroll: Licence

Ce projet est distribué sous licence MIT. Consultez le fichier [LICENSE](LICENSE) pour plus d'informations.

---

## :link: Projet associé

Ce projet complète mon script d'infrastructure NAS, qui prépare notamment Docker et le réseau nécessaires à l'hébergement des services.

Retrouvez mes projets sur GitHub :

- [Installeur n8n Docker](https://github.com/doomguyfrench/instaleur-n8n-docker)
- [Autres projets](https://github.com/doomguyfrench)

---

## :pushpin: Objectif

Proposer une installation simple et reproductible de n8n sur un NAS personnel, en complément d'une infrastructure domestique déjà opérationnelle.