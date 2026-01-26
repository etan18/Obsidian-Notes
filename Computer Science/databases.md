A database **transaction** is the base unit of work when interacting with the database. Depending on your use case, a single transaction may encompass multiple queries or operations with the database.

A well designed database will capture the four properties of the **ACID** acronym in all transactions:
- **Atomicity**: a transaction is either completed fully or not at all. A transaction may not leave the system in a state of data loss or corruption.
- **Consistency**: transactions only make changes to tables in predefined, predictable ways.
- **Isolation**: when multiple users are reading and writing from the same table all at once, isolation of their transactions ensures that the concurrent transactions don't interfere with or affect one another.
- **Durability**: changes to your data made by successfully executed transactions will be saved, even in the event of system failure.

## SQL databases
[[SQL]] databases (e.g. MySQL, PostgreSQL) are also known as **relational databases**. They are efficient with handling many tables of structured data, which are each defined by a schema. However, the primary drawback is that SQL databases are difficult to scale horizontally due to their relational nature. **Horizontal scaling** in [[distributed systems]] involves adding more servers in order to share the load more manageably across resources.

**NoSQL** (e.g. MongoDB, DynamoDB) was introduced to address the horizontal scaling problems of traditional SQL. It is a non-relational database which
- Does not support table relationships, and data is usually stored in documents or as key-value pairs. This makes them more flexible and easy to set up.
- Typically designed for write-heavy and/or distributed systems
- Does not guarantee strong consistency, rather only eventual consistency. This means that updates to replicas of the data may take longer, resulting in potentially stale reads.
Data can be stored in NoSQL databases in many different forms, including JSON, key-value pairs, tables with rows and dynamic columns, or nodes and edges. This can be unstructured or semi-structured data, as opposed to SQL DBs which store structured tables.

### online analytical processing
OLAP systems must aggregate data from a variety of sources so that it can be analyzed for reporting (e.g. business intelligence) or forecasting purposes. Because these are such common use cases, we have special databases called **data warehouses** which are optimized for analytics.