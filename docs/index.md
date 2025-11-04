# RADAR

Un outil CLI Python pour interroger Active Directory via SSH et PowerShell.

## Présentation

RADAR permet d'interroger un Active Directory distant de manière sécurisée en se connectant à un serveur Windows via SSH et en exécutant des commandes PowerShell pour récupérer des informations sur :

- Utilisateurs (actifs, désactivés, expirés)
- Ordinateurs du domaine
- Groupes et leurs membres
- Contrôleurs de domaine

## Fonctionnalités principales

- Connexion SSH sécurisée vers un serveur Windows
- Interrogation Active Directory via PowerShell
- Affichage formaté des résultats sous forme de tableaux
- Filtres avancés pour les utilisateurs désactivés ou expirés
- Mode debug pour le dépannage

## Documentation

- **[Installation](installation.md)** - Guide complet d'installation de RADAR et configuration du serveur Windows
- **[Utilisation](usage.md)** - Exemples de commandes et options disponibles
- **[Fonctionnement](how-it-works.md)** - Architecture et détails techniques du projet
