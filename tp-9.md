# TP 9

## 9.1 Création de tables

### 1)

Création d’une table simple.
Créer une nouvelle table « CLASSES » dans le schéma TP2 comme suit :

| Nom colonne | Type données  | Null possible | Contrainte    |
| ----------- | ------------- | ------------- | ------------- |
| ID          | NUMBER        | NON           | Clef primaire |
| LIBELLE     | VARCHAR2(20)  | NON           |               |
| DESCRIPTION | VARCHAR2(255) | OUI           |               |

```sql
CREATE TABLE CLASSES (
ID NUMBER NOT NULL PRIMARY KEY,
LIBELLE VARCHAR(20) NOT NULL,
DESCRIPTION VARCHAR(20) NOT NULL,
);
```

Créer une nouvelle table « FOURNISSEURS » dans le schéma TP2 comme suit :

| Nom colonne | Type données  | Null possible | Contrainte       |
| ----------- | ------------- | ------------- | ---------------- |
| ID          | NUMBER        | NON           | Clef primaire    |
| NOM         | VARCHAR2(20)  | NON           |                  |
| ADRESSE     | VARCHAR2(255) | NON           |                  |
| TELEPHONE   | VARCHAR2(16)  | OUI           |                  |
| EMAIL       | VARCHAR2(50)  | OUI           |                  |
| CEE         | VARCHAR2(3)   | NON           | CEE = NON ou OUI |

```sql
CREATE TABLE FOURNISSEURS (
    ID NUMBER NOT NULL PRIMARY KEY,
    NOM VARCHAR2(20) NOT NULL,
    ADRESSE VARCHAR2(255) NOT NULL,
    TELEPHONE VARCHAR2(16) NOT NULL,
    EMAIL VARCHAR2(50),
    CEE VARCHAR2(3) NOT NULL,
    CONSTRAINT CEE_CONSTRAINT
    CHECK (CEE IN ('OUI', 'NON'))
);
```

Créer une nouvelle table « PIECES » dans le schéma TP2 comme suit :

| Nom colonne | Type données  | Null possible | Contrainte                                 |
| ----------- | ------------- | ------------- | ------------------------------------------ |
| REFERENCE   | VARCHAR2(20)  | NON           | Clef primaire                              |
| FABRIQUANT  | VARCHAR2(20)  | NON           |                                            |
| DESCRIPTION | VARCHAR2(255) | NON           |                                            |
| FOURNISSEUR | NUMBER        | OUI           | Clef étrangère ID de la table FOURNISSEURS |
| TYPE        | NUMBER        | OUI           |                                            |

```sql
CREATE TABLE PIECES (
    REFERENCE VARCHAR2(20) NOT NULL PRIMARY KEY,
    FABRIQUANT VARCHAR2(20) NOT NULL,
    DESCRIPTION VARCHAR(255) NOT NULL,
    FOURNISSEUR NUMBER,
    TYPE NUMBER,
    CONSTRAINT FK_FOURNISSEUR
    FOREIGN KEY (FOURNISSEUR)
    REFERENCES FOURNISSEURS (ID)
);
```

Créer une nouvelle table « STOCKS » dans le schéma TP2 comme suit :

| Nom colonne     | Type données | Null possible | Contrainte            |
| --------------- | ------------ | ------------- | --------------------- |
| REF_PIECE       | VARCHAR2(20) | NON           | Clef primaire         |
| QUANTITE        | NUMBER       | NON           | DEFAUT = 0            |
| LOCALISATION    | NUMBER       | OUI           |
| DATE_INVENTAIRE | DATE         | OUI           | DEFAUT = Date du jour |

La valeur par défaut est à définir après le type de données mais avant la contrainte [NOT] NULL.
La syntaxe est : DEFAULT expression

```sql
CREATE TABLE STOCKS(
    REF_PIECE VARCHAR2(20) NOT NULL PRIMARY KEY,
    QUANTITE NUMBER DEFAULT 0 NOT NULL,
    LOCALISATION NUMBER ,
    DATE_INVENTAIRE DATE DEFAULT SYSDATE
);
```

```sql
CREATE TABLE INTERVENTIONS (
    NO_INTERVENTION VARCHAR2(20) NOT NULL PRIMARY KEY,
    REFERENCE_PEC VARCHAR2(20)
    INTERVENANT NUMBER(*,0) NOT NULL,
    DETAIL VARCHAR2(255),
    DATE_INTERVENTION DATE,
    TEMPS_PASSE NUMBER(5,2)
    CONSTRAINT REFERENCE_PEC_FK
    FOREIGN KEY (REFERENCE_PEC)
    REFERENCES PRISES_EN_CHARGE (REFERENCE)
    CONSTRAINT INTERVENANT
    FOREIGN KEY (REFERENCE_PEC)
    REFERENCES SALARIES (MATRICULE)

);
```

## 9.2 Modification des tables

### 1)

Modification de la table STOCKS le type de données de la colonne QUANTITE doit être NUMBER(5,0).

```sql
ALTER TABLE STOCKS MODIFY(QUANTITE NUMBER(5,0));
```

### 2)

    Ajouter une contrainte à la colonne CIVILITE de la table CLIENTS pour vérifier que sa valeur est « M. » ou « MME ».

```sql
ALTER TABLE CLIENTS MODIFY(CIVILITE CHECK(CIVILITE in('M.' , 'MME')));
```

### 3)

Ajouter une contrainte à la colonne CIVILITE de la table SALARIES pour vérifier que sa valeur est « M. » ou « MME ».

```sql
ALTER TABLE SALARIES MODIFY(CIVILITE CHECK(CIVILITE in('M.' , 'MME')));
```

### 4)

Ajouter une contrainte à la table PRISES_EN_CHARGE pour vérifier que DATE_FIN est supérieure DATE_DEBUT.

```sql
ALTER TABLE PRISES_EN_CHARGE ADD CHECK(DATE_FIN > DATE_DEBUT);
```

### 5)

Ajouter la contrainte STOCKS_PIECES_FK à la table STOCKS : la colonne REF_PIECE est une clef étrangère de la colonne REFERENCE de la table PIECES.

```sql
ALTER TABLE STOCKS ADD CONSTRAINT STOCKS_PIECES_FK FOREIGN KEY (REF_PIECE) REFERENCES PIECES(REFERENCE)
```

## 9.3 Renommage d’une table

### 1)

Renommer la table PIECES en « PIECES_DETACHEES ».

```sql
RENAME PIECES TO PIECES_DETACHES
```

## 9.4 Suppression d’une table

### 1)

Supprimer la table STOCKS.

```sql
DROP TABLE STOCKS;
```
