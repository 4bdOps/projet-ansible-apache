# Projet 6 : Déploiement Automatisé et Rolling Deployment avec Ansible

Ce projet consiste à automatiser l'installation, la configuration et la mise à jour d'un serveur web Apache sur une infrastructure virtuelle. L'objectif est de garantir un déploiement fiable et esthétique tout en utilisant les meilleures pratiques DevOps comme le **Rolling Deployment**.

## 🚀 Fonctionnalités du Projet
- **Installation Automatisée** : Déploiement du serveur Apache2 via un Playbook Ansible.
- **Gestion d'Inventaire** : Utilisation d'un fichier `inventory.ini` pour cibler dynamiquement les serveurs.
- **Interface Web Esthétique** : Déploiement d'une page `index.html` moderne (CSS3) avec support complet des accents (UTF-8).
- **Continuité de Service** : Mise en œuvre d'une stratégie de "Rolling Update" via la directive `serial`.

---

## 👥 Membres du Groupe et Répartition des Tâches

Conformément aux objectifs du projet, les responsabilités ont été réparties entre les 4 membres de l'équipe :

| Membre | Rôle | Tâches principales |
| :--- | :--- | :--- |
| **Abdellah YEOUSSOMMASS** | **Lead DevOps** | Initialisation du projet Git, configuration de l'inventaire et synchronisation GitHub. |
| **Miguel ZDIDIDU** | **Administrateur Système** | Configuration de la VM cible, gestion de la connectivité SSH et des accès privilégiés (sudo). |
| **Chaimae MOUSSALY** | **Ingénieur Automatisation** | Développement du Playbook Ansible (`install_apache.yml`) et gestion du Rolling Deployment. |
| **Moncef ESSAKEN** | **Développeur Web & QA** | Création de la page web, design CSS, correction de l'encodage UTF-8 et tests finaux. |

---

## 📋 Documentation des Étapes de Réalisation

Le projet a été mené à bien en suivant ces étapes détaillées :

### 1. Préparation de l'Infrastructure
- Création du répertoire de travail et initialisation de Git.
- Configuration du fichier `inventory.ini` avec l'adresse IP de la machine cible (`10.0.2.15`).
- Validation de la communication entre le nœud maître et le nœud géré via la commande `ansible ping`.

### 2. Développement du Playbook
- Rédaction des tâches pour l'installation du paquet `apache2`.
- Utilisation de la directive `become: yes` pour obtenir les droits root nécessaires à l'installation.
- Configuration du service pour qu'il soit démarré et activé au boot.

### 3. Création et Déploiement du Contenu
- Conception d'une page web esthétique avec CSS intégré.
- **Correction des accents** : Utilisation de `<meta charset="UTF-8">` pour assurer un affichage parfait des caractères spéciaux.
- Automatisation du transfert du fichier vers `/var/www/html/` via le module `copy`.

### 4. Rolling Deployment & Finalisation
- Ajout de `serial: 1` dans le playbook pour simuler une mise à jour progressive.
- Versionnage final du code et export du projet vers le dépôt distant GitHub.

---

## 🛠️ Guide d'Utilisation

Pour déployer la solution sur votre propre infrastructure :

1. Assurez-vous d'avoir Ansible installé.
2. Clonez ce dépôt.
3. Exécutez le playbook avec la commande suivante :
   ```bash
   ansible-playbook -i inventory.ini install_apache.yml -K
