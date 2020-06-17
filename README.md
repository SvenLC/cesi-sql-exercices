# TP

## 2.1 Sélections simple

### 1)

Sélection du contenu de la table REGIONS

```
SELECT * FROM REGIONS;
```

### 2)

Sélections seulement region_name de toutes les régions dans la table REGIONS

```
SELECT REGION_NAME FROM REGIONS;
```

### 3)

Sélection pour tous les employés: EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER dans la table EMPLOYEES

```
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER FROM EMPLOYEES;
```

### 4)

Sélection pour tous les employés: FIRST_NAME, LAST_NAME et COMMISSION ( SALAIRE x %COMMISSION)

```
SELECT FIRST_NAME, LAST_NAME, (SALARY * COMMISSION_PCT) AS COMMISSION FROM EMPLOYEES;
```

## 2.2 Sélection avec fonction

### 1)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et COMMISSION (SALAIRE x %COMMISSION_PCT) avec une valeur non nulle

```
SELECT FIRST_NAME, LAST_NAME, (SALARY * NVL(COMMISSION_PCT, 0)) AS COMMISSION FROM EMPLOYEES;
```

### 2)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et COMMISSION (SALAIRE x %COMMISSION_PCT) arrondie à la centaine

```
SELECT FIRST_NAME, LAST_NAME, ROUND((SALARY * NVL(COMMISSION_PCT, 0)), -2) AS COMMISSION FROM EMPLOYEES;
```

### 3)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et date d’embauche(HIRE_DATE)

```
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE FROM EMPLOYEES;
```

### 4)

Sélection pour tous les employés : FIRST_NAME, LAST_NAME et année d’embauche(HIRE_DATE)

```
SELECT FIRST_NAME, LAST_NAME, EXTRACT(YEAR FROM HIRE_DATE) FROM EMPLOYEES;
```

## 2.3

### 1)

Sélection de : FIRST_NAME, LAST_NAME et SALARY pour les employés ayant un salaire > 12000.

```
SELECT FIRST_NAME, LAST_NAME, SALARY FROM EMPLOYEES WHERE SALARY > 12000;
```

### 2)

Sélection de : FIRST_NAME, LAST_NAME et SALARY pour les employés ayant un salaire
compris entre 5000 et 6000.

```
SELECT FIRST_NAME, LAST_NAME, SALARY FROM EMPLOYEES WHERE SALARY > 5000 AND SALARY < 6000;
```

### 3)

Sélection de : FIRST_NAME, LAST_NAME et année d’embauche (HIRE_DATE) pour les employés embauchés avant 2003.

```
SELECT FIRST_NAME, LAST_NAME, EXTRACT(YEAR FROM HIRE_DATE) FROM EMPLOYEES WHERE EXTRACT(YEAR FROM HIRE_DATE) < 2003;
```

### 4)

Sélection de : FIRST_NAME, LAST_NAME et COMMISSION_PCT pour les employés ayant une commission.

```
SELECT FIRST_NAME, LAST_NAME, COMMISSION_PCT FROM EMPLOYEES WHERE COMMISSION_PCT IS NOT NULL;
```
