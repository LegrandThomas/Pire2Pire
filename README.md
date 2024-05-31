# Pire2Pire

![image pire2pire](https://github.com/LegrandThomas/Pire2Pire/blob/main/assets/img/pire2pire_img.webp)

## Table des matières

1. [Le projet](#Le-Projet)
2. [Contexte du projet](#Contexte-du-projet)
3. [Régles de gestion](#Régles-de-gestion)
4. [Dictionnaire de données](#Dictionnaire-de-données)
5. [MCD / MLD](#mcd--mld)
6. [régles de cardinalités](#régles-de-cardinalités)
7. [MPD textuel](#Mpd-textuel)
8. [script BDD](#Script-BDD)

## Le Projet:

<details>
   <summary>pire2pire.com : Conception BDD avec MERISE</summary>
    Votre mission est de concevoir la base de données d’une plateforme de formation en ligne nommée pire2pire.com à l'aide de la méthode MERISE.
 </details>

<details>
   <summary>MERISE </summary>
   « Méthode d'Étude et de Réalisation Informatique par les Sous-Ensembles pour les Systèmes d'Entreprises »
 </details>

 ## Contexte du projet:
  
  <details>
      <summary>contexte</summary>
      Les formations sont organisés en modules.

​

Chaque module est caractérisé par un numéro de module sous forme de Semantic Versionning, un intitulé, un objectif pédagogique, un contenu (textes, images et vidéos), une durée en heures, un ou plusieurs tags et un auteur.

​

Un module peut faire partie d'une ou plusieurs formations, comme par exemple un pire module "Commandes de base Git" pourrait faire partie d'une pire formation "Frontend Javascript" et "DevOps", voir  plus.

​

Une lecçon peut contenir un texte et/ou une image et/ou une vidéo.

​

​

Les apprenants peuvent s'inscrire à une ou plusieurs formations, ils peuvent choisir de ne pas suivre certains des modules s'ils possèdent déjà, par exemple, les compétences. Autrement dit, ils peuvent arbitrairement valider les modules de leur choix en un clic.

​

Chaque apprenant est évalué pour chaque module et possède un état de fin de module (OK / KO).

​

Une formation est considérée comme terminée lorsque tous les modules ont été validés.

​

Chaque apprenant est caractérisé par un numéro d’inscription unique, un nom, un prénom, une adresse et une date de naissance.

​

Un formateurs est auteur d'un module pour une formation donnée, chaque formateur est caractérisé par un code, un nom, un prénom.

​

  </details>

   ## Régles de gestion:
  
  <details>
      <summary>Régles de gestion</summary>
     Entités et Règles de Gestion


Vue d'ensemble des entités

    Visitors (uniquement pour les régles de gestions)
    Users
    Roles 
    Statuses 
    Tags 
    Adress
    Formations
    Modules
    Lessons
    Contents
    Compose
    Follow
    To Tag
    Validate
    Study



Visitors

    Règles de gestion :
        Peut consulter et naviguer sur l’application.
        Peut s’inscrire et créer son compte en fournissant les informations nécessaires à l’inscription.
        Devient apprenant suite à l'inscription.

users:
    Un user à 1 et 1 seul rôle qui déterminera les ses autorisations

     Attribut particuliers :
        Identification_code : code d'identification commençant par un lettre  associé à un rôle puis des chiffres, doit etre unique afin que chaque apprenant, formateur ou administrateur aient un code d'identification unique.
        exemple pour un 'student' : S051, un 'trainer' : T421, un administrator : A121

  user avec le role d'apprenant (student)

    Règles de gestion :
        Peut consulter et naviguer sur l’application.
        Peut s’identifier sur l’application en renseignant ses informations de connexion.
        Peut modifier ses informations de profil.
        Peut se désinscrire (désactivation) et/ou supprimer son compte.
        Peut utiliser son droit d’accès, de rectification ou suppression des données.
        Peut rechercher zéro ou plusieurs modules par leur nom, tag, etc.
        Peut consulter zéro ou plusieurs formations.
        Peut s’inscrire ou suivre zéro ou plusieurs formations.
        Ne peut souscrire à une formation que s’il ne la suit pas déjà.
        Peut suivre zéro ou plusieurs modules d’une formation.
        Peut suivre zéro ou plusieurs leçons d’un module.
        Peut avoir zéro ou plusieurs leçons validées.
        Peut s’auto-valider zéro ou plusieurs leçons.
        Peut avoir zéro ou plusieurs modules validés.
        Peut avoir zéro ou plusieurs formations validées.
        Peut suivre sa progression pour une formation, un module, y compris les leçons validées.

user avec le role formateurs (trainer)

    Règles de gestion :
        Peut consulter et naviguer sur l’application.
        Peut s’identifier sur l’application en renseignant ses informations de connexion.
        Peut modifier ses informations de profil.
        Peut utiliser son droit d’accès, de rectification ou suppression des données.
        Peut rechercher zéro ou plusieurs modules par leur nom, tag, etc.
        Peut consulter zéro ou plusieurs formations.
        Peut créer zéro ou plusieurs formations.
        Peut changer le statut de zéro ou plusieurs de ses formations (crées par lui), en brouillon, en ligne ou retirée.
        Peut modifier zéro ou plusieurs de ses formations (crées par lui), nom, description, contenu, etc.
        Peut être auteur de zéro ou plusieurs modules.
        Peut être auteur de zéro ou plusieurs leçons.
        Peut créer, modifier, supprimer un tag.

user avec le role administrateur (administrateur)

    Règles de gestion :
        Peut modifier le role d'un user.
Roles

    Règles de gestion :
        Doit avoir un id unique un nom unique
        Le code_role_prefix doit être unique est composé d'une lettre

Adress

    Règles de gestion :
        Doit avoir un id unique et un pseudo unique.


Formations

    Règles de gestion :
        Doit avoir un nom unique et un numéro de formation unique.
        Doit avoir un et un seul statut (en ligne, brouillon, retirée).
        Est constituée de zéro ou plusieurs modules.
        Une formation au statut 'en ligne' doit comporter au moins un module au statut 'en ligne'.
        Est suivie par zéro ou plusieurs apprenants.
        Peut être validée par zéro ou plusieurs apprenants.

Modules

   
    Règles de gestion :
        Doit avoir un nom unique et un numéro de module unique.
        Doit avoir un et un seul statut (en ligne, brouillon, retirée).
        Est constitué de zéro ou plusieurs leçons.
        Un module au statut 'en ligne' doit être constitué d’une à plusieurs leçons aux statuts 'en ligne'.
        Peut être dans zéro ou plusieurs formations.
        Peut être suivi par zéro ou plusieurs apprenants.
        Peut être validé par zéro ou plusieurs apprenants.

Leçons


    Règles de gestion :
        Doit avoir un nom unique et un numéro de leçon unique.
        Doit avoir un et un seul statut (en ligne, brouillon, retirée).
        Peut avoir zéro ou un contenu

Statuses

    Règles de gestion :
        Doit avoir un nom unique et un numéro de statuts unique.

Tags
  
    Règles de gestion :
        Doit avoir un nom unique et un numéro de tags unique.

contents

     Règles de gestion :
        Doit avoir un numéro de contenu unique.
        Le text_name doit être unique.
        Le img_name doit être unique.
        Le video_name doit être unique.


Règles de Gestion Complètes
Utilisateurs

    Un utilisateur doit avoir un rôle unique parmi Apprenant, Formateur, et Administrateur.
    Un utilisateur doit avoir une adresse e-mail unique.
    Un utilisateur peut s'identifier sur l'application en renseignant ses informations de connexion.
    Un utilisateur peut modifier ses informations de profil.
    Un utilisateur peut se désinscrire et/ou supprimer son profil.
    Un utilisateur peut utiliser son droit d’accès, de rectification ou suppression des données.

Apprenants

    Un apprenant doit avoir un numéro d’apprenant unique.
    Un apprenant peut consulter et naviguer sur l’application.
    Un apprenant peut rechercher zéro ou plusieurs formations par leur nom, tag, etc.
    Un apprenant peut consulter zéro ou plusieurs formations.
    Un apprenant peut s’inscrire ou suivre zéro ou plusieurs formations.
    Un apprenant ne peut souscrire à une formation que s’il ne la suit pas déjà.
    Un apprenant peut suivre zéro ou plusieurs modules d’une formation.
    Un apprenant peut suivre zéro ou plusieurs leçons d’un module.
    Un apprenant peut avoir zéro ou plusieurs leçons validées.
    Un apprenant peut s’auto-valider zéro ou plusieurs leçons.
    Un apprenant peut avoir zéro ou plusieurs modules validés.
    Un apprenant peut avoir zéro ou plusieurs formations validées.
    Un apprenant peut suivre sa progression pour une formation, un module, y compris les leçons validées.

Formateurs

    Un formateur doit avoir un numéro de formateur unique.
    Un formateur peut rechercher zéro ou plusieurs formations par leur nom, tag, etc.
    Un formateur peut consulter zéro ou plusieurs formations.
    Un formateur peut créer zéro ou plusieurs formations.
    Un formateur peut changer le statut de zéro ou plusieurs de ses formations (crées par lui) en brouillon, en ligne ou retirée.
    Un formateur peut modifier zéro ou plusieurs de ses formations (crées par lui), nom, description, contenu, etc.
    Un formateur peut être auteur de zéro ou plusieurs modules.
    Un formateur peut être auteur de zéro ou plusieurs leçons.
    Un formateur peut créer, modifier, supprimer un tag.

Administrateurs


    Un administrateur peut attribuer et révoquer des rôles utilisateurs.
 

Formations

    Une formation doit avoir un nom unique et un numéro de formation unique.
    Une formation doit avoir un et un seul statut (en ligne, brouillon, retirée).
    Une formation est constituée de zéro ou plusieurs modules.
    Une formation au statut 'en ligne' doit comporter au moins un module au statut 'en ligne'.
    Une formation est suivie par zéro ou plusieurs apprenants.
    Une formation peut être validée par zéro ou plusieurs apprenants.

Modules

    Un module doit avoir un nom unique et un numéro de module unique.
    Un module doit avoir un et un seul statut (en ligne, brouillon, retirée).
    Un module a un ou plusieurs auteurs (formateurs).
    Un module est constitué de zéro ou plusieurs leçons.
    Un module au statut 'en ligne' doit être constitué d’une à plusieurs leçons aux statuts 'en ligne'.
    Un module peut être dans zéro ou plusieurs formations.
    Un module peut être suivi par zéro ou plusieurs apprenants.
    Un module peut être validé par zéro ou plusieurs apprenants.

Leçons

    Une leçon doit avoir un nom unique et un numéro de leçon unique.
    Une leçon doit avoir un et un seul statut (en ligne, brouillon, retirée).
    Une leçon a un ou plusieurs auteurs (formateurs).
    Une leçon doit avoir un texte et une vidéo.
    Une leçon peut avoir une ou plusieurs images.
    Une leçon doit avoir un ou plusieurs tags.

Statuts

    Un statut doit avoir un nom unique.

Tags

    Un tag doit avoir un nom unique.



​

  </details>
  
  ## Dictionnaire de données:
  
  <details>
      <summary>Dictionnaire de données</summary>

### Table : roles

| Attribut            | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|---------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_roles            | SERIAL        | -        | PRIMARY KEY     | Identifiant du rôle  | 123                                   |
| name                | VARCHAR(50)   | 50       | NOT NULL, UNIQUE| Nom du rôle          | Formateur                             |
| role_code_prefix    | VARCHAR(1)    | 1        | NOT NULL, UNIQUE| Préfixe du code du rôle | F                                   |
| created_at          | DATE          | -        | NOT NULL        | Date de création du rôle | 2024-05-28                          |
| updated_at          | DATE          | -        | NOT NULL        | Date de mise à jour du rôle | 2024-05-28                         |

### Table : statuses
| Attribut            | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|---------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_statuses         | SERIAL        | -        | PRIMARY KEY     | Identifiant du statut | 456                                  |
| name                | VARCHAR(50)   | 50       | NOT NULL, UNIQUE| Nom du statut       | En cours                              |
| created_at          | DATE          | -        | NOT NULL        | Date de création du statut | 2024-05-28                         |
| updated_at          | DATE          | -        | NOT NULL        | Date de mise à jour du statut | 2024-05-28                        |

### Table : tags
| Attribut            | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|---------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_tags             | SERIAL        | -        | PRIMARY KEY     | Identifiant du tag   | 789                                   |
| name                | VARCHAR(100)  | 100      | NOT NULL, UNIQUE| Nom du tag           | Informatique                          |
| created_at          | DATE          | -        | NOT NULL        | Date de création du tag | 2024-05-28                         |
| updated_at          | DATE          | -        | NOT NULL        | Date de mise à jour du tag | 2024-05-28                        |

### Table : users
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_users              | UUID          | 36       | PRIMARY KEY     | Identifiant de l'utilisateur | a3b3f0a6-7c35-4b57-bf69-57c46d48f1d2 |
| email                 | VARCHAR(255)  | 255      | NOT NULL, UNIQUE| Adresse email de l'utilisateur | example@example.com               |
| password              | VARCHAR(255)  | 255      | NOT NULL        | Mot de passe de l'utilisateur | $2y$10$CEAwANbAtAD20iTeu5M43.ohvYT4L7tyfDu7VgiYO4Wq5TcaiLADC                            |
| is_active             | BOOLEAN       | -        | NOT NULL        | Statut d'activation de l'utilisateur | true                          |
| identification_code   | VARCHAR(50)   | 50       | NOT NULL, UNIQUE| Code d'identification de l'utilisateur | ABC123  
| first_name            | VARCHAR(255)  | 255      | NOT NULL        | Prénom               | John                                  |
| last_name             | VARCHAR(255)  | 255      | NOT NULL        | Nom                  | Doe                                   |
| pseudo                | VARCHAR(255)  | 255      | NOT NULL, UNIQUE| Pseudo               | johndoe                               |
| birthdate             | DATE          | -        | NOT NULL        | Date de naissance    | 1990-01-01                            |                         |
| created_at            | DATE          | -        | NOT NULL        | Date de création de l'utilisateur | 2024-05-28                        |
| updated_at            | DATE          | -        | NOT NULL        | Date de mise à jour de l'utilisateur| 2024-05-28                       |

**Foreign Key Constraints:**
- `id_users_1` REFERENCES `users(id_users)`
- `id_roles` REFERENCES `roles(id_roles)`

### Table : formations
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_formations         | SERIAL        | -        | PRIMARY KEY     | Identifiant de la formation | 987                                 |
| name                  | VARCHAR(100)  | 100      | NOT NULL, UNIQUE| Nom de la formation | Formation A                           |
| description           | VARCHAR(255)  | 255      |                 | Description de la formation | Description de la formation      |
| created_at            | DATE          | -        | NOT NULL        | Date de création de la formation | 2024-05-28                       |
| updated_at            | DATE          | -        | NOT NULL        | Date de mise à jour de la formation | 2024-05-28                      |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_statuses` REFERENCES `statuses(id_statuses)`

### Table : modules
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_modules            | SERIAL        | -        | PRIMARY KEY     | Identifiant du module | 654                                 |
| name                  | VARCHAR(100)  | 100      | NOT NULL, UNIQUE| Nom du module        | Module A                              |
| description           | VARCHAR(50)   | 50       |                 | Description du module | Description du module                 |
| objectif              | VARCHAR(50)   | 50       |                 | Objectif du module   | Objectif du module                    |
| duration              | TIME          | -        |                 | Durée du module      | 02:30:00                              |
| version               | VARCHAR(10)   | 10       |                 | Version du module    | 1.0                                   |
| created_at            | DATE          | -        | NOT NULL        | Date de création du module | 2024-05-28                       |
| updated_at            | DATE          | -        | NOT NULL        | Date de mise à jour du module | 2024-05-28                      |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_statuses` REFERENCES `statuses(id_statuses)`

### Table : lessons
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_lessons            | SERIAL        | -        | PRIMARY KEY     | Identifiant de la leçon | 321                               |
| name                  | VARCHAR(100)  | 100      | NOT NULL, UNIQUE| Nom de la leçon     | Leçon A                               |
| description           | VARCHAR(255)  | 255      |                 | Description de la leçon | Description de la leçon             |
| created_at            | DATE          | -        | NOT NULL        | Date de création de la leçon | 2024-05-28                      |
| updated_at            | DATE          | -        | NOT NULL        | Date de mise à jour de la leçon | 2024-05-28                     |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_statuses` REFERENCES `statuses(id_statuses)`
- `id_modules` REFERENCES `modules(id_modules)`

### Table : contents
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_contents           | SERIAL        | -        | PRIMARY KEY     | Identifiant du contenu | 111                               |
| name_text             | VARCHAR(50)   | 50       | UNIQUE          | Nom du texte         | Texte_A                               |
| text                  | VARCHAR(255)  | 255      |                 | Texte                | "Contenu du texte"                    |
| name_img              | VARCHAR(50)   | 50       | UNIQUE          | Nom de l'image       | Image_A                               |
| img_url               | VARCHAR(50)   | 50       |                 | URL de l'image       | "http://exemple.com/image.jpg"       |
| name_video            | VARCHAR(50)   | 50       | UNIQUE          | Nom de la vidéo      | Video_A                               |
| video_url             | VARCHAR(50)   | 50       |                 | URL de la vidéo      | "http://exemple.com/video.mp4"       |
| created_at            | DATE          | -        | NOT NULL        | Date de création du contenu | 2024-05-28                       |
| updated_at            | DATE          | -        | NOT NULL        | Date de mise à jour du contenu | 2024-05-28                      |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_lessons` REFERENCES `lessons(id_lessons)`

### Table : adress
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_adress           | SERIAL        | -        | PRIMARY KEY     | Identifiant du profil | 999                               |
| house_number_or_building | INTEGER    | -        | NOT NULL        | Numéro de maison ou de bâtiment | 123 |
| street                | VARCHAR(100)  | 100      | NOT NULL        | Rue                  | Main Street                           |
| city                  | VARCHAR(50)   | 50       | NOT NULL        | Ville                | Anytown                               |
| zip_code              | VARCHAR(50)   | 50       | NOT NULL        | Code postal          | 12345                                 |
| adress_line2          | VARCHAR(50)   | 50       |                 | Ligne d'adresse 2    | (facultatif)                          |
| country               | VARCHAR(50)   | 50       | NOT NULL        | Pays                 | Country X                             |
| created_at            | DATE          | -        | NOT NULL        | Date de création du profil | 2024-05-28                       |
| updated_at            | DATE          | -        | NOT NULL        | Date de mise à jour du profil | 2024-05-28                      |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`

### Table : compose
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_formations         | INTEGER       | -        | PRIMARY KEY     | Identifiant 
de la formation | 419                               |
| id_modules            | INTEGER       | -        | PRIMARY KEY     | Identifiant 
du module | 123                               |

**Foreign Key Constraints:**
- `id_formations` REFERENCES `formations(id_formations)`
- `id_modules` REFERENCES `modules(id_modules)`

### Table : follow
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_users              | UUID          | 36       | PRIMARY KEY     | Identifiant de l'utilisateur | a3b3f0a6-7c35-4b57-bf69-57c46d48f1d2 |
| id_formations         | INTEGER       | -        | PRIMARY KEY     | Identifiant de la formation suivie | 987                               |
| start_date            | DATE          | -        |                 | Date de début de la formation | 2024-05-28                      |
| end_date              | DATE          | -        |                 | Date de fin de la formation | 2024-06-28                        |
| is_finished           | BOOLEAN       | -        | NOT NULL        | Statut de fin de la formation | true                            |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_formations` REFERENCES `formations(id_formations)`

### Table : to_tag
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_modules            | INTEGER       | -        | PRIMARY KEY     | Identifiant du module | 123                               |
| id_tags               | INTEGER       | -        | PRIMARY KEY     | Identifiant du tag   | 456                               |

**Foreign Key Constraints:**
- `id_modules` REFERENCES `modules(id_modules)`
- `id_tags` REFERENCES `tags(id_tags)`

### Table : validate
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_users              | UUID          | 36       | PRIMARY KEY     | Identifiant de l'utilisateur | a3b3f0a6-7c35-4b57-bf69-57c46d48f1d2 |
| id_modules            | INTEGER       | -        | PRIMARY KEY     | Identifiant du module | 654                               |
| validate_date         | DATE          | -        | NOT NULL        | Date de validation du module | 2024-05-28                        |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_modules` REFERENCES `modules(id_modules)`

### Table : study
| Attribut              | Type          | Longueur | Contraintes      | Description          | Exemple                                |
|-----------------------|---------------|----------|-----------------|----------------------|---------------------------------------|
| id_users              | UUID          | 36       | PRIMARY KEY     | Identifiant de l'utilisateur | a3b3f0a6-7c35-4b57-bf69-57c46d48f1d2 |
| id_lessons            | INTEGER       | -        | PRIMARY KEY     | Identifiant de la leçon | 321                               |
| validation_date       | DATE          | -        |                 | Date de validation de la leçon | 2024-05-28                      |

**Foreign Key Constraints:**
- `id_users` REFERENCES `users(id_users)`
- `id_lessons` REFERENCES `lessons(id_lessons)`

​

  </details>
  

## MCD / MLD
<details>
      <summary>MCD</summary>

![image pire2pire](https://github.com/LegrandThomas/Pire2Pire/blob/main/assets/img/p2pmcd.png)

</details>    

<details>
      <summary>MLD</summary>

![image pire2pire](https://github.com/LegrandThomas/Pire2Pire/blob/main/assets/img/p2pmld.png)

</details>    

## régles de cardinalités

<details>
      <summary>justifications des cardinalités</summary>

Users et Roles

    1 user a 1 et 1 seul rôle : Lors de l'inscription, est attribué un rôle unique (apprenant par défaut).
    1 rôle est affecté à 0 ou plusieurs users : Un rôle peut être attribué à plusieurs utilisateurs, mais il peut aussi ne pas être attribué du tout.

Users et Profiles

    1 user a 0 ou 1 seul profil : Permet de créer rapidement un utilisateur en base de données sans avoir à renseigner un profil complet.
    1 profil appartient à 1 et 1 seul user : Chaque profil est associé à un seul utilisateur.

Users et Administrateurs

    1 user (s'il a le rôle 'administrator') peut changer le rôle de zéro ou plusieurs users : Un administrateur peut modifier les rôles d'autres utilisateurs.
    1 rôle user peut être changé par 0 ou plusieurs users (ayant le rôle 'administrator') : Les utilisateurs ayant le rôle d'administrateur peuvent modifier les rôles des utilisateurs.

Users et Contenus

    1 user (s'il a le rôle 'trainer') peut générer/modifier zéro ou plusieurs contenus : Un formateur peut créer ou modifier plusieurs contenus.
    1 contenu est généré/modifié par zéro ou 1 seul user (ayant le rôle 'trainer') : Chaque contenu est associé à un formateur qui le crée ou le modifie.

Users et Leçons

    1 user (s'il a le rôle 'trainer') peut générer/modifier zéro ou plusieurs leçons : Un formateur peut créer ou modifier plusieurs leçons.
    1 leçon est générée/modifiée par zéro ou 1 seul user (ayant le rôle 'trainer') : Chaque leçon est associée à un formateur qui la crée ou la modifie.

Users et Modules

    1 user (s'il a le rôle 'trainer') peut générer/modifier zéro ou plusieurs modules : Un formateur peut créer ou modifier plusieurs modules.
    1 module est généré/modifié par zéro ou 1 seul user (ayant le rôle 'trainer') : Chaque module est associé à un formateur qui le crée ou le modifie.

Users et Formations

    1 user (s'il a le rôle 'trainer') peut générer/modifier zéro ou plusieurs formations : Un formateur peut créer ou modifier plusieurs formations.
    1 formation est générée/modifiée par zéro ou 1 seul user (ayant le rôle 'trainer') : Chaque formation est associée à un formateur qui la crée ou la modifie.

Users et Formations (Suivi)

    1 user (s'il a le rôle 'student') peut suivre zéro ou plusieurs formations : Un étudiant peut suivre plusieurs formations. On sauvegardera sa date de début, de fin, et l'état de validation de la formation (is_finished boolean).
    1 formation est suivie par 0 ou plusieurs users (ayant le rôle 'student') : Une formation peut être suivie par plusieurs étudiants.

Users et Modules (Validation)

    1 user (s'il a le rôle 'student') peut valider zéro ou plusieurs modules : Un étudiant peut valider plusieurs modules. On sauvegarde la date de validation du module pour cet utilisateur.
    1 module peut être suivi par 0 ou plusieurs users (ayant le rôle 'student') : Un module peut être suivi par plusieurs étudiants.

Users et Leçons (Validation)

    1 user (s'il a le rôle 'student') peut suivre et valider zéro ou plusieurs leçons : Un étudiant peut suivre et valider plusieurs leçons. On sauvegarde la date de validation de la leçon pour cet utilisateur.
    1 leçon peut être étudiée/validée par 0 ou plusieurs users (ayant le rôle 'student') : Une leçon peut être étudiée et validée par plusieurs étudiants.

Formations et Modules

    1 formation est composée de 0 ou plusieurs modules : Une formation peut contenir plusieurs modules.
    Un module peut être dans 0 ou plusieurs formations : Un module peut être utilisé dans plusieurs formations.

Modules et Leçons

    1 module est constitué de 0 ou plusieurs leçons : Un module peut contenir plusieurs leçons.
    1 leçon peut être dans 0 ou 1 module : Chaque leçon appartient à un seul module ou n'appartient à aucun module.

Leçons et Contenus

    1 leçon comprend 0 ou un contenu : Une leçon peut avoir un contenu associé ou ne pas en avoir.
    1 contenu se trouve dans 0 ou 1 leçon : Un contenu est associé à une leçon ou n'est pas associé.

Modules et Tags

    1 module a 1 ou plusieurs tags : Un module doit avoir au moins un tag.
    1 tag est associé à 0 ou plusieurs modules : Un tag peut être utilisé pour plusieurs modules.

Formations et Statuts

    1 formation a 1 et 1 seul statut : Chaque formation a un seul statut (en ligne, brouillon, retirée).
    1 statut est associé à 0 ou plusieurs formations : Un statut peut être appliqué à plusieurs formations.

Modules et Statuts

    1 module a 1 et 1 seul statut : Chaque module a un seul statut (en ligne, brouillon, retirée).
    1 statut est associé à 0 ou plusieurs modules : Un statut peut être appliqué à plusieurs modules.

Leçons et Statuts

    1 leçon a 1 et 1 seul statut : Chaque leçon a un seul statut (en ligne, brouillon, retirée).
    1 statut est associé à 0 ou plusieurs leçons : Un statut peut être appliqué à plusieurs leçons.

Statuts

    1 statut doit avoir un nom unique : Chaque statut a un nom unique.
    1 statut est associé à 0 ou plusieurs entités : Un statut peut être utilisé pour plusieurs formations, modules ou leçons.

Tags

    1 tag doit avoir un nom unique : Chaque tag a un nom unique.
    1 tag est associé à 0 ou plusieurs modules : Un tag peut être utilisé pour plusieurs modules.

</details>   

## MPD textuel

<details>
      <summary>MPD textuel</summary>
roles = (id_roles INT AUTO_INCREMENT, name VARCHAR(50) , role_code_prefix VARCHAR(1) , created_at DATE, updated_at DATE);

statuses = (id_statuses INT AUTO_INCREMENT, name VARCHAR(50) , created_at DATE, updated_at DATE);

tags = (id_tags INT AUTO_INCREMENT, name VARCHAR(100) , created_at DATE, updated_at DATE);

users = (id_users UUID, first_name VARCHAR(255) , last_name VARCHAR(255) , email VARCHAR(255) , password VARCHAR(255) , pseudo VARCHAR(255) , birthdate DATE, is_active BOOLEAN, identification_code VARCHAR(50) , created_at DATE, updated_at DATE, #id_users_1*, #id_roles);

formations = (id_formations INT AUTO_INCREMENT, name VARCHAR(100) , description VARCHAR(255) , created_at DATE, updated_at DATE, #id_users, #id_users_1, #id_statuses);

modules = (id_modules INT AUTO_INCREMENT, name VARCHAR(100) , description VARCHAR(50) , objectif VARCHAR(50) , duration TIME, version VARCHAR(10) , created_at DATE, updated_at DATE, #id_users, #id_users_1, #id_statuses);

lessons = (id_lessons INT AUTO_INCREMENT, name VARCHAR(100) , description VARCHAR(255) , created_at DATE, updated_at DATE, #id_users, #id_statuses, #id_modules*);

contents = (id_contents INT AUTO_INCREMENT, name_text VARCHAR(50) , text VARCHAR(255) , name_img VARCHAR(50) , img_url VARCHAR(50) , name_video VARCHAR(50) , video_url VARCHAR(50) , created_at DATE, updated_at DATE, #id_users, #id_users_1, #id_lessons*);

adress = (id_profiles INT AUTO_INCREMENT, house_number_or_building INT, street VARCHAR(100) , city VARCHAR(50) , zip_code VARCHAR(50) , adress_line2 VARCHAR(50) , country VARCHAR(50) , created_at DATE, updated_at DATE, #id_users);

compose = (#id_formations, #id_modules);
follow = (#id_users, #id_formations, start_date DATE, end_date DATE, is_finished BOOLEAN);

to_tag = (#id_modules, #id_tags);

validate = (#id_users, #id_modules, validate_date DATE);

study = (#id_users, #id_lessons, validation_date DATE);

revise = (#id_users, #id_lessons);




</details>   

## script BDD

<details>
      <summary>script BDD</summary>


CREATE TABLE roles(
   id_roles INT AUTO_INCREMENT,
   name VARCHAR(50)  NOT NULL,
   role_code_prefix VARCHAR(1)  NOT NULL,
   created_at NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   PRIMARY KEY(id_roles),
   UNIQUE(name),
   UNIQUE(role_code_prefix)
);

CREATE TABLE statuses(
   id_statuses INT AUTO_INCREMENT,
   name VARCHAR(50)  NOT NULL,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   PRIMARY KEY(id_statuses),
   UNIQUE(name)
);

CREATE TABLE tags(
   id_tags INT AUTO_INCREMENT,
   name VARCHAR(100)  NOT NULL,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   PRIMARY KEY(id_tags),
   UNIQUE(name)
);

CREATE TABLE users(
   id_users UUID,
   first_name VARCHAR(255)  NOT NULL,
   last_name VARCHAR(255)  NOT NULL,
   email VARCHAR(255)  NOT NULL,
   password VARCHAR(255)  NOT NULL,
   pseudo VARCHAR(255)  NOT NULL,
   birthdate DATE NOT NULL,
   is_active BOOLEAN NOT NULL,
   identification_code VARCHAR(50)  NOT NULL,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   id_users_1 UUID,
   id_roles INT NOT NULL,
   PRIMARY KEY(id_users),
   UNIQUE(email),
   UNIQUE(pseudo),
   UNIQUE(identification_code),
   FOREIGN KEY(id_users_1) REFERENCES users(id_users),
   FOREIGN KEY(id_roles) REFERENCES roles(id_roles)
);

CREATE TABLE formations(
   id_formations INT AUTO_INCREMENT,
   name VARCHAR(100)  NOT NULL,
   description VARCHAR(255) ,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   id_users UUID NOT NULL,
   id_users_1 UUID NOT NULL,
   id_statuses INT NOT NULL,
   PRIMARY KEY(id_formations),
   UNIQUE(name),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_users_1) REFERENCES users(id_users),
   FOREIGN KEY(id_statuses) REFERENCES statuses(id_statuses)
);

CREATE TABLE modules(
   id_modules INT AUTO_INCREMENT,
   name VARCHAR(100)  NOT NULL,
   description VARCHAR(50) ,
   objectif VARCHAR(50) ,
   duration TIME,
   version VARCHAR(10) ,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   id_users UUID NOT NULL,
   id_users_1 UUID NOT NULL,
   id_statuses INT NOT NULL,
   PRIMARY KEY(id_modules),
   UNIQUE(name),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_users_1) REFERENCES users(id_users),
   FOREIGN KEY(id_statuses) REFERENCES statuses(id_statuses)
);

CREATE TABLE lessons(
   id_lessons INT AUTO_INCREMENT,
   name VARCHAR(100)  NOT NULL,
   description VARCHAR(255) ,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   id_users UUID NOT NULL,
   id_statuses INT NOT NULL,
   id_modules INT,
   PRIMARY KEY(id_lessons),
   UNIQUE(name),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_statuses) REFERENCES statuses(id_statuses),
   FOREIGN KEY(id_modules) REFERENCES modules(id_modules)
);

CREATE TABLE contents(
   id_contents INT AUTO_INCREMENT,
   name_text VARCHAR(50) ,
   text VARCHAR(255) ,
   name_img VARCHAR(50) ,
   img_url VARCHAR(50) ,
   name_video VARCHAR(50) ,
   video_url VARCHAR(50) ,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   id_users UUID NOT NULL,
   id_users_1 UUID NOT NULL,
   id_lessons INT,
   PRIMARY KEY(id_contents),
   UNIQUE(id_lessons),
   UNIQUE(name_text),
   UNIQUE(name_img),
   UNIQUE(name_video),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_users_1) REFERENCES users(id_users),
   FOREIGN KEY(id_lessons) REFERENCES lessons(id_lessons)
);

CREATE TABLE adress(
   id_profiles INT AUTO_INCREMENT,
   house_number_or_building INT NOT NULL,
   street VARCHAR(100)  NOT NULL,
   city VARCHAR(50)  NOT NULL,
   zip_code VARCHAR(50)  NOT NULL,
   adress_line2 VARCHAR(50) ,
   country VARCHAR(50)  NOT NULL,
   created_at DATE NOT NULL DEFAULT CURRENT_DATE,
   updated_at DATE NOT NULL DEFAULT CURRENT_DATE,
   id_users UUID NOT NULL,
   PRIMARY KEY(id_profiles),
   UNIQUE(id_users),
   FOREIGN KEY(id_users) REFERENCES users(id_users)
);

CREATE TABLE compose(
   id_formations INT,
   id_modules INT,
   PRIMARY KEY(id_formations, id_modules),
   FOREIGN KEY(id_formations) REFERENCES formations(id_formations),
   FOREIGN KEY(id_modules) REFERENCES modules(id_modules)
);

CREATE TABLE follow(
   id_users UUID,
   id_formations INT,
   start_date DATE,
   end_date DATE,
   is_finished BOOLEAN NOT NULL,
   PRIMARY KEY(id_users, id_formations),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_formations) REFERENCES formations(id_formations)
);

CREATE TABLE to_tag(
   id_modules INT,
   id_tags INT,
   PRIMARY KEY(id_modules, id_tags),
   FOREIGN KEY(id_modules) REFERENCES modules(id_modules),
   FOREIGN KEY(id_tags) REFERENCES tags(id_tags)
);

CREATE TABLE validate(
   id_users UUID,
   id_modules INT,
   validate_date DATE NOT NULL,
   PRIMARY KEY(id_users, id_modules),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_modules) REFERENCES modules(id_modules)
);

CREATE TABLE study(
   id_users UUID,
   id_lessons INT,
   validation_date DATE,
   PRIMARY KEY(id_users, id_lessons),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_lessons) REFERENCES lessons(id_lessons)
);

CREATE TABLE revise(
   id_users UUID,
   id_lessons INT,
   PRIMARY KEY(id_users, id_lessons),
   FOREIGN KEY(id_users) REFERENCES users(id_users),
   FOREIGN KEY(id_lessons) REFERENCES lessons(id_lessons)
);




</details>   
