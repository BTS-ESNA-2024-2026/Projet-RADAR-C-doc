# Installation

## Prérequis

Avant d'installer RADAR, assurez-vous d'avoir :

- Python 3.6 ou supérieur
- Un serveur Windows avec Active Directory accessible via SSH
- OpenSSH installé et configuré sur le serveur Windows
- Un compte avec les privilèges nécessaires pour interroger Active Directory

## Étapes d'installation

### 1. Cloner le projet

```bash
git clone https://github.com/BTS-ESNA-2024-2026/Projet-RADAR-C.git
cd Projet-RADAR-C
```

### 2. Créer et activer un environnement virtuel Python

=== "Linux/Mac"
    ```bash
    python3 -m venv venv
     source ./venv/bin/activate
    ```

=== "Windows"
    ```bash
    python3 -m venv venv
    venv\Scripts\activate
    ```

### 3. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 4. Rendre le script exécutable (optionnel)

!!! note "Linux/Mac uniquement"
    ```bash
    chmod +x main.py
    ```

## Configuration du serveur Windows

Pour que RADAR fonctionne, le serveur Windows doit avoir OpenSSH Server et le module Active Directory PowerShell installés.

### 1. Installation d'OpenSSH Server

Ouvrez PowerShell en tant qu'administrateur et exécutez :

```powershell
# Installer OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Démarrer le service
Start-Service sshd

# Configurer le démarrage automatique
Set-Service -Name sshd -StartupType 'Automatic'
```

### 2. Installation du module Active Directory PowerShell

```powershell
Install-WindowsFeature -Name "RSAT-AD-PowerShell" -IncludeAllSubFeature
```

### 3. Configuration du pare-feu

Pour autoriser les connexions SSH, configurez le pare-feu Windows :

```powershell
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```
