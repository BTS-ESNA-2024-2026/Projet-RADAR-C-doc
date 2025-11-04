# RADAR

Un outil pour récupérer des informations depuis un Active Directory distant.

## Installation

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
   venv\Scripts\activate  # Sur Windows
   ```

3. **Installer les dépendances**

   ```bash
   pip install -r requirements.txt
   ```

4. **Rendre le script exécutable (optionnel, Linux/Mac uniquement)**

   ```bash
   chmod +x main.py
   ```

### Configuration du serveur Windows

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

## Utilisation

### Syntaxe de base

```bash
python main.py --host <IP_SERVEUR> --username <NOM_UTILISATEUR> --password <MOT_DE_PASSE> [OPTIONS]
```

### Options disponibles

- `-u`, `--users` : Lister tous les utilisateurs
- `-c`, `--computers` : Lister tous les ordinateurs
- `-g`, `--groups` : Lister tous les groupes
- `-dc`, `--domain-controllers` : Lister tous les contrôleurs de domaine
- `--disabled` : Filtrer uniquement les utilisateurs désactivés (à utiliser avec `--users`)
- `--expired` : Filtrer uniquement les utilisateurs expirés (à utiliser avec `--users`)
- `--debug` : Activer le mode debug pour afficher les commandes exécutées

### Exemples d'utilisation

#### Lister tous les utilisateurs

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --users
```

Sortie :

```text
ID | Username  | Firstname | Lastname | Groups    | Last login  | Disabled | Expired
---|-----------|-----------|----------|-----------|-------------|----------|--------
1  | john.doe  | john      | doe      | employees | 10/05 15h03 | Yes      | Yes
2  | bob.clark | bob       | clark    | employees | 01/12 02h28 | No       | No
```

#### Lister uniquement les utilisateurs désactivés

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --users --disabled
```

#### Lister uniquement les utilisateurs expirés

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --users --expired
```

#### Lister tous les ordinateurs

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --computers
```

Sortie :

```text
ID | Hostname | Groups
---|----------|-------
1  | PC-ROOM1 | school
```

#### Lister tous les groupes

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --groups
```

Sortie :

```text
ID | Name      | Members
---|-----------|---------
1  | employees | john.doe
```

#### Lister tous les contrôleurs de domaine

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --domain-controllers
```

Sortie :

```text
ID | Name | IP
---|------|--------------
1  | dc1  | 192.168.1.123
```

#### Mode debug

```bash
python main.py --host 192.168.1.100 --username Administrateur --password AdminP4ss --users --debug
```

## Fonctionnement

RADAR se connecte via SSH à un serveur Windows et exécute des commandes PowerShell pour interroger Active Directory.
# radar_doc
