# Utilisation

## Syntaxe de base

```bash
python main.py --host <IP> --username <USER> --password <PASS> [OPTIONS]
```

**Exemple :**
```bash
python main.py --host 192.148.141.37 --username Administrateur --password MdpTahCompliquer --users
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
| `--oJ` | - | Output in JSON |
| `--oC` | - | Output in CSV |

## Exemples par fonctionnalité

### Utilisateurs

**Lister tous les utilisateurs :**
```bash
python main.py --host <IP> --username <USER> --password <PASS> --users
```

**Uniquement les utilisateurs désactivés :**
```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --disabled
```

!!! tip "Conseil"
    Utilisez cette option pour auditer les comptes désactivés qui devraient peut-être être supprimés.

**Uniquement les utilisateurs expirés :**
```bash
python main.py --host <IP> --username <USER> --password <PASS> --users --expired
```

**Sortie exemple :**
```text
ID | Username  | Firstname | Lastname | Groups    | Last login  | Disabled | Expired
---|-----------|-----------|----------|-----------|-------------|----------|--------
1  | john.doe  | john      | doe      | employees | 10/05 15h03 | Yes      | Yes
2  | bob.clark | bob       | clark    | employees | 01/12 02h28 | No       | No
```

### Ordinateurs

```bash
python main.py --host <IP> --username <USER> --password <PASS> --computers
```

**Sortie exemple :**
```text
ID | Hostname | Groups
---|----------|-------
1  | PC-ROOM1 | school
2  | PC-ROOM2 | school
```

### Groupes

```bash
python main.py --host <IP> --username <USER> --password <PASS> --groups
```

**Sortie exemple :**
```text
ID | Name      | Members
---|-----------|---------
1  | employees | john.doe, bob.clark
2  | admins    | administrator
```

### Contrôleurs de domaine

```bash
python main.py --host <IP> --username <USER> --password <PASS> --domain-controllers
```

!!! inf "Précision"
    Utilisez cette option pour générer un résultat en format Json ou CSV.

**Sortie exemple :**
```text
ID | Name | IP
---|------|--------------
1  | dc1  | 192.168.1.123
```

### Type de sortie Json/CSV

!!! info "Précision"
    Utilisez cette option pour générer un résultat au format Json ou CSV.

```bash
python main.py --host <IP> --username <USER> --password <PASS> --user --oJ
```

```bash
python main.py --host <IP> --username <USER> --password <PASS> --user --oC
```