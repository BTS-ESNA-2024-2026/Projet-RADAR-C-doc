# Utilisation

## Syntaxe de base

```bash
python main.py --host <IP> --username <USER> --password <PASS> [OPTIONS]
```

**Exemple :**

```bash
python main.py --host 192.168.1.37 --username Administrateur --password MotDePasse123 --users
```

## Options disponibles

| Option | Alias | Description |
|--------|-------|-------------|
| `--users` | `-u` | Lister tous les utilisateurs |
| `--computers` | `-c` | Lister tous les ordinateurs |
| `--groups` | `-g` | Lister tous les groupes |
| `--domain-controllers` | `-d` | Lister tous les contrôleurs de domaine |
| `--disabled` | - | Filtrer uniquement les utilisateurs désactivés (avec `--users`) |
| `--expired` | - | Filtrer uniquement les utilisateurs expirés (avec `--users`) |
| `--debug` | - | Activer le mode debug |
| `--oJ` | - | Sortie au format JSON |
| `--oC` | - | Sortie au format CSV |

## Exemples par fonctionnalité

### Utilisateurs

#### Lister tous les utilisateurs

```bash
python main.py --host <IP> --username <USER> --password <PASS> --users
# ou
python main.py --host <IP> --username <USER> --password <PASS> -u
```

**Sortie exemple :**

```text
ID | Username  | Firstname | Lastname | Groups    | Last login  | Disabled | Expired
---|-----------|-----------|----------|-----------|-------------|----------|--------
1  | john.doe  | john      | doe      | employees | 10/05 15h03 | Yes      | Yes
2  | bob.clark | bob       | clark    | employees | 01/12 02h28 | No       | No
```

#### Lister uniquement les utilisateurs désactivés

```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --disabled
```

**Sortie exemple :**

```text
ID | Username  | Firstname | Lastname | Groups    | Last login  | Disabled | Expired
---|-----------|-----------|----------|-----------|-------------|----------|--------
1  | john.doe  | john      | doe      | employees | 10/05 15h03 | Yes      | Yes
```

> **Astuce :** Utilisez cette option pour auditer les comptes désactivés qui devraient peut-être être supprimés.

#### Lister uniquement les utilisateurs expirés

```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --expired
```

**Sortie exemple :**

```text
ID | Username  | Firstname | Lastname | Groups    | Last login  | Disabled | Expired
---|-----------|-----------|----------|-----------|-------------|----------|--------
1  | john.doe  | john      | doe      | employees | 10/05 15h03 | Yes      | Yes
```

### Ordinateurs

#### Lister tous les ordinateurs de l'Active Directory

```bash
python main.py --host <IP> --username <USER> --password <PASS> --computers
# ou
python main.py --host <IP> --username <USER> --password <PASS> -c
```

**Sortie exemple :**

```text
ID | Hostname | Groups
---|----------|-------
1  | PC-ROOM1 | school
2  | PC-ROOM2 | school
```

### Groupes

#### Lister tous les groupes et leurs membres

```bash
python main.py --host <IP> --username <USER> --password <PASS> --groups
# ou
python main.py --host <IP> --username <USER> --password <PASS> -g
```

**Sortie exemple :**

```text
ID | Name      | Members
---|-----------|---------
1  | employees | john.doe, bob.clark
2  | admins    | administrator
```

### Contrôleurs de domaine

#### Lister tous les contrôleurs de domaine

```bash
python main.py --host <IP> --username <USER> --password <PASS> --domain-controllers
# ou
python main.py --host <IP> --username <USER> --password <PASS> -d
```

**Sortie exemple :**

```text
ID | Name | IP
---|------|--------------
1  | dc1  | 192.168.1.123
```

### Format de sortie

#### Export au format JSON

```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --oJ
```

#### Export au format CSV

```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --oC
```

> **Note :** Les options `--oJ` et `--oC` peuvent être utilisées avec toutes les commandes de listage (utilisateurs, ordinateurs, groupes, contrôleurs de domaine).

### Mode debug

Pour activer le mode debug et obtenir plus d'informations sur l'exécution :

```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --debug
```
