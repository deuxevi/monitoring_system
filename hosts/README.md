Voici le fichier README en français pour décrire le contenu du fichier `Vagrantfile` :

---

# Configuration Vagrant pour l'Infrastructure de Monitoring

Ce dépôt contient la configuration Vagrant pour mettre en place une infrastructure simple avec des machines de monitoring et des machines cibles. L'infrastructure est conçue pour simuler un environnement où des outils de monitoring comme **Prometheus**, **Grafana**, et **Loki** peuvent être déployés et testés.

## Vue d'ensemble

La configuration Vagrant définit trois machines virtuelles (VM) :

- **monitor** : Une VM dédiée à l'exécution des outils de monitoring (par exemple, Prometheus, Grafana, Loki).
- **target1** : Une VM représentant une machine cible à surveiller.
- **target2** : Une autre machine cible à surveiller.

Chaque VM est configurée avec une adresse IP spécifique sur un réseau privé, et un playbook Ansible est utilisé pour provisionner les logiciels et la configuration nécessaires sur les VMs.

## Détails de la configuration Vagrant

Le fichier `Vagrantfile` définit trois machines virtuelles avec la configuration suivante :

### 1. VM Monitor
- **Nom d'hôte** : `monitor`
- **Adresse IP** : `192.168.56.104`
- **Box** : `generic/debian12` (Debian 12)
  
Cette machine sera utilisée pour exécuter les logiciels de monitoring (Prometheus, Grafana, Loki, etc.) qui collecteront et visualiseront les métriques et les logs.

### 2. VM Target1
- **Nom d'hôte** : `target1`
- **Adresse IP** : `192.168.56.12`
- **Box** : `generic/debian12` (Debian 12)

Cette machine sera surveillée par l'instance de Prometheus exécutée sur la VM `monitor`. Elle peut représenter n'importe quel serveur à surveiller.

### 3. VM Target2
- **Nom d'hôte** : `target2`
- **Adresse IP** : `192.168.56.163`
- **Box** : `generic/debian12` (Debian 12)

Comme pour `target1`, cette machine sera également surveillée par la VM `monitor`.

### Provisionnement avec Ansible

Les VMs sont provisionnées à l'aide d'un playbook Ansible situé dans le fichier `../provisioning/playbook.yml`. L'inventaire pour le playbook est fourni dans le fichier `../provisioning/inventory.ini`. Ce processus de provisionnement installera et configurera les outils de monitoring sur la machine `monitor` et tout agent nécessaire sur les machines cibles.

---

## Prérequis

Avant de commencer, assurez-vous d'avoir installé les outils suivants :

- **Vagrant** : Pour créer et gérer les machines virtuelles.
- **VirtualBox** (ou tout autre fournisseur compatible avec Vagrant) : Pour exécuter les VMs.
- **Ansible** : Pour provisionner les VMs avec les configurations nécessaires.

---

## Instructions d'installation

1. **Cloner le dépôt** :

   ```bash
   git clonehttps://github.com/deuxevi/monitoring_system.git
   cd monitoring_system/hosts
   ```

2. **Lancer les VMs avec Vagrant** :

   Utilisez la commande suivante pour créer et démarrer les VMs définies dans le `Vagrantfile` :

   ```bash
   vagrant up
   ```

3. **Provisionner les VMs avec Ansible** :

   Le provisionnement sera exécuté automatiquement après la création des VMs. Si vous souhaitez déclencher manuellement le provisionnement, utilisez la commande suivante :

   ```bash
   vagrant provision
   ```

   Cela exécutera le playbook Ansible situé dans `../provisioning/playbook.yml`, configurant les outils de monitoring et les machines cibles.

4. **Accéder à l'interface de monitoring** :

   Une fois les VMs provisionnées, vous pouvez accéder à l'interface de monitoring (par exemple, Grafana) sur la VM `monitor` à l'adresse suivante :

   - **Grafana** : `http://192.168.56.104:8081`

   Les identifiants par défaut sont les suivants :

   - **Nom d'utilisateur** : `admin`
   - **Mot de passe** : `admin`

---

## Configuration requise

### 1. Configuration des Sources de Données dans Grafana

Après le démarrage de Grafana, vous devrez configurer les sources de données pour que Grafana puisse récupérer les métriques de **Prometheus** et les logs de **Loki** :

1. **Prometheus** : 
   - Allez dans **Configuration** > **Sources de données** dans Grafana.
   - Ajoutez une nouvelle source de données de type **Prometheus**.
   - Entrez l'URL suivante : `http://192.168.56.104:9090` (l'IP de la VM `monitor` où Prometheus est en cours d'exécution).
   
2. **Loki** :
   - Ajoutez une nouvelle source de données de type **Loki**.
   - Entrez l'URL suivante : `http://192.168.56.104:3100` (l'IP de la VM `monitor` où Loki est en cours d'exécution).

Cela permettra à Grafana de se connecter à Prometheus pour les métriques et à Loki pour les logs.

Voici la correction de votre texte :

---

### 2. Configuration de Rocket.Chat pour Recevoir les Notifications d'Alerte

Afin de recevoir les notifications d'alertes de Prometheus via **Rocket.Chat**, vous devez configurer une intégration entre **Alertmanager** et Rocket.Chat :

1. **Créer un webhook dans Rocket.Chat** :
   - Allez dans **Administration** > **Intégrations** > **Webhooks sortants**.
   - Créez un nouveau webhook pour recevoir les notifications depuis Prometheus.
   - Copiez l'URL du webhook généré (cela sera utilisé dans **Alertmanager** pour envoyer les alertes).

2. **Configurer Alertmanager pour envoyer les alertes à Rocket.Chat** :
   - Mettez à jour le lien du webhook dans le fichier de configuration d'**Alertmanager** (`alertmanager.yml`).
   - Ajoutez ou modifiez la configuration suivante dans la section `receivers` pour pointer vers l'URL du webhook Rocket.Chat :

   ```yaml
   receivers:
     - name: 'rocketchat'
       webhook_configs:
         - url: 'https://chat.example.com/hooks/your-webhook-url'  # Remplacez par votre URL de webhook Rocket.Chat
   ```

Cela permettra à **Alertmanager** d'envoyer les alertes à votre instance **Rocket.Chat** via le webhook configuré.
