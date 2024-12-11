# Vagrant Setup for Multi-VM Environment

Ce projet configure un environnement multi-VM avec Vagrant. Il inclut trois machines virtuelles : `monitor`, `moodle` et `jitsimeet`, toutes basées sur Debian 12.

## Prérequis

Avant de commencer, assurez-vous que votre système dispose des éléments suivants :

- [Vagrant](https://www.vagrantup.com/) (version 2.0 ou ultérieure)
- [VirtualBox](https://www.virtualbox.org/) (ou tout autre fournisseur compatible avec Vagrant)

## Installation

1. Clonez ce dépôt sur votre machine locale :

    ```bash
    git clone <URL_DU_DEPOT>
    cd <NOM_DU_DEPOT>
    ```

2. Initialisez les machines virtuelles avec Vagrant :

    ```bash
    vagrant up
    ```

## Configuration des Machines Virtuelles

### Monitor
- **Hostname** : `monitor`
- **IP privée** : `192.168.56.104`
- **Box** : `generic/debian12`

### Moodle
- **Hostname** : `moodle`
- **IP privée** : `192.168.56.12`
- **Box** : `generic/debian12`

### Jitsi Meet
- **Hostname** : `jitsimeet`
- **IP privée** : `192.168.56.163`
- **Box** : `generic/debian12`

## Notes

1. **Ressources des VM** : Par défaut, les configurations de mémoire et CPU sont commentées. Pour ajuster ces paramètres, décommentez et modifiez la section suivante dans le fichier Vagrantfile :

    ```ruby
    config.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
      vb.cpus = 2
    end
    ```

2. **Redirection de ports** : Une section pour la redirection de ports est également incluse, mais elle est commentée. Vous pouvez la personnaliser en décommentant et ajustant la configuration :

    ```ruby
    config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
    config.vm.usable_port_range = (8000..9000)
    ```

## Commandes Utiles

- **Démarrer les VM** :

    ```bash
    vagrant up
    ```

- **Se connecter à une VM** :

    ```bash
    vagrant ssh <nom_vm>
    ```

    Exemple :
    ```bash
    vagrant ssh monitor
    ```

- **Arrêter les VM** :

    ```bash
    vagrant halt
    ```

- **Détruire les VM** :

    ```bash
    vagrant destroy
    ```

## Support

Pour toute question ou problème, veuillez ouvrir un ticket dans ce dépôt ou contacter l'administrateur du projet.

---

**Auteur** : [Votre Nom]  
**Licence** : [Type de licence, ex : MIT, GPL, etc.]
