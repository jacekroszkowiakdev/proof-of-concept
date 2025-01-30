# Database Decision Guide for Large Projects

READ:

1. [Relational vs. Document Database: Key Differences & Examples](https://atlan.com/relational-vs-document-database/)
2. [What is Azure Database for PostgreSQL - Flexible Server?](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/service-overview)
3. [Azure Cosmos DB](https://azure.microsoft.com/pl-pl/products/cosmos-db)
4. [Top 6 ORM for modern Node.js App Development](https://amplication.com/blog/top-6-orms-for-modern-nodejs-app-development)
5. [Draw  ERD - Entity Rrelationship Diagram](https://www.lucidchart.com/pages/er-diagrams)

## Step 1: Understand Project Requirements

**NOTE**: Not all questions may apply, at least at the early stage of the project.
We should discuss that with the team, but ideas and questions are welcome.

1. **Data Structure**:
   - Structured and relational, or semi-structured/unstructured?
   Jacek: Structured and relational, with transactions following ACID compliance.

2. **Data Relationships**:
   - Complex relationships (e.g., many-to-many)?
   - Are joins and constraints critical?

3. **Data Volume**:
   - Current and future growth?

4. **Read/Write Pattern**:
   - Read-heavy, write-heavy, or balanced?
   - Real-time data processing needed?

5. **Query Complexity**:
   - Complex queries (e.g., joins, aggregations)?
   Jacek: expected, data model will be created to show this.
   - Simple lookups by key? 
   Jacek: No.

6. **Scalability Needs**:
   - Vertical (single server) or horizontal (distributed)?
   Jacek: Postgres can be scalled both vertical and horizontal, there are middleware and plugins available to support horizontal scalling.
   - Global distribution?
   Jacek: To be decided, but possible with PostgreSQL

7. **Performance Expectations**:
   - Latency and throughput requirements.
   Jacek: Topic needs subject matter expert 

8. **Transactions and Consistency**:
   - ACID compliance needed? 
   Jacek: Yes, ACID compliance is essential, as transactions—particularly payments—must adhere to these principles to ensure reliability, consistency, and integrity throughout the process
   - Eventual consistency acceptable?
   Jacek: strong consistency ensures robust data integrity and is required for this project.


9. **Budget Constraints**:
   - Open-source/free or managed/commercial solutions?
   Jacek: PostgreSQL chosen for it's other strenghts, but is also open-source. 

10. **Tech Stack Integration**:
    - Compatibility with your frameworks and tools?
    Jacek: PostgreSQL is a mature soluton with rich ecosutem and community support. Is designed to work in any cloud, and is consider a best option from the cost standpoint.
    - ORM or query tool support?
    Jacek: Prisma ORM was decides based on familarity and recomendations as best solution (followed by TypeORM)

---

## Step 2: Research Database Options

1. **Relational Databases**:
   - Examples: PostgreSQL, MySQL, MariaDB, Oracle, SQL Server.
   - Best for structured, relational data with complex queries.
   Jacek: After thorough research and consultation with a senior database specialist, PostgreSQL was selected as the preferred choice.

2. **NoSQL Databases**:
   - Types:
     - Document Stores: MongoDB, Couchbase.
     - Key-Value Stores: Redis, DynamoDB.
     - Columnar: Cassandra, HBase.
     - Graph: Neo4j, Amazon Neptune.
   - Best for flexible schema and scalability.
   Jacek: Despite these advantages, PostgreSQL was chosen due to its robust support for structured and semi-structured data (via JSON/JSONB), ACID compliance, strong community support, and the ability to handle complex queries while still being scalable for many use cases.

3. **NewSQL Databases**:
   - Combines relational features with horizontal scalability.
   - Examples: CockroachDB, Google Spanner.
   Jacek: However, the team lacks familiarity with NewSQL databases, making them less practical to implement and maintain effectively in the current setup.

4. **Managed vs. Self-Hosted**:
   - **Managed**: AWS RDS, MongoDB Atlas – reduces operational burden.
   - **Self-Hosted**: Full control but more maintenance effort.
   Jacek: To be decided.

---

## Step 3: Evaluate Key Criteria

1. **Scalability**:
   - Horizontal (e.g., MongoDB, Cassandra) vs. Vertical (e.g., PostgreSQL).
   Jacek: Postgres can be scalled both vertical and horizontal.

2. **Performance**:
   - Low-latency/high-throughput: NoSQL (e.g., Redis).
   - Complex queries: Relational DBs (e.g., PostgreSQL).
   Jacek: Complex queries are expected given the project size and goals.

3. **Community and Ecosystem**:
   - Active community for support?
   - Tools for monitoring, backups, etc.?
   Jacek: Topic needs subject matter expert, but I'd say it's needed, yes.

4. **Learning Curve**:
   - Team familiarity or willingness to learn?
   Jacek: Team is faimiliar with Relational DB and query language. Official docs and AI to support development.

5. **Backup and Disaster Recovery**:
   - Automated backups, replication, failover support?
   Jacek: To be decided later, I suggest a main DB with failover Replica for maximum resilence and minimum downtime.

6. **Licensing**:
   - Open-source vs. proprietary.
   Jacek: PostgreSQL was chosen. 

---

## Step 4: Prototype and Test

1. **Create a Proof of Concept (POC)**:
   - Set up a small-scale prototype with PostgreSQL. 

2. **Benchmarking**:
   - Test for query speed, transaction latency, and scalability.
   Jacek: Later in the project if needed, but PostgreSQL performance is more than sufficient.

3. **Evaluate Operational Simplicity**:
   - Check ease of setup, configuration, monitoring, and maintenance. 
   Jacek: PostgreSQL is not complicated to setup, docs and AI are great help. Monitoring and maintenance should also be no problem as this is mature, proved DB solution.

4. **Simulate Failure Scenarios**:
   - Test handling of downtime, replication, and recovery.
   Jacek: DB main and DB replica as resilient and secure solution. To be discussed if our own deployment or popular cloud solutons i.e AWS or Azure. 

---

## Step 5: Compare Based on Use Cases

| **Use Case**                                   | **Best Choice**                                    |
|-----------------------------------------------|---------------------------------------------------|
| Complex relationships, data integrity         | Relational DB (e.g., PostgreSQL, MySQL)           |
| Flexible schema, fast writes, horizontal scale | NoSQL (e.g., MongoDB, DynamoDB)                  |
| Low-latency key-value caching                 | Redis, Memcached                                 |
| Time-series data                              | InfluxDB, TimescaleDB                            |
| Large-scale analytics                         | BigQuery, Snowflake                              |
| Highly concurrent, geographically distributed | CockroachDB, Cassandra                           |
| Graph-based relationships                     | Neo4j, Amazon Neptune                            |

---

## Step 6: Make a Final Decision

1. **Prioritize Key Requirements**:
   - Match database strengths to your project needs.

2. **Plan for Long-Term Scalability**:
   - Choose a database that supports projected growth.

3. **Document Your Decision**:
   - Write a rationale explaining the choice. **IN PROGRESS**
   - Include considerations for future migrations and scaling. **Jacek: Topic needs subject matter expert**


