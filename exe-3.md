# 3 Regroupements GROUP BY … HAVING

## 3.1 Requêtes de regroupement

### 1)

Sélection du nombre de ville de LOCATIONS

```sql
SELECT COUNT(\*) "Nombre de ville" FROM LOCATIONS;
```

### 2)

Sélection de : nom de la ville, salaire moyen des employés pour tous les villes de LOCATIONS ayant des employés

```sql
SELECT CITY, ROUND(avg(SALARY)) "Salaire" FROM EMPLOYEES
JOIN DEPARTMENTS USING (DEPARTMENT_ID)
JOIN LOCATIONS USING (LOCATION_ID)
GROUP BY CITY;
```

## 3.2 Filtrage des regroupements

### 1)

Sélection de : nom du pays, le salaire minimum, le salaire maximum, le salaire moyen arrondi à l’unité pour toutes les pays de COUNTRIES ayant au moins 5 employés.

```sql
SELECT COUNTRY_NAME "Pays", MIN(SALARY) "Salaire minimum", MAX(SALARY) "Salaire maximum", ROUND(avg(SALARY)) "Salaire moyen" FROM EMPLOYEES
JOIN DEPARTMENTS USING (DEPARTMENT_ID)
JOIN LOCATIONS USING (LOCATION_ID)
JOIN COUNTRIES USING (COUNTRY_ID)
GROUP BY COUNTRY_NAME
HAVING COUNT(*) >= 5;
```
