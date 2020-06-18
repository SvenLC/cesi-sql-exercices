# TP

## 2.1 Sélections simple

### 1)

Sélection du contenu de la table REGIONS

```sql
SELECT * FROM REGIONS;
```

### 2)

Sélections seulement region_name de toutes les régions dans la table REGIONS

```sql
SELECT REGION_NAME FROM REGIONS;
```

### 3)

Sélection pour tous les employés: EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER dans la table EMPLOYEES

```sql
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER FROM EMPLOYEES;
```

### 4)

Sélection pour tous les employés: FIRST_NAME, LAST_NAME et COMMISSION ( SALAIRE x %COMMISSION)

```sql
SELECT FIRST_NAME, LAST_NAME, (SALARY * COMMISSION_PCT) AS COMMISSION FROM EMPLOYEES;
```

## 2.2 Sélection avec fonction

### 1)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et COMMISSION (SALAIRE x %COMMISSION_PCT) avec une valeur non nulle

```sql
SELECT FIRST_NAME, LAST_NAME, (SALARY * NVL(COMMISSION_PCT, 0)) AS COMMISSION FROM EMPLOYEES;
```

### 2)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et COMMISSION (SALAIRE x %COMMISSION_PCT) arrondie à la centaine

```sql
SELECT FIRST_NAME, LAST_NAME, ROUND((SALARY * NVL(COMMISSION_PCT, 0)), -2) AS COMMISSION FROM EMPLOYEES;
```

### 3)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et date d'embauche(HIRE_DATE)

```sql
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE FROM EMPLOYEES;
```

### 4)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et année d'embauche(HIRE_DATE)

```sql
SELECT FIRST_NAME, LAST_NAME, EXTRACT(YEAR FROM HIRE_DATE) FROM EMPLOYEES;
```

## 2.3

### 1)

Sélection de : FIRST_NAME, LAST_NAME et SALARY pour les employés ayant un salaire > 12000.

```sql
SELECT FIRST_NAME, LAST_NAME, SALARY FROM EMPLOYEES WHERE SALARY > 12000;
```

### 2)

Sélection de : FIRST_NAME, LAST_NAME et SALARY pour les employés ayant un salaire
compris entre 5000 et 6000.

```sql
SELECT FIRST_NAME, LAST_NAME, SALARY FROM EMPLOYEES WHERE SALARY > 5000 AND SALARY < 6000;
```

### 3)

Sélection de : FIRST_NAME, LAST_NAME et année d'embauche (HIRE_DATE) pour les employés embauchés avant 2003.

```sql
SELECT FIRST_NAME, LAST_NAME, EXTRACT(YEAR FROM HIRE_DATE) FROM EMPLOYEES WHERE EXTRACT(YEAR FROM HIRE_DATE) < 2003;
```

### 4)

Sélection de : FIRST_NAME, LAST_NAME et COMMISSION_PCT pour les employés ayant une commission.

```sql
SELECT FIRST_NAME, LAST_NAME, COMMISSION_PCT FROM EMPLOYEES WHERE COMMISSION_PCT IS NOT NULL;
```

### 5)

Sélection de : first_name, last_name et commission_pct au format « 0,xx » pour les employés ayant une commission.

```sql
SELECT FIRST_NAME, LAST_NAME, TO_CHAR(COMMISSION_PCT, '0.99') FROM EMPLOYEES WHERE COMMISSION_PCT IS NOT NULL;
```

> Remarque : avec '0,99', toutes les valeurs étaient amenées à 0,00. Une solution ?

### 6)

Sélection de : first_name, last_name et department_id pour les employés des département 70 et 90.

```sql
SELECT FIRST_NAME, LAST_NAME, DEPARTMENT_ID FROM EMPLOYEES WHERE DEPARTMENT_ID IN (70,90);
```

### 7)

Sélection de : first_name, last_name, job_id et department_id pour les employés ayant une fonction d'administration c'est-à-dire que le job_id commence par « AD ».

```sql
SELECT FIRST_NAME, LAST_NAME, JOB_ID, DEPARTMENT_ID FROM EMPLOYEES WHERE JOB_ID LIKE('AD%');
```

### 8)

Sélection de : first_name, last_name, nombre de mois d'ancienneté pour tous les employés.

```sql
SELECT FIRST_NAME, LAST_NAME, ROUND(MONTHS_BETWEEN(SYSDATE, HIRE_DATE)) AS "ANCIENNETE (Mois)" FROM EMPLOYEES;
```

### 9)

Sélection de : first_name, last_name, job_id et nombre de jours d'ancienneté pour les employés ayant moins d'une année d'ancienneté au 10 août 2008.

```sql
SELECT FIRST_NAME, LAST_NAME, ROUND((TO_DATE('10/08/2008') - HIRE_DATE)) AS "ANCIENNETE (Jours)"
FROM EMPLOYEES
WHERE TO_DATE('10/08/2008') - HIRE_DATE < 366;
```

### 10)

Sélection des noms de départements n'ayant pas de manager

```sql
SELECT DEPARTMENT_NAME FROM DEPARTMENTS WHERE MANAGER_ID IS NULL;
```

### 11)

Sélection des adresses, des états et des villes des locations du pays US

```sql
SELECT STREET_ADDRESS, STATE_PROVINCE, CITY FROM LOCATIONS
WHERE COUNTRY_ID = 'US';
```

### 12)

Sélection numéro de rue (s'il existe sinon '....', nom de la rue, ville de

> WTF ???

### 13)

Sélection dans la table historique de jobs numéro de l'employé, le mois/année de début et de fin et l'ID du job.

```sql
SELECT EMPLOYEE_ID, TO_CHAR(START_DATE, 'MM/YYYY') AS START_DATE, TO_CHAR(END_DATE, 'MM/YYYY') AS END_DATE, JOB_ID FROM JOB_HISTORY;
```

### 14)

Sélection, dans la table des employés, le prénom et le nom et la reconstruire l'email à partir de nom et du prénom de chaque employé

```sql
SELECT FIRST_NAME, LAST_NAME, UPPER(SUBSTR(FIRST_NAME, 0, 1) || LAST_NAME) as EMAIL FROM EMPLOYEES;
```

### 15)

Sélection dans la table historique de jobs numéro de l'employé, le mois/année de début et de fin et l'ID du job.

> Voir exercice 13

### 16)

Sélection des ID, nom, et prénom des employés dont le salaire annuel + commission > 82000

```sql
SELECT EMPLOYEE_ID, LAST_NAME, FIRST_NAME FROM EMPLOYEES WHERE (COMMISSION_PCT*SALARY+SALARY)*12 > 82000;
```

### 17)

Sélection du ° de téléphone, nom, prénom des employés qui n'ont pas un ° de téléphone du type 123.123.1234,

```sql
SELECT PHONE_NUMBER, LAST_NAME, FIRST_NAME FROM EMPLOYEES WHERE PHONE_NUMBER NOT LIKE ('___.___.____');
--version REGEX :
SELECT PHONE_NUMBER, LAST_NAME, FIRST_NAME FROM EMPLOYEES WHERE NOT REGEXP_LIKE(PHONE_NUMBER, '[0-9]{3}.[0-9]{3}.[0-9]{4}');
```

### 18)

Sélection pour chaque employé ayant une commission >= a 15%, le prénom et le nom et leur trigramme (1 lettre du prénom + 1 lettre du nom + dernière lettre de nom) le tout en majuscule

```sql
SELECT FIRST_NAME, LAST_NAME, UPPER(SUBSTR(FIRST_NAME, 0, 1) || SUBSTR(LAST_NAME, 0, 1) || SUBSTR(LAST_NAME, -1, 1)) AS TRIGRAMME FROM EMPLOYEES
=======
```

### 19)

Sélection pour de tous les employés ayant 2 e de suite « ee » dans leur nom ou leur prénom.

```sql
SELECT * FROM EMPLOYEES WHERE FIRST_NAME LIKE ('%ee%') OR LAST_NAME LIKE('%ee%');
```

### 20)

Sélection du nom et prénom des employés avec pour les noms la première et dernière lettre en clair et les autres remplacées par « \* ».

```sql
SELECT
  SUBSTR(LAST_NAME, 0, 1) || REPLACE(LAST_NAME, SUBSTR(LAST_NAME, 1, LENGTH(LAST_NAME)), '*') || SUBSTR(LAST_NAME, -1, 1) AS LAST_NAME,
  SUBSTR(FIRST_NAME , 0, 1) || REPLACE(FIRST_NAME, SUBSTR(FIRST_NAME, 1, LENGTH(FIRST_NAME)), '*') || SUBSTR(FIRST_NAME , -1, 1) AS FIRST_NAME
FROM EMPLOYEES;
```

### 21)

Sélection pour du nom et prénom des employés qui ont le même nombre de lettres dans leur nom que dans leur prénom.

```sql
SELECT LAST_NAME, FIRST_NAME FROM EMPLOYEES WHERE LENGTH(LAST_NAME) = LENGTH(FIRST_NAME);
```

### 22)

> Comme 21.

### 23)

Sélection pour du nom et prénom des employés qui ont moins 2 l (lettre L) dans leur nom et prénom

```sql
SELECT * FROM EMPLOYEES WHERE (LENGTH(FIRST_NAME) - LENGTH(REPLACE(FIRST_NAME, 'l', ''))) + (LENGTH(LAST_NAME) - LENGTH(REPLACE(LAST_NAME, 'l', ''))) < 2;
```

### 24)

Sélection des locations dont le code postal n'a que des chiffres

```sql
SELECT * FROM LOCATIONS WHERE REGEXP_LIKE(POSTAL_CODE, '^[0-9]+$');
```

## 3.1 Produit cartésien

### 1)

Sélection de : toutes les colonnes du produit catésien de COUNTRIES et de
REGIONS.

```sql
SELECT * FROM COUNTRIES, REGIONS;
```

## 3.2 Jointures simple (équijointures)

### 1)

Sélection de : nom du pays et du nom de sa régions pour tous les pays de COUNTRIES.

```sql
SELECT COUNTRY_NAME, REGION_NAME FROM COUNTRIES INNER JOIN REGIONS ON COUNTRIES.REGION_ID = REGIONS.REGION_ID;
```

### 2)

Sélection de : nom de la ville, nom du pays et du nom de sa régions pour toutes les villes de LOCATIONS.

```sql
SELECT CITY, COUNTRY_NAME, REGION_NAME FROM LOCATIONS
INNER JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID
INNER JOIN REGIONS ON COUNTRIES.REGION_ID = REGIONS.REGION_ID;
```

### 3)

```sql
SELECT DEPARTMENT_NAME, REGION_NAME FROM DEPARTMENTS
INNER JOIN LOCATIONS ON DEPARTMENTS.LOCATION_ID = LOCATIONS.LOCATION_ID
INNER JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID
INNER JOIN REGIONS ON COUNTRIES.REGION_ID = REGIONS.REGION_ID;
```

### 4)

```sql
SELECT DEPARTMENT_NAME, CITY FROM DEPARTMENTS
INNER JOIN LOCATIONS ON DEPARTMENTS.LOCATION_ID = LOCATIONS.LOCATION_ID;
```

## 3.3 Jointures externes

### 1)

Sélection de : nom département, nom de sa ville et nom de son manager, s’il existe, pour tous les départements de DEPARTMENTS

```sql
SELECT DEPARTMENT_NAME, CITY, LAST_NAME
FROM DEPARTMENTS
INNER JOIN LOCATIONS ON DEPARTMENTS.LOCATION_ID = LOCATIONS.LOCATION_ID
LEFT JOIN EMPLOYEES ON DEPARTMENTS.MANAGER_ID = EMPLOYEES.EMPLOYEE_ID;
```

### 2)

Sélection de : nom région, titre de job s’il existe, pour tous les régions de
REGIONS. Si une région n’a pas de job retourner la région , ‘pas de job’

```sql
SELECT DISTINCT REGION_NAME, NVL(JOB_TITLE, 'Pas de Job !')
FROM JOBS
INNER JOIN EMPLOYEES ON JOBS.JOB_ID = EMPLOYEES.JOB_ID
INNER JOIN DEPARTMENTS ON EMPLOYEES.DEPARTMENT_ID = DEPARTMENTS.DEPARTMENT_ID
INNER JOIN LOCATIONS ON DEPARTMENTS.LOCATION_ID = LOCATIONS.LOCATION_ID
INNER JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID
FULL JOIN REGIONS ON COUNTRIES.REGION_ID = REGIONS.REGION_ID;
```

## 3.4 Auto-jointure

### 1)

) Sélection de : prénom, nom et nom du manager pour tous les employés de
EMPLOYEES ayant un salaire < 2500

```sql
SELECT e.FIRST_NAME, e.LAST_NAME, m.FIRST_NAME
FROM EMPLOYEES e
INNER JOIN EMPLOYEES m ON e.MANAGER_ID = m.EMPLOYEE_ID
WHERE e.SALARY < 2500;
```

## 4.1

### 1)

Sélection du salaire moyen de l’ensemble des employés de EMPLOYEES

```sql
SELECT AVG(SALARY)
FROM EMPLOYEES;
```

### 2)

Sélection de : nom de département, salaire moyen des employés pour tous les
départements de DEPARTMENTS

```sql
SELECT DEPARTMENT_NAME, NVL(ROUND(AVG(SALARY)),0)
FROM EMPLOYEES
JOIN DEPARTMENTS ON EMPLOYEES.DEPARTMENT_ID = DEPARTMENTS.DEPARTMENT_ID
GROUP BY DEPARTMENT_NAME;
```

### 3)

Sélection de : nom de département, nom de fonction, nombre d’employés pour la fonction pour les départements de DEPARTMENTS et les fonctions de JOBS ayant des employés

```sql
SELECT DEPARTMENT_NAME, JOB_TITLE, COUNT(EMPLOYEE_ID)
FROM DEPARTMENTS
INNER JOIN EMPLOYEES ON DEPARTMENTS.DEPARTMENT_ID = EMPLOYEES.DEPARTMENT_ID
INNER JOIN JOBS ON EMPLOYEES.JOB_ID = JOBS.JOB_ID
GROUP BY DEPARTMENT_NAME, JOB_TITLE
ORDER BY DEPARTMENT_NAME;
```

### 4)

Sélection de : nom de la ville, le salaire minimum, le salaire maximum, nombre d’employés pour toutes les villes de LOCATIONS ayant des employés

```sql
SELECT CITY, MIN(SALARY), MAX(SALARY), COUNT(EMPLOYEE_ID)
FROM LOCATIONS
INNER JOIN DEPARTMENTS ON LOCATIONS.LOCATION_ID = DEPARTMENTS.LOCATION_ID
INNER JOIN EMPLOYEES ON DEPARTMENTS.DEPARTMENT_ID = EMPLOYEES.DEPARTMENT_ID
GROUP BY CITY;
```

## 4.2 Filtrage des regroupements

### 1)

Sélection de : nom de la ville, le salaire minimum, le salaire maximum, le salaire moyen arrondi à l’unité pour toutes les villes de LOCATIONS ayant au moins 5 employés.

```sql
SELECT CITY, MIN(SALARY), MAX(SALARY), ROUND(AVG(SALARY)), COUNT(EMPLOYEE_ID)
FROM LOCATIONS
INNER JOIN DEPARTMENTS ON LOCATIONS.LOCATION_ID = DEPARTMENTS.LOCATION_ID
INNER JOIN EMPLOYEES ON DEPARTMENTS.DEPARTMENT_ID = EMPLOYEES.DEPARTMENT_ID
GROUP BY CITY
HAVING COUNT(EMPLOYEE_ID) >= 5;
```

### 2)

Sélection de : nom du manager, nom de la fonction des employés, commission
moyenne arrondie à l’unité pour tous les manager des employés de EMPLOYEES
ayant une commission et chaque fonction de JOBS de ces employés.

```sql
SELECT m.LAST_NAME as "Manager", j.JOB_TITLE as "Métier", ROUND(AVG(e.COMMISSION_PCT*e.SALARY)) as "Commission moyenne"
FROM EMPLOYEES e
INNER JOIN EMPLOYEES m ON e.MANAGER_ID = m.EMPLOYEE_ID
INNER JOIN JOBS j ON e.JOB_ID = j.JOB_ID
WHERE e.COMMISSION_PCT IS NOT NULL
GROUP BY m.LAST_NAME, j.JOB_TITLE;
```

### 3)

Sélection de : prénom, nom des employés de EMPLOYEES ayant changés de
fonction (indiqués dans JOB_HISTORY)

```sql
SELECT DISTINCT e.FIRST_NAME, e.LAST_NAME
FROM EMPLOYEES e
INNER JOIN JOB_HISTORY j ON e.EMPLOYEE_ID = j.EMPLOYEE_ID;
```

### 4)

Sélection de : ville, nom du manager, % de commission moyenne des employés de EMPLOYEES par villes et managers dont les subordonnées ont une commission.

```sql
SELECT city, m.last_name, TO_CHAR(AVG(e.COMMISSION_PCT * 100), ‘90’) || ‘ %’
FROM EMPLOYEES e
JOIN EMPLOYEES m ON e.MANAGER_ID = m.EMPLOYEE_ID
JOIN DEPARTMENTS d ON e.DEPARTMENT_ID =  DEPARTMENTS.DEPARTMENT_ID
JOIN LOCATIONS l ON d.LOCATION_ID = l.LOCATION_ID
GROUP BY CITY, m.LAST_NAME
HAVING AVG(e.COMMISSION_PCT) IS NOT NULL ;
```

### 5)

```sql
SELECT COUNTRY_ID, m.LAST_NAME, COUNT(*)
FROM LOCATIONS
INNER JOIN DEPARTMENTS on LOCATIONS.LOCATION_ID = DEPARTMENTS.LOCATION_ID
INNER JOIN EMPLOYEES m on DEPARTMENTS.DEPARTMENT_ID = m.DEPARTMENT_ID
INNER JOIN EMPLOYEES e on e.MANAGER_ID = m.EMPLOYEE_ID
GROUP BY COUNTRY_ID, m.LAST_NAME
HAVING COUNTRY_ID <> 'US';
```

## 5.1 Sous requête dans la clause WHERE

### 1)

Sélection first_name, last_name des employés de EMPLOYEES ayant le plus petit salaire

```sql
SELECT FIRST_NAME, LAST_NAME
FROM EMPLOYEES
WHERE SALARY = (SELECT MIN(SALARY) FROM EMPLOYEES);
```

### 2)

Sélection first_name, last_name des employés de EMPLOYEES qui sont managers

```sql
SELECT m.FIRST_NAME, m.LAST_NAME
FROM EMPLOYEES m
WHERE m.EMPLOYEE_ID IN (SELECT MANAGER_ID FROM EMPLOYEES);
```

### 3)

Sélection de : first_name, last_name des employés de EMPLOYEES ayant le même last_name.

```sql
SELECT FIRST_NAME, LAST_NAME
FROM EMPLOYEES
WHERE LAST_NAME IN (
SELECT LAST_NAME FROM EMPLOYEES GROUP BY LAST_NAME HAVING COUNT(*) > 1);
```

### 4)

Sélection de : prénom, nom, fonction, précédente fonction des employés de
EMPLOYEES ayant changés de fonction (indiqués dans JOB_HISTORY)

```sql
SELECT e.FIRST_NAME, e.LAST_NAME, e.JOB_ID, h.JOD_ID
FROM EMPLOYEES e
JOIN JOB_HISTORY h ON e.EMPLOYEE_ID = h.EMPLOYEE_ID
WHERE EMPLOYEE_ID = h.EMPLOYEE_ID
```

## 5.2 Sous requête dans la clause FROM

### 1)

Sélection first_name, last_name, salaire des employés de EMPLOYEES ayant le plus petit salaire ou le plus gros salaire

### 2)

Sélection de : prénom, nom, fonction, précédente fonction des employés de
EMPLOYEES ayant changés de fonction (indiqués dans JOB_HISTORY)

```sql
SELECT FIRST_NAME, LAST_NAME, job_actuel.JOB_TITLE "Fonction actuelle", job_precedent.JOB_TITLE "Précédente fonction"
FROM JOB_HISTORY
JOIN EMPLOYEES ON EMPLOYEES.EMPLOYEE_ID = JOB_HISTORY.EMPLOYEE_ID
JOIN JOBS job_actuel ON EMPLOYEES.JOB_ID = job_actuel.JOB_ID
JOIN JOBS job_precedent ON JOB_HISTORY.JOB_ID = job_precedent.JOB_ID
JOIN
(
  SELECT EMPLOYEE_ID, MAX(END_DATE) AS max_date
  FROM JOB_HISTORY
  GROUP BY EMPLOYEE_ID
) precedent
ON precedent.EMPLOYEE_ID = EMPLOYEES.EMPLOYEE_ID
AND precedent.MAX_DATE = JOB_HISTORY.END_DATE;
```

### 3)

Sélection first_name, last_name des employés de EMPLOYEES qui sont managers

```sql
SELECT e.FIRST_NAME, e.LAST_NAME
FROM EMPLOYEES e
JOIN
(
  SELECT MANAGER_ID, COUNT(EMPLOYEE_ID)
  FROM EMPLOYEES
  GROUP BY MANAGER_ID
) manager
ON e.EMPLOYEE_ID = manager.MANAGER_ID;
```
