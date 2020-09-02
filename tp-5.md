# TP Oracle SQL 5

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
