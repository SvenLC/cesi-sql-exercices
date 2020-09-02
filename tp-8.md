# TP 8

## 8.1 Ordre COMMIT

### 1)

Ouvrir une invite de commande Windows et taper la ligne suivante pour se connecter à la base de données Oracle en tant qu’utilisateur « TP2 » :

Ouverture d’une session sous SQLPLUS :

sqlplus TP2/tp2

### 2)

Insérer la ligne suivante dans la table « SALARIES ».

| Matricule | Civilité | Nom    | Prénom  | Responsable | Fonction | Atelier |
| --------- | -------- | ------ | ------- | ----------- | -------- | ------- |
| 43        | M.       | BERGER | Clément | 26          | 3        | 1       |

```sql
INSERT INTO SALARIES (MATRICULE, CIVILITE, NOM, PRENOM, N_MOINS_1, FONCTION, ATELIER)
VALUES ( 43, 'M.', 'BERGER', 'Clement', 26, 3, 1);
```

## 8.2 Ordre ROLLBACK

### 1)

Dans la session TP2 de SQL Developer :

| Matricule | Civilité | Nom   | Prénom | Responsable | Fonction | Atelier |
| --------- | -------- | ----- | ------ | ----------- | -------- | ------- |
| 44        | MME      | LEROY | Annie  | 27          | 1        | 2       |

```sql
INSERT INTO SALARIES (MATRICULE, CIVILITE, NOM, PRENOM, N_MOINS_1, FONCTION, ATELIER)
VALUES ( 44, 'MME', 'LEROY', 'Annie', 27, 1, 2);
```

Sélectionner toutes les lignes de la table SALARIES.

Taper « ROLLBACK ; » pour annuler la transaction.
Sélectionner, de nouveau, toutes les lignes de la table SALARIES.
Vérifier que la salariée « Annie LEROY » est absente du résultat.

## 8.3 Ordre SAVEPOINT

### 1)

Ajout d’une ligne.

Insérer de nouveau la ligne suivante dans la table « SALARIES » :

| Matricule | Civilité | Nom   | Prénom | Responsable | Fonction | Atelier |
| --------- | -------- | ----- | ------ | ----------- | -------- | ------- |
| 44        | MME      | LEROY | Annie  | 27          | 1        | 2       |

```sql
INSERT INTO SALARIES (MATRICULE, CIVILITE, NOM, PRENOM, N_MOINS_1, FONCTION, ATELIER)
VALUES ( 44, 'MME', 'LEROY', 'Annie', 27, 1, 2);
```

Sélectionner toutes les lignes de la table SALARIES et vérifier la présence d’« Annie LEROY » dans le résultat.

Taper;

```sql
SAVEPOINT sauvegarde
```

pour mettre un point de sauvegarde dans la transaction.

### 2)

Ajout d’une seconde ligne.

Insérer de nouveau la ligne suivante dans la table « CLIENTS » :

| Matricule | Civilité | Nom     | Prénom |
| --------- | -------- | ------- | ------ |
| 7         | M        | ROUSSEL | Eric   |

```sql
INSERT INTO CLIENTS (ID, CIVILITE, NOM, PRENOM)
VALUES ( 7, 'M.', 'ROUSSEL', 'Eric');
```

Sélectionner toutes les lignes de la table CLIENT et vérifier la présence d’« Eric ROUSSEL » dans le résultat.

Taper;

```sql
ROLLBACK TO SAVEPOINT sauvegarde
```

Vérifier que l’insertion d’ « Eric ROUSSEL » dans la table CLIENTS a été annulée
Vérifier qu’ « Annie LEROY » est toujours présente dans la table SALARIES.

Taper;

```sql
COMMIT
```

### 3)

Dans la session SQLPLUS :
Sélectionner toutes les lignes de la table SALARIES.
Vérifier que la salarié « Annie LEROY » est présent dans le résultat.

## 8.4 Ordre LOCK TABLE

### 1)

Dans la session SQLPLUS :
Poser un verrou sur la table CLIENTS en mode « EXCLUSIVE ».
Vérifier que l’on peut sélectionner les lignes de la table CLIENTS.

```sql
LOCK TABLE CLIENTS
IN EXCLUSIVE MODE;
```

### 2)

Dans la session TP2 de SQL Developer :
Vérifier que l’on peut sélectionner les lignes de la table CLIENTS.
Insérer de nouveau dans la table CLIENTS :

| Matricule | Civilité | Nom     | Prénom |
| --------- | -------- | ------- | ------ |
| 7         | M        | ROUSSEL | Eric   |

```sql
INSERT INTO CLIENTS (ID, CIVILITE, NOM, PRENOM)
VALUES ( 7, 'M.', 'ROUSSEL', 'Eric');
```

Que se passe-t-il ?
L’ordre SQL est en attente :

### 3)

Dans la session SQLPLUS :
Terminer la transaction dans la session SQLPLUS par une validation ou un retour arrière.

```sql
COMMIT
```

### 4)

Dans la session TP2 de SQL Developer :
La session n’est plus en attente.
Vérifier le contenu de la table CLIENTS.

```sql
SELECT * FROM CLIENTS;
```

### 5)

Dans la session SQLPLUS :
Supprimer dans la table SALARIES « M. FOURNIER ».
Vérifier le contenu de la table SALARIES.

```sql
DELETE FROM SALARIES WHERE CIVILITE = 'M.' AND NOM = 'FOURNIER';
```

## 6)

Dans la session TP2 de SQL Developer :
Vérifier le contenu de la table SALARIES.

| MATRICULE | CIV | NOM      | PRENOM  | N_MOINS_1 | FONCTION | ATELIER |
| --------- | --- | -------- | ------- | --------- | -------- | ------- |
| 5         | MME | DUBOIS   | LAURA   |           | 4        |         |
| 27        | MME | LEGRAND  | JULIE   | 5         | 6        | 2       |
| 19        | MME | DURAND   | ELODIE  | 5         | 5        |         |
| 26        | M.  | MARTIN   | ROMAIN  | 5         | 6        | 1       |
| 40        | M.  | MOREAU   | NICOLAS | 26        | 3        | 1       |
| 34        | MME | ROUX     | AURELIE | 26        | 2        | 1       |
| 36        | M.  | FOURNIER | TTHOMAS | 27        | 1        | 2       |
| 15        | M.  | BLANC    | JULIEN  | 27        | 1        | 2       |
| 43        | M.  | BERGER   | Clément | 26        | 3        | 2       |
| 44        | MME | LEROY    | Annie   | 27        | 1        | 2       |

« M. FOURNIER » est toujours présent.
Modifier le prénom de « M. FOURNIER » en « THOMAS »
Que se passe-t-il ?

### 7)

Dans la session SQLPLUS :
Annuler la transaction dans la session SQLPLUS par l’ordre SQL « ROLLBACK ».

### 8) Dans la session TP2 de SQL Developer :

La session n’est plus en attente.
Vérifier le contenu de la table SALARIES.

| MATRICULE | CIV | NOM      | PRENOM  | N_MOINS_1 | FONCTION | ATELIER |
| --------- | --- | -------- | ------- | --------- | -------- | ------- |
| 5         | MME | DUBOIS   | LAURA   |           | 4        |         |
| 27        | MME | LEGRAND  | JULIE   | 5         | 6        | 2       |
| 19        | MME | DURAND   | ELODIE  | 5         | 5        |         |
| 26        | M.  | MARTIN   | ROMAIN  | 5         | 6        | 1       |
| 40        | M.  | MOREAU   | NICOLAS | 26        | 3        | 1       |
| 34        | MME | ROUX     | AURELIE | 26        | 2        | 1       |
| 36        | M.  | FOURNIER | THOMAS  | 27        | 1        | 2       |
| 15        | M.  | BLANC    | JULIEN  | 27        | 1        | 2       |
| 43        | M.  | BERGER   | Clément | 26        | 3        | 2       |
| 44        | MME | LEROY    | Annie   | 27        | 1        | 2       |

## 8.5 Ordre SELECT … FOR UPDATE

### 1)

Dans la session SQLPLUS :
Sélectionner les salariés aux matricules 43 et 44 de la table SALARIES pour les mettre à jour en ajoutant en fin d’ordre la clause FOR UPDATE.

| MATRICULE | CIV | NOM    | PRENOM  | N_MOINS_1 | FONCTION | ATELIER |
| --------- | --- | ------ | ------- | --------- | -------- | ------- |
| 43        | M.  | BERGER | Clément | 26        | 3        | 2       |
| 44        | MME | LEROY  | Annie   | 27        | 1        | 2       |

```sql
SELECT * FROM SALARIES
WHERE MATRICULE = 43 OR MATRICULE = 44
FOR UPDATE;
```

Modifier le prénom du salarié au matricule 44 afin de mettre son prénom au majuscule.

```sql
UPDATE SALARIES
SET PRENOM = 'ANNIE'
WHERE MATRICULE = 44;
```

### 2)

Dans la session TP2 de SQL Developer :
Modifier le prénom de du salarié au matricule 43 afin de mettre son prénom au majuscule.
Que se passe-t-il ?

```sql
UPDATE SALARIES
SET PRENOM = 'CLEMENT'
WHERE MATRICULE = 43;
```

### 3)

Dans la session SQLPLUS :
Valider la transaction.

### 4)

Dans la session TP2 de SQL Developer :
La session n’est plus en attente.
Valider la transaction.
Vérifier le contenu de la table SALARIES.

| MATRICULE | CIV | NOM      | PRENOM  | N_MOINS_1 | FONCTION | ATELIER |
| --------- | --- | -------- | ------- | --------- | -------- | ------- |
| 5         | MME | DUBOIS   | LAURA   |           | 4        |         |
| 27        | MME | LEGRAND  | JULIE   | 5         | 6        | 2       |
| 19        | MME | DURAND   | ELODIE  | 5         | 5        |         |
| 26        | M.  | MARTIN   | ROMAIN  | 5         | 6        | 1       |
| 40        | M.  | MOREAU   | NICOLAS | 26        | 3        | 1       |
| 34        | MME | ROUX     | AURELIE | 26        | 2        | 1       |
| 36        | M.  | FOURNIER | THOMAS  | 27        | 1        | 2       |
| 15        | M.  | BLANC    | JULIEN  | 27        | 1        | 2       |
| 43        | M.  | BERGER   | CLEMENT | 26        | 3        | 2       |
| 44        | MME | LEROY    | ANNIE   | 27        | 1        | 2       |
