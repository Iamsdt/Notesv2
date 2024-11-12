---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - neo4j
  - database
---


## Neo4j Introduction

**Playground:** https://sandbox.neo4j.com/

**I. Introduction**

* **What is Neo4j?**  A NoSQL graph database.  Stores data as nodes and relationships, unlike relational (SQL) databases that use tables.  Excellent for connected data (social networks, recommendations, knowledge graphs).  Faster for complex relationship traversals than relational joins.

* **Why Graphs?** Relationships are core.  Intuitive for connected data.  Efficient querying and navigation of relationships.  High performance for relationship-heavy tasks (e.g., "friends of friends").

* **Key Concepts:**
    * **Nodes:** Entities (person, product, city).
    * **Relationships:** Connections between nodes ("KNOWS," "BOUGHT"). Always have a direction.
    * **Properties:** Key-value pairs on nodes/relationships (name, age, price).
    * **Labels:** Node categories (:Person, :Product). Used for grouping/filtering.
    * **Direction:**  Alice KNOWS Bob ≠ Bob KNOWS Alice.


**II. Setup**

* **Neo4j Desktop (Recommended):** Download, install, manage local Neo4j instances.  (Provide documentation link).
* **Neo4j Sandbox (Faster):** Cloud-based temporary instances. Requires signup. (Provide link).
* **Neo4j Browser:** Web interface for Cypher queries, visualization, database management. (Typically `http://localhost:7474/browser/` for local).

**III. Cypher – The Query Language**

* **Basics:**
    * `CREATE`: Create nodes/relationships (`CREATE (p:Person {name: "Alice"})`).
    * `MATCH`: Find nodes/relationships (`MATCH (p:Person) RETURN p`).
    * `RETURN`: Specify output (`RETURN p.name`).
    * `WHERE`: Filter (`MATCH (p:Person) WHERE p.age > 25 RETURN p`).
    * merge: you can merge data if its available
```
MERGE (p:Person {name:"Alice"}) 
ON CREATE SET p.age = 25
ON MATCH SET p.last_updated = date()
```

* **Creating:**
    * Node: `CREATE (n:Person {name:"Bob", age:30})`
    * Relationship: `MATCH (alice:Person {name:"Alice"}), (bob:Person {name:"Bob"}) CREATE (alice)-[:KNOWS]->(bob)`

* **Filtering:**
    * By property: `MATCH (p:Person) WHERE p.name = "Alice" RETURN p`
    * Across relationships: `MATCH (p:Person)-[:KNOWS]->(f:Person) WHERE p.name = "Alice" RETURN f`

* **Traversing:**
    * Outgoing: `MATCH (p:Person)-[:KNOWS]->(f) RETURN f`
    * Incoming: `MATCH (p:Person)<-[:KNOWS]-(f) RETURN f`
    * Any direction: `MATCH (p:Person)-[:KNOWS]-(f) RETURN f`  (Explain arrow direction).

* **Optional Matches:** `MATCH (p:Person {name:"Alice"}) OPTIONAL MATCH (p)-[:KNOWS]->(f) RETURN p, f` (Returns Alice even without a "KNOWS" relationship).


**IV. Hands-on: Movie Database**

* **Filtering:**
    1. Specific movie:  `MATCH (m:Movie {title: 'Apollo 13'}) RETURN m`
    2. Counting: How many movies did Tom Hanks act in? `MATCH (p:Person {name:"Tom Hanks"})-[:ACTED_IN]->(m:Movie) RETURN count(m)`
    3. OR operator: Find movies with Tom Hanks or Kevin Bacon: `MATCH (p:Person)-[:ACTED_IN]->(m:Movie) WHERE p.name = "Tom Hanks" OR p.name = "Kevin Bacon" RETURN m`
    4. Using DISTINCT: List the distinct genres in the database: `MATCH (m:Movie) RETURN DISTINCT m.genre`
    5. Ordering: List movies by release date: `MATCH (m:Movie) RETURN m ORDER BY m.released DESC`
    6. Limiting results: Show only the top 3 oldest movies: `MATCH (m:Movie) RETURN m ORDER BY m.released ASC LIMIT 3`
    7. Collecting results: Get all actors in a list for a specific movie: `MATCH (m:Movie {title:"Apollo 13"})<-[:ACTED_IN]-(a:Person) RETURN m.title, collect(a.name) AS actors`

- Relationship
    1. Actors in movie (any direction): `MATCH (m:Movie {title: 'Apollo 13'})-[:ACTED_IN]-(p:Person) RETURN p`
    2. Movies by Tom Hanks: `MATCH (p:Person {name: 'Tom Hanks'})-[:ACTED_IN]->(m:Movie) RETURN m`
    3. Apollo 13 actors' other movies: `MATCH (m:Movie {title: 'Apollo 13'})<-[:ACTED_IN]-(p:Person)-[:ACTED_IN]->(other:Movie) RETURN other`
    4. Apollo 13 actors who also directed: `MATCH (m:Movie {title: 'Apollo 13'})<-[:ACTED_IN]-(p:Person)-[:DIRECTED]->(other:Movie) RETURN other`
    5. Who directed and acted in the same movie? `MATCH (p:Person)-[:DIRECTED]->(m:Movie)<-[:ACTED_IN]-(p) RETURN p, m`

- Recommendation Engine (Simple)
movies similar to "Apollo 13" based on shared actors
```cypher
MATCH (m:Movie {title:"Apollo 13"})<-[:ACTED_IN]-(a:Person)-[:ACTED_IN]->(other:Movie)
WHERE other.title <> "Apollo 13" // Exclude the original movie
RETURN other.title, count(a) AS sharedActors
ORDER BY sharedActors DESC  // Order by the number of shared actors
LIMIT 5 // Limit to top 5 recommendations
```
