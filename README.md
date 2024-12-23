### Étude et mise en place d'un système de monitoring des infrastructures informatiques

Ce projet propose une solution complète pour la surveillance des infrastructures informatiques en utilisant des outils open-source modernes tels que **Grafana**, **Prometheus**, et **Loki**. Développé dans le cadre d'un stage chez **Dac Technologies**, il répond aux besoins critiques de monitoring en permettant la collecte, l’analyse et la visualisation des métriques système, ainsi que la gestion centralisée des journaux applicatifs.

#### Fonctionnalités principales :
- **Visualisation des métriques système** (CPU, RAM, stockage, etc.) via des tableaux de bord Grafana personnalisés.
- **Gestion centralisée des logs** grâce à Loki et des requêtes flexibles en LogQL.
- **Système d’alertes proactives** configuré avec Prometheus pour notifier les anomalies en temps réel.
- **Architecture scalable et flexible** adaptée aux environnements distribués.
- **Automatisation de la collecte des données** avec des outils tels que Prometheus et Node Exporter, permettant une mise à jour continue des informations.
- **Tableaux de bord dynamiques** permettant une analyse approfondie des performances et des incidents de manière intuitive.

#### Perspectives :
- Intégration future du machine learning pour la prédiction des pannes et l’analyse prédictive des performances des systèmes.
- Automatisation des actions correctives en réponse aux alertes, réduisant ainsi le temps de réaction et les risques d’interruptions de service.
- Extension du monitoring aux applications métier spécifiques, avec la collecte de métriques sur des microservices ou des applications en conteneurs.
- Déploiement d'une plateforme multi-cloud, permettant de gérer des infrastructures hybrides et d’améliorer la résilience des systèmes.

#### Contenu du dépôt :
- **hosts/Vagrantfile :** Fichier de configuration pour la création d’une machine virtuelle de développement afin de tester l’architecture de monitoring.
- **provisioning/roles :** Rôles Ansible pour l’installation et la configuration des outils de monitoring (Prometheus, Grafana, Loki).
- **provisioning/inventory.ini :** Inventaire des hôtes à surveiller par le système de monitoring.
- **provisioning/playbook.yml :** Playbook Ansible pour automatiser le déploiement et la configuration de l’infrastructure de monitoring.
- **Mémoire :** Document détaillant l’analyse du système, la mise en œuvre, et les résultats des tests de performance.

---

#### Idéal pour :  
- **Administrateurs système** cherchant une solution open-source pour le monitoring des infrastructures informatiques.
- **Étudiants ou professionnels** souhaitant comprendre et mettre en œuvre une architecture de surveillance avancée dans un environnement distribué.
- **Entreprises** désireuses d'implémenter une solution flexible et évolutive pour la gestion des performances et la détection proactive des incidents.

---

[Prise en main](hosts/README.md)