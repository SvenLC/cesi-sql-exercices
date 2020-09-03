# Contrôle de connaissance Maîtrise du language SQL

Sven Le Cann

## 1)

```sql
SELECT * FROM SALARIES;
```

## 2)

```sql
SELECT PRENOM, NOM FROM SALARIES
WHERE CIVILITE = 'MME';
```

## 3)

```sql
SELECT CIVILITE, PRENOM, NOM FROM CLIENTS
LEFT JOIN VOITURES ON CLIENTS.ID = VOITURES.PROPRIETAIRES;
```

## 4)

```sql
SELECT MARQUES.NOM AS "Marque", MODELES.NOM AS "Modèles" FROM MODELES
LEFT JOIN MARQUES ON MODELES.MARQUE = MARQUES.ID
ORDER BY Marque, Modèles;
```

## 5)

```sql
SELECT MARQUES.NOM, COUNT(MODELES.ID) FROM MARQUES
JOIN MODELES ON MARQUES.ID = MODELES.MARQUE
GROUP BY MARQUES.NOM;
```

## 6)

```sql
SELECT * FROM MARQUES
OUTER JOIN MODELES ON MARQUES.ID = MODELES.MARQUE;
```

## 7)

```sql
INSERT INTO CLIENTS (ID, CIVILITE, NOM, PRENOM)
VALUES (50, 'M.', 'LE GAC', 'Yann');
```

## 8)

```sql
UPDATE CLIENTS
SET PRENOM = 'Alan'
WHERE ID = 50;
```

## 9)

```sql
DELETE FROM CLIENTS
WHERE NOM = 'LE GAC' AND PRENOM = 'Alan';
```

## 10)

```sql
UPDATE CLIENTS
SET PRENOM = UPPER(PRENOM);
```

## 11)

L'ordre COMMIT permet de sauvegarder dans la bases de données les modifications effectuées lors d'une transaction, afin qu'elles puissent être visibles par toutes les sessions connectées.

L'ordre ROLLBACK permet de revenir à un point de sauvegarde ou au dernier COMMIT lors d'une transaction.

## 12)

```sql
CREATE TABLE OUTILLAGES (
    NO_INVENTAIRE NUMBER NOT NULL PRIMARY KEY,
    DESCRIPTION VARCHAR2(255) NOT NULL,
    DATE_ACQUISITION DATE,
    TYPE_OUTIL NUMBER
);
```

## 13)

```sql
CREATE VIEW VUE_PEC_EN_COURS AS (
    SELECT REFERENCE, VEHICULE, DATE_DEBUT, DATE_FIN FROM PRISES_EN_CHARGE
    WHERE DATE_FIN = NULL
);
```

## 14)

```sql
RENAME VOITURES TO VEHICULES;
```
