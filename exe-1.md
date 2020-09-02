# 1 Jointures

## 1.1 Produit Cartésien

### 1)

Sélection de : toutes les colonnes du produit catésien de COUNTRIES et de REGIONS.

```sql
SELECT * FROM COUNTRIES, REGIONS;
```

## 1.2 Jointures simples

### 1)

Sélection de : nom de la ville et du nom de son pays pour tous les villes de LOCATIONS.

```sql
SELECT CITY, COUNTRIES.COUNTRY_NAME FROM LOCATIONS
JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID;
```

### 2)

Sélection de : nom de la ville, nom du pays et du nom de sa régions pour toutes les villes de LOCATIONS

```sql
SELECT CITY, COUNTRIES.COUNTRY_NAME, REGIONS.REGION_NAME FROM LOCATIONS
JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID
JOIN REGIONS ON COUNTRIES.REGION_ID = REGIONS.REGION_ID;
```

### 3)

Sélection de : nom du département, nom du manager du département et nom de son pays pour toutes les départements de DEPARTMENT ayant un manager

```sql
SELECT DEPARTMENTS.DEPARTMENT_NAME, EMPLOYEES.FIRST_NAME, LOCATIONS.CITY FROM DEPARTMENTS
INNER JOIN EMPLOYEES ON DEPARTMENTS.MANAGER_ID = EMPLOYEES.EMPLOYEE_ID
INNER JOIN LOCATIONS ON DEPARTMENTS.LOCATION_ID = LOCATIONS.LOCATION_ID;
```
