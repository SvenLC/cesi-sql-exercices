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
SELECT CITY "Ville", COUNTRY_NAME "Pays" FROM LOCATIONS
INNER JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID;
```

### 2)

Sélection de : nom de la ville, nom du pays et du nom de sa régions pour toutes les villes de LOCATIONS

```sql
SELECT CITY "Ville", COUNTRY_NAME "Pays", REGION_NAME "Continent" FROM LOCATIONS
INNER JOIN COUNTRIES ON LOCATIONS.COUNTRY_ID = COUNTRIES.COUNTRY_ID
INNER JOIN REGIONS ON COUNTRIES.REGION_ID = REGIONS.REGION_ID;
```

### 3)

Sélection de : nom du département, nom du manager du département et nom de son pays pour toutes les départements de DEPARTMENT ayant un manager

```sql
SELECT DEPARTMENT_NAME "Département", LAST_NAME "Manager", COUNTRY_NAME "Pays" FROM DEPARTMENTS
INNER JOIN LOCATIONS ON DEPARTMENTS.LOCATION_ID = LOCATIONS.LOCATION_ID
INNER JOIN COUNTRIES ON COUNTRIES.COUNTRY_ID = LOCATIONS.COUNTRY_ID
INNER JOIN EMPLOYEES ON DEPARTMENTS.MANAGER_ID = EMPLOYEES.EMPLOYEE_ID;
```

## 1.3 Jointures externes

### 1)

Sélection de : nom du département, nom de son pays et nom du manager du département s’il existe pour toutes les départements de DEPARTMENT

```sql
SELECT DEPARTMENT_NAME "Département", LAST_NAME "Manager", COUNTRY_NAME "Pays" FROM DEPARTMENTS
NATURAL JOIN LOCATIONS
INNER JOIN COUNTRIES USING(COUNTRY_ID)
LEFT JOIN EMPLOYEES ON DEPARTMENTS.MANAGER_ID = EMPLOYEES.EMPLOYEE_ID;
```

Utilisation de la jointure NATURAL et de USING pour l'exemple
