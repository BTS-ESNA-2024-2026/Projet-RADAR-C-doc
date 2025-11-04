# Fonctionnement

## Flux d'exécution

1. **Connexion SSH** : RADAR établit une connexion SSH sécurisée vers le serveur Windows
2. **Exécution PowerShell** : Les commandes PowerShell sont envoyées via la session SSH
3. **Interrogation AD** : PowerShell interroge Active Directory avec les cmdlets appropriés
4. **Traitement des données** : Les résultats sont parsés et formatés
5. **Affichage** : Les données sont présentées sous forme de tableaux

## Structure du projet

```
radar/
├── main.py                 # Point d'entrée
├── src/
│   ├── __init__.py
│   ├── radar.py           # Classe principale
│   ├── ssh_connector.py   # Gestion SSH
│   ├── ad_client.py       # Commandes AD
│   ├── formatter.py       # Formatage tableaux
│   └── models.py          # Modèles de données
├── requirements.txt       # Dépendances
└── README.md             # Documentation
```

## Commandes PowerShell utilisées

### Get-ADUser

Récupère les informations sur les utilisateurs :

```powershell
Get-ADUser -Filter * -Properties *
```

Propriétés récupérées :
- SamAccountName (nom d'utilisateur)
- GivenName (prénom)
- Surname (nom de famille)
- Enabled (compte actif/désactivé)
- AccountExpirationDate (date d'expiration)
- LastLogonDate (dernière connexion)
- MemberOf (groupes)

### Get-ADComputer

Récupère les informations sur les ordinateurs :

```powershell
Get-ADComputer -Filter * -Properties *
```

### Get-ADGroup et Get-ADGroupMember

Récupère les groupes et leurs membres :

```powershell
Get-ADGroup -Filter *
Get-ADGroupMember -Identity "NomDuGroupe"
```

### Get-ADDomainController

Récupère les contrôleurs de domaine :

```powershell
Get-ADDomainController -Filter *
```

## Technologies utilisées

| Technologie | Utilisation |
|------------|-------------|
| **Python 3** | Langage principal |
| **Paramiko** | Bibliothèque SSH |
| **PowerShell** | Interrogation AD |
| **Active Directory** | Source de données |
