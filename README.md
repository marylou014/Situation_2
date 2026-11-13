# Situation 2 – Plateforme de collecte des éléments de paie

Application web développée dans le cadre de mon BTS SIO SLAM. But créer une plateform web pour un cabinet comptable et gestionnaire de paie.
Elle permet aux entreprises clientes de saisir elles-mêmes, chaque mois, les éléments variables de leurs salariés (absences, congés, heures supplémentaires, primes…) afin que le gestionnaire de paie puisse établir les bulletins de salaire plus rapidement.

## Objectifs

- **Centraliser** les informations des salariés de toutes les entreprises du cabinet
- **Simplifier** la collecte des éléments de paie en fin de mois
- **Responsabiliser** les entreprises, qui saisissent leurs propres données
- **Conserver** l'historique de chaque mois pour chaque salarié

## Rôles

| Rôle | Droits principaux |
| --- | --- |
| Entreprise | Gérer ses salariés (créer, modifier, archiver) et saisir les informations du bulletin de chaque mois |
| Gestionnaire de paie | Consulter ses dossiers (entreprises), leurs salariés, les bulletins mois par mois et l'historique |

## Technologies

- PHP 
- MySQL / MariaDB
- HTML / CSS / JavaScript
- Docker (`docker-compose.yaml`)

## Architecture du projet

```
├── config/
│   ├── auth.php              # authentification et vérification des rôles
│   └── db.php                # connexion à la base de données (PDO)
│
├── includes/                 # parties communes des pages (header, footer)
│   ├── header.php            
│   ├── footer.php   
│
├── public/                   # racine web
│   ├── asset/
│   │   ├── css/
│   │   ├── img/
│   │   └── js/
│   │
│   ├── entreprise/           # espace entreprise
│   │   ├── homeEnt.php       # accueil entreprise
│   │   ├── salarier.php      # liste des salariés
│   │   ├── salarierForm.php  # création / modification d'un salarié
│   │   ├── archive.php       # archivage d'un salarié
│   │   ├── bulletin.php      # liste des bulletins (mois)
│   │   └── bulletinForm.php  # saisie des éléments du bulletin
│   │
│   ├── gestionnaire/         # espace gestionnaire de paie
│   │   ├── homeGes.php       # accueil gestionnaire
│   │   ├── dossiers.php      # liste des entreprises
│   │   ├── salarierInfo.php  # fiche complète d'un salarié
│   │   └── bulletinInfo.php  # consultation du bulletin par mois
│   │
│   ├── connexion.php
│   ├── déconnexions.php
│   └── index.php             # point d'entrée, redirection selon le rôle
│
├── docker-compose.yaml
└── README.md
```

## Règles de gestion

- Un salarié est rattaché à une seule entreprise
- Une entreprise ne voit et ne modifie que ses propres salariés
- Un gestionnaire ne consulte que les entreprises dont il a la charge
- CDD : date de fin obligatoire ; CDI : pas de date de fin
- Temps partiel : horaires de travail obligatoires
- N° de sécurité sociale : 15 chiffres
- Un seul dossier de bulletin par salarié et par mois
- Arrêt maladie : arrêt de travail joint obligatoire
- Indemnité kilométrique : carte grise et nombre de km obligatoires
- Les données de chaque mois sont conservées, jamais écrasées
- La suppression d'un salarié est un archivage (l'historique est conservé)


## Auteur

Marylou – BTS SIO SLAM, EPSI Montpellier