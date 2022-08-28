# Simplilearn

## 1

The three types of data models:

- Physical data model - This is where the framework or schema describes how data is physically stored in the database.
  - **the what kind of database, how much disk,etc**
- Conceptual data model - This model focuses on the high-level, user’s view of the data in question
  - **MDC: modèle conceptuel de données**
- Logical data models - They straddle between physical and theoretical data models, allowing the logical representation of data to exist apart from the physical storage.
  - **MDL: modele logique de donnees**

## 2

A table consists of data stored in rows and columns. Columns, also known as fields, show data in vertical alignment. Rows also called a record or tuple, represent data’s horizontal alignment.

## 3

Database normalization is the process of designing the database in such a way that it reduces data redundancy without sacrificing integrity.

## 4. What Does a Data Modeler Use Normalization For?

The purposes of normalization are:

Remove useless or redundant data
Reduce data complexity
Ensure relationships between the tables in addition to the data residing in the tables
Ensure data dependencies and that the data is stored logically.

## 5

Denormalization is a technique where redundant data is added to an already normalized database. **The procedure enhances read performance by sacrificing write performance.**

## 6. What Does ERD Stand for, and What is it?

ERD stands for Entity Relationship Diagram and is a logical entity representation, defining the relationships between the entities. Entities reside in boxes, and arrows symbolize relationships.

## 7

A surrogate key, also known as a primary key , enforces numerical attributes. This surrogate key replaces natural keys. Instead of having primary or composite primary keys, data modelers create the surrogate key, which is a valuable tool for identifying records, building SQL queries, and enhancing performance.
