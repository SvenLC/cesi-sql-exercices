# TP Oracle SQL 4

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
