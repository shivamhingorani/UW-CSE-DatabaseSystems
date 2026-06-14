# CSE 414: Introduction to Database Systems

**Institution:** University of Washington  
**Term:** Fall 2019

---

## About the Course

CSE 414 is a broad introduction to relational database theory and practice, covering the spectrum from writing SQL queries on day one to designing distributed big data pipelines by the end of the quarter. The course is organized around a core question that reappears at every level: *how do we store, retrieve, and reason about large collections of structured data efficiently and correctly?*

The assignments progress from the foundations of the relational model through the theory underlying schema design, into application-level programming against a live database, and finally into distributed systems designed to handle data at a scale where a single relational database is no longer sufficient.

---

## Topics Covered

### Relational Model and Basic SQL
The course opens with the relational model: relations as sets of tuples, schemas, keys, and the semantics of the SQL `SELECT`-`FROM`-`WHERE` block. Early assignments cover `CREATE TABLE`, `INSERT`, and single-table queries with projections, filters, and sorting, using small hand-crafted datasets to isolate query semantics cleanly before scaling up.

### Joins, Aggregation, and the Flights Dataset
The bulk of the SQL curriculum is developed against a real-world flight database — a normalized schema spanning carriers, routes, months, and weekday dimensions joined against a table of individual flight records. Assignments here cover `JOIN` across multiple tables, grouped aggregation with `GROUP BY` and `HAVING`, and queries that answer analytical questions: which carriers have the worst on-time records, which routes are most congested on Mondays, and how cancellation rates vary by season.

### Advanced SQL and Cloud Databases
Later SQL assignments introduce correlated subqueries, `EXISTS`/`NOT EXISTS` predicates, and multi-level aggregation patterns — queries that require reasoning about groups of groups. The course also moves from local SQLite to **Azure SQL Server** as the DBMS, providing hands-on experience with a cloud-hosted relational system and prompting a written reflection on the practical differences between local and cloud execution.

### Query Languages Beyond SQL
A dedicated unit steps back from SQL to examine the *formal foundations* of relational querying. **Relational algebra** — selection (σ), projection (π), join (⋈), union (∪), set difference (−), and rename (ρ) — is the mathematical model that underlies every SQL query optimizer. **Datalog** is introduced as a logic-programming alternative that makes recursive queries (transitive closure, reachability) naturally expressible as rules over base relations, something standard SQL handles awkwardly. Assignments bridge all three representations.

### Database Theory: Functional Dependencies and Normalization
The theoretical core of schema design. A relation with hidden redundancy is analyzed using **functional dependencies** (FDs): inference rules (Armstrong's axioms), attribute closure computation, and candidate key identification. The goal is **BCNF decomposition** — a principled process of splitting a relation into smaller relations that eliminate update anomalies while preserving a lossless join. A SQL component validates the decomposition against the `mrFrumble` dataset.

### Application Programming with JDBC
The programming capstone of the course is a full command-line **flight booking application** backed by Azure SQL Server, built in Java using JDBC. Beyond query execution, this assignment confronts the challenges of multi-user database applications: `SERIALIZABLE` transaction isolation to prevent double-booking, `setAutoCommit(false)` with explicit commit/rollback, and retry logic for deadlock handling. The application implements user login, flight search (direct and one-stop), seat booking, payment, reservations listing, and cancellation with refund.

### Big Data: MapReduce and Spark
When a single relational database is insufficient, distributed computing takes over. This unit covers the **MapReduce programming model** — mapper, combiner, reducer — as a framework for parallelizing analytical queries across clusters. **Apache Spark** is introduced as a higher-level abstraction over MapReduce, with RDD and DataFrame APIs that eliminate the boilerplate of raw MapReduce while retaining its scalability. Jobs run both locally and on **Amazon EMR** (Elastic MapReduce), and the assignment compares SQL, MapReduce, and Spark for the same analytical queries on Parquet-formatted flight data.

### NoSQL and Semi-Structured Data with AsterixDB
The course closes by examining what happens when data doesn't fit neatly into tables. **AsterixDB** is a parallel DBMS for JSON-like semi-structured data; its **SQL++** query language extends standard SQL to handle nested objects, collection-valued attributes, and heterogeneous records. Queries run against the *Mondial* world database — countries, cities, rivers, and political entities with deeply nested and multi-valued fields that would require unwieldy schema gymnastics to model relationally.

---

## Repository Structure

```
CSE 414/
├── HW1/    Basic SQL: DDL, DML, single-table queries
├── HW2/    Joins and aggregation on the flights dataset
├── HW3/    Advanced subqueries and Azure SQL Server
├── HW4/    Datalog and relational algebra
├── HW5/    Functional dependencies and BCNF normalization
├── HW6/    JDBC flight booking application
├── HW7/    MapReduce and Spark on Amazon EMR
└── HW8/    AsterixDB / SQL++ on the Mondial dataset
```

Each subdirectory is a public wrapper containing a README and a private `src/` submodule with the source code and submission materials.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| SQL (SQLite / Azure SQL Server) | Primary query language; local and cloud DBMS |
| Datalog | Logic-programming query language |
| Java + JDBC | Application-layer database programming (HW6) |
| Apache Spark | Distributed data processing (HW7) |
| Amazon EMR | Cloud cluster execution for MapReduce/Spark (HW7) |
| Maven | Java build system (HW6, HW7) |
| AsterixDB / SQL++ | NoSQL system for semi-structured data (HW8) |
