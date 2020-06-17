# TP

## 2.1 Sélections simple

### 1) Sélection du contenu de la table REGIONS

```
SELECT * FROM REGIONS;
```

### 2) Sélections seulement region_name de toutes les régions dans la table REGIONS

```
SELECT REGION_NAME FROM REGIONS;
```

### 3) Sélection pour tous les employés: EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER dans la table EMPLOYEES

```
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, PHONE_NUMBER FROM EMPLOYEES;
```

### 4) Sélection pour tous les employés: FIRST_NAME, LAST_NAME et COMMISSION ( SALAIRE x %COMMISSION)

```
SELECT FIRST_NAME, LAST_NAME, (SALARY * COMMISSION_PCT) AS COMMISSION FROM EMPLOYEES;
```

## 2.2 Sélection avec fonction

### 1) Sélection pour tous les employés : FIRST_NAME, LAST_NAME et COMMISSION (SALAIRE x %COMMISSION_PCT) avec une valeur non nulle

```
SELECT FIRST_NAME, LAST_NAME, (SALARY * NVL(COMMISSION_PCT, 0)) AS COMMISSION FROM EMPLOYEES;
```

### 2) Sélection pour tous les employés : FIRST_NAME, LAST_NAME et COMMISSION (SALAIRE x %COMMISSION_PCT) arrondie à la centaine

```
SELECT FIRST_NAME, LAST_NAME, ROUND((SALARY * NVL(COMMISSION_PCT, 0)), -2) AS COMMISSION FROM EMPLOYEES;
```
