# 🚀 Déploiement Automatisé avec Ansible

> Projet DevOps — Installation automatique Apache + Rolling Deployment sur 3 VMs Ubuntu (VirtualBox)

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                      VirtualBox                         │
│                                                         │
│   ┌──────────────────┐                                  │
│   │   CONTRÔLEUR     │  SSH → web1 (10.0.0.1)          │
│   │   10.0.0.3       │  SSH → web2 (10.0.0.2)          │
│   │   (Ansible)      │                                  │
│   └──────────────────┘                                  │
│                                                         │
│   Accès depuis PC Windows :                             │
│   http://192.168.56.102  → web1                         │
│   http://192.168.56.101  → web2                         │
└─────────────────────────────────────────────────────────┘
```

| Machine      | IP Interne  | IP Host-Only      | Rôle        |
|--------------|-------------|-------------------|-------------|
| Contrôleur   | 10.0.0.3    | —                 | Ansible     |
| web1         | 10.0.0.1    | 192.168.56.102    | Apache      |
| web2         | 10.0.0.2    | 192.168.56.101    | Apache      |

---

## 📂 Structure du projet

```
ansible-complet/
│
├── hosts                          ← Inventaire (liste des serveurs)
├── ansible.cfg                    ← Configuration Ansible
├── deploy.yml                     ← Playbook Rolling Deployment
├── rollback.yml                   ← Playbook Rollback
│
├── group_vars/
│   ├── all.yml                    ← Variables pour toutes les machines
│   └── webservers.yml             ← Variables pour le groupe webservers
│
├── host_vars/
│   ├── web1.yml                   ← Variables spécifiques web1
│   └── web2.yml                   ← Variables spécifiques web2
│
└── roles/
    └── apache/
        ├── tasks/main.yml         ← Tâches d'installation Apache
        ├── handlers/main.yml      ← Handler redémarrage Apache
        ├── templates/index.html.j2← Page web (Jinja2)
        └── vars/main.yml          ← Variables du role
```

---

## 🚀 Lancer le déploiement

```bash
# Test de connexion
ansible all -m ping

# Déploiement complet (Rolling)
ansible-playbook deploy.yml

# En cas de problème : rollback
ansible-playbook rollback.yml
```

---

## 🔁 Rolling Deployment

Le fichier `deploy.yml` utilise `serial: 1` :
- web1 mis à jour → vérifié ✅ → web2 mis à jour
- Si web1 échoue → web2 reste disponible ✅
- Zéro interruption de service ✅

---

## 🌐 Voir les pages web

Ouvrir dans le navigateur sur ton PC Windows :

```
http://192.168.56.102   → page web1 (thème bleu)
http://192.168.56.101   → page web2 (thème violet)
```

---

## 📦 Git

```bash
git init
git add .
git commit -m "Initial commit - Ansible Apache Rolling Deployment"
git remote add origin https://github.com/TON_USERNAME/ansible-projet.git
git push -u origin main
```
