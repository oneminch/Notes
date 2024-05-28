---
alias: DB
---
## Concepts

- Playlist: https://www.youtube.com/playlist?list=PLQnljOFTspQXjD0HOzN7P2tgzu7scWpl2
- Article: https://dev.to/basementdevs/database-for-newbies-n46
## Introduction

- Databases 
    - are structured digital information stores
    - build indices to efficiently query data
    - define relationships between datasets
- Every database has a way of structuring / organizing and interacting with this stored information: Database Management Systems (DBMS)
    - Fundamental ways of interacting with databases:
        - **C**reate
        - **R**ead
        - **U**pdate
        - **D**elete
        - Commonly known as CRUD
- DBMS's are mainly of two types:
    - **Relational**
        - organize data in tabular form with columns (categories / attributes) and rows (entries)
        - uses a structure that allows us to identify and access data in relation to another piece of data in the database. 
        - often, data is organized into tables.
        - highly structured
        - strict data types
        - great for complex datasets
        - SQL is used to interact with them
        - a schema needs to be defined before putting anything into a database
          - ![[Database Schema]]
        - well known DBMS for these include MySQL & PostgreSQL.
    - **Non-relational** - which is also known as NoSQL; SQL is not used to interact with them.
        - generally more flexible and less strict
        - creating a schema isn't necessary
        - ideal for decentralised / distribured networks of data
        - e.g. graph, key-value, document
        - well known DBMS for these include MongoDB.

## Relational Databases

- **Primary Key**
    - A field which uniquely identifies each row/record in a database table.
    - Must contain unique, non-NULL values
    - A table can only have one composed on single or multiple fields (*composite key*).
    - Generally created while the database and table are created, but can also be created after a table is created.
- **Foreign Key**
    - aka *referencing key*.
    - Used to link two tables together.
    - A column or combination of columns whose values match a primary key in a different table.



- [Cloudflare D1](https://developers.cloudflare.com/d1)
- [CockroachDB](https://www.cockroachlabs.com/product/)
- [Neon](https://neon.tech/)
- [PlanetScale](https://planetscale.com/)
- [Supabase](https://supabase.com/database)
## Non-relational (NoSQL) Databases

### Document Databases

- [MongoDB](https://www.mongodb.com/)
### Key-Value Databases

- [Redis](https://redis.io/)
- [Upstash](https://upstash.com/)
- [Vercel KV](https://vercel.com/storage/kv)
## Data Modelling

## Indexing

## Data Integrity

## ORMs

- [Prisma](https://www.prisma.io/)
- [Sequelize](https://sequelize.org/)
## Transactions

- ACID

## Normalization

## Graph Databases

- [Dgraph](https://dgraph.io/)
## Multi-model Databases ==?==

## CMS

## Local-First Apps

- ElectricSQL

- TinyBase

---
## Further

### Books 📚

- Seven Databases in Seven Weeks (Eric Redmond)

### Learn 🧠

- [Prisma's Data Guide](https://www.prisma.io/dataguide)

### Reads 📄

- [A Shelfish Starter Guide to Databases](https://maggieappleton.com/databases)

### Videos 🎥

- [7 Database Paradigms - Fireship (YouTube)](https://youtube.com/watch?v=W2Z7fbCLSTw)

