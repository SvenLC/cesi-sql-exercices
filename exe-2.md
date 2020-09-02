# 2 Sous-requètes

## 2.1 Sous requête dans la clause WHERE

### 1)

Sélection first_name, last_name des employés de EMPLOYEES qui sont managers d’un département

```sql
SELECT FIRST_NAME, LAST_NAME FROM EMPLOYEES
WHERE EMPLOYEE_ID IN (SELECT MANAGER_ID FROM DEPARTMENTS);
```

## 2.2 Sous requête dans la clause FROM

### 1)

Sélection first_name, last_name, salaire des employés de EMPLOYEES ayant le plus petit salaire ou le plus gros salaire

```sql
SELECT FIRST_NAME, LAST_NAME, SALARY FROM EMPLOYEES
JOIN(SELECT MIN(SALARY) salaire_min, MAX(SALARY) salaire_max FROM EMPLOYEES)
    salaires ON EMPLOYEES.SALARY = salaires.salaire_min
            OR EMPLOYEES.SALARY = salaires.salaire_max;
```
