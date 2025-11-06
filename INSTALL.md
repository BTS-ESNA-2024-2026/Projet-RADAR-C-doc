## Installation / Setup

- Dépendances
- Étapes pour lancer le projet en local (cmd, docker, etc.)

# RADAR

Radar est un outil pour récupérer des informations depuis un Active Directory distant.

## Installation:

### Prérequis

- Python 3.6 ou supérieur
- Un serveur Windows avec Active Directory accessible via SSH
- OpenSSH installé et configuré sur le serveur Windows
- Un compte avec les privilèges nécessaires pour interroger Active Directory

### Étapes d'installation

1. **Cloner le projet**
    
    ```bash
    git clone <repository-url>
    cd radar
    ```
    
2. **Créer et activer un environnement virtuel Python**
    
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # Sur Linux/Mac
    # ou
    venv\\Scripts\\activate  # Sur Windows
    ```
    
3. **Installer les dépendances**
    
    ```bash
    pip install -r requirements.txt
    ```
    
4. **Rendre le script exécutable (optionnel, Linux/Mac uniquement)**
    
    ```bash
    chmod +x main.py
    ```
    

## Configuration du serveur Windows

Pour que RADAR fonctionne, le serveur Windows doit :

1. **Avoir OpenSSH Server installé et démarré**
    
    ```powershell
    # Dans PowerShell en tant qu'administrateur
    Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
    Start-Service sshd
    Set-Service -Name sshd -StartupType 'Automatic'
    ```
    
2. **Avoir le module Active Directory PowerShell installé**
    
    ```powershell
    Install-WindowsFeature -Name "RSAT-AD-PowerShell" -IncludeAllSubFeature
    ```
    
3. **Autoriser les connexions SSH** (configurer le pare-feu si nécessaire)
    
    ```powershell
    New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
    ```