# Database Design

## Vocab

- Data: anything we store in the database
- Database: where we store data
- Relational Database: store things in tables
- Database Management System (DMS): how to control database
- RDBMS: how to control relational database
- Null: no value,  empty value in specific field
- Anomalies: errors in data integrity
- Entity: about thing that we store Ex. User, People
- Attributes: the data about entity we store Ex. Name, Age
- Relation: connect between 2 set of data
- Tuple: All attributes about entity, a row of the table
- File: another term of table
- Record: another term of row
- Field: another term of column
- Normalization: the process of building the best database design

## Why Database Design

- Data Integrity: Data is up to date and correct.
  - Entity Integrity: Uniqueness
  - Referential Integrity: Keep the connections across multiple tables
  - Domain Integrity: Acceptable Value of the Column

## Design Pattern

### Conceptual Design

- Unlimited Brain Storm Phrase
- More General
- How data is related

### Logical Design

### Physical

- More Specific

## Data Type

- Char(20): 20 bytes of string

## SQL

- Structured Query Language

## Keys

- Key is thing that make data unique
- Unique
- Never change
- Not null

### Primary Key

- Unique
- Never change
- Not null

### Foreign Key

- Use to connect relation between parent and child database

### Superkey

- not practical, for design only
  - can every row be unique
  - if yes, move to candidate key
  - how many columns are needed to make the row unique
  - how many candidate key do I have 

- any column that make row unique
- typically not defined in database

### Candidate Key

- the least column that make row unique
