# TP 7

## 71. Ordre INSERT

### 1)

Insertion dans la table CLIENTS de 2 nouvelles lignes.

```sql
INSERT INTO CLIENTS (ID, CIVILITE, NOM, PRENOM) VALUES (11, 'MME', 'GARNIER', 'Jeanne');
INSERT INTO CLIENTS (ID, CIVILITE, NOM, PRENOM) VALUES (14,	'M.', 'DURAND', 'Loïc');
```

### 2)

Insertion dans la table PRISE_EN_CHARGE d’une nouvelle ligne.

```sql
INSERT INTO PRISES_EN_CHARGE (REFERENCE, VEHICULE, DETAIL, KILOMETRAGE, DATE_DEBUT, SALARIE_MATRICULE)
VALUES ('2019-0001', 'WW-660-CD', 'Entretien périodique', 15089, LAST_DAY(ADD_MONTHS(SYSDATE, -1 )), 15);
```

```sql
INSERT INTO PRISES_EN_CHARGE (REFERENCE, VEHICULE, DETAIL, KILOMETRAGE, DATE_DEBUT, SALARIE_MATRICULE)
VALUES ('2019-0002', 'WW-826-FX', 'Equilibrage pneu à l’avant gauche', 62975, TO_DATE('2019/02/01 16:58:00', 'YYYY/MM/DD HH24:MI:SS'), 15);
```

```sql
INSERT INTO PRISES_EN_CHARGE (REFERENCE, VEHICULE, DETAIL, KILOMETRAGE, DATE_DEBUT, SALARIE_MATRICULE)
VALUES ('2019-0003', 'WW-885-AK', 'Echappement', 62975, SYSDATE - 1, 36);
```

```sql
INSERT INTO PRISES_EN_CHARGE (REFERENCE, VEHICULE, DETAIL, KILOMETRAGE, DATE_DEBUT, SALARIE_MATRICULE)
VALUES ('2019-0004', 'WW-454-QR', 'Retouche peinture aile avant droite', 3561, SYSDATE, 40);
```

### 3)

Insertion dans la table SALARIES d’une nouvelle ligne.

```sql
INSERT INTO SALARIES (MATRICULE, CIVILITE, NOM, PRENOM, FONCTION)
VALUES (42,	'M.', 'DUVAL', 'Gilles', (SELECT ID FROM FONCTIONS WHERE TITRE = 'PEINTRE'));
```

### 4)

Ajout d’un client.

```sql
INSERT INTO CLIENTS (ID, CIVILITE, NOM, PRENOM)
VALUES ((SELECT MAX(ID) FROM CLIENTS )+ 1,	'MME', 'MOREL', 'Marie');
```

## 7.2 Ordre UPDATE

### 1)

Mise à jour de la ligne ajoutée au 1 du § 1.1 (client BRUN) : son prénom est
« Jean-Noël ».

```sql
UPDATE CLIENTS
SET PRENOM = 'Jean-Noël'
WHERE NOM = 'BRUN';
```

### 2)

Mise à jour de la ligne ajoutée au 2 du § 1.1 (référence 2019-0001) : le véhicule est le « WW-046-JV » et le kilométrage est de 21328.

```sql
UPDATE PRISE_EN_CHARGE
SET VEHICULE = 'WW-046-JVV',
    KILOMETRAGE = 21326
WHERE REFERENCE = '2019-001';
```

### 3)

Mise à jour de la ligne ajoutée au 3 du § 1.1 (matricule 42) : l’atelier est « CARROSSERIE ».

```sql
UPDATE SALARIES
SET ATELIER = (SELECT ID FROM ATELIERS WHERE NOM ='CAROSSERIE')
WHERE MATRICULE = 42;
```

### 4)

Mise à jour des lignes de la PRISES_EN_CHARGE : le matricule du salarie est celui du « supérieur » de celui existant.

```sql
UPDATE PRISES_EN_CHARGE
SET SALARIE_MATRICULE = (SELECT n_moins1 FROM SALARIES WHERE MATRICULE =PRISES_EN_CHARGE.SALARIE_MATRICULE);
```

### 5)

Affectation du véhicule de « M. MOREL » à « MME MOREL ».

```sql
UPDATE VOITURES
SET PROPRIETAIRES = (SELECT ID FROM CLIENTS WHERE NOM = 'MOREL' AND CIVILITE = 'MME')
WHERE PROPRIETAIRES = (SELECT ID FROM CLIENTS WHERE NOM = 'MOREL' AND CIVILITE = 'MM');
```

## 7.3 Ordre DELETE

### 1)

Suppression de la ligne de PRISES_EN_CHARGE ayant comme référence
« 2019-0002 ».

```sql
DELETE FROM PRISES_EN_CHARGE WHERE REFERENCE = '2019-001';
```

### 2)

Suppression dans CLIENT du nom « ROUSSEL».

```sql
DELETE FROM CLIENTS WHERE NOM = 'ROUSSEL';
```

### 3)

Suppression dans CLIENT du nom « DURAND » .
Que se passe-t-il ?

```sql
DELETE FROM CLIENTS WHERE NOM = 'DURAND';
```

### 4)

Suppressions de la base de données de « DUPONT Erwan » et de ses véhicules.

```sql
DELETE FROM VOITURES
WHERE PROPRIETAIRE = (SELECT ID FROM CLIENTS WHERE NOM = 'DUPONT' AND PRENOM = 'Erwan');
```

```sql
DELETE FROM CLIENTS WHERE NOM = 'DUPONT' AND PRENOM = 'Erwan';
```
