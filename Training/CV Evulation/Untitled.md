Next day:
1. Neo4j intro
2. 3rd party Payment Gate, how its work and security
3. Azure and GCP, AWS Services


What we missed?
1. API request with large payload how to optimize it
Solution:
1. Data Compression
2. Chunking Data (Pagination or Streaming)
3. Use Efficient Data Formats
4. Avoid Redundant Data
5. Batching Requests
6. Payload Splitting and Resumable Uploads

### Missed?
given an array of the string, create map
1. SQL Query Optimization

A request go through all the service, how do you identify how service performing
Use Distributed Tracing
Implement Monitoring and Metrics (Service-Level Metrics)
Analyze Logs (Centralized Logging)



## Payment Security
https://stripe.com/resources/more/payment-security

A nice cheat sheet of different databases in cloud services
https://www.veritis.com/blog/aws-vs-azure-vs-gcp-the-cloud-platform-of-your-choice/
https://cloud.google.com/docs/get-started/aws-azure-gcp-service-comparison

## Neo4j Introduction
Playground: https://sandbox.neo4j.com/
**I. Introduction**

* **What is Neo4j?**
	A NoSQL database, specifically a *graph* database. Stores data as nodes and relationships, unlike relational databases (SQL) that use tables, rows, and columns.
    * Analogy: Think of a social network – people are nodes, and their connections (friendships) are relationships.  Good for connected data: social networks, recommendations, knowledge graphs, fraud detection, network analysis.
    * Contrast with relational databases:  Joins can be slow for complex relationships, graph databases excel at traversing relationships.

* **Why Graphs?**
     Relationships are first-class citizens – makes querying and navigating connections efficient. Intuitive modeling – closer to how we think about connected data. Performance advantage for relationship-heavy queries (compared to relational joins).
    * Example: Finding "friends of friends" is much easier in a graph database.

* **Key Concepts:**
    * **Nodes:** Represent entities (e.g., a person, a product, a city).
    * **Relationships:** Connect nodes, representing the connection between them (e.g., "KNOWS," "BOUGHT," "LOCATED_IN").  Always have a direction.
    * **Properties:** Key-value pairs that store information about nodes and relationships (e.g., name, age, price, date).
    * **Labels:**  Categories or tags for nodes (e.g., :Person, :Product).  Allow grouping and filtering.
    * **Direction:** Relationships have a direction (e.g., Alice KNOWS Bob is different from Bob KNOWS Alice).

**II. Setting Up

* **Neo4j Desktop (Recommended):**
    * Download and install Neo4j Desktop (show steps or provide documentation link).  Allows creating and managing local Neo4j instances.
* **Neo4j Sandbox (Alternative):**
    * For quicker setup, use Neo4j Sandbox (show link).  Cloud-based, temporary instances. Requires signup.
* **Neo4j Browser:**
    * Explain: The web-based interface for interacting with Neo4j. Used to write and execute Cypher queries, visualize the graph, and manage the database.
    * Show how to access the browser (usually at `http://localhost:7474/browser/` for local instances).

**III. Cypher - The Query Language**

* **Basic Syntax:**
    * **CREATE:**  Create nodes and relationships. `CREATE (p:Person {name: "Alice"})`
    * **MATCH:** Find existing nodes and relationships.  `MATCH (p:Person) RETURN p`
    * **RETURN:** Specify what data to return.  `RETURN p.name`
    * **WHERE:** Filter results.  `MATCH (p:Person) WHERE p.age > 25 RETURN p`

* **Creating Nodes and Relationships:**
    * `CREATE (n:Person {name:"Bob", age:30})`
    * `MATCH (alice:Person {name:"Alice"}), (bob:Person {name:"Bob"}) CREATE (alice)-[:KNOWS]->(bob)`

* **Filtering:**
    * `MATCH (p:Person) WHERE p.name = "Alice" RETURN p`
    * `MATCH (p:Person)-[:KNOWS]->(f:Person) WHERE p.name = "Alice" RETURN f`

* **Traversing Relationships:**
    * `MATCH (p:Person)-[:KNOWS]->(f) RETURN f` (Outgoing relationship)
    * `MATCH (p:Person)<-[:KNOWS]-(f) RETURN f` (Incoming relationship)
    * `MATCH (p:Person)-[:KNOWS]-(f) RETURN f` (Any direction)
    * Emphasize the arrow direction in the query and how it affects results.


* **Optional Matches:**
    * `MATCH (p:Person {name:"Alice"}) OPTIONAL MATCH (p)-[:KNOWS]->(f) RETURN p, f` (Returns Alice even if she doesn't know anyone)

**IV. Hands-on Coding Exercises
* **Movie Database Example:**
Filtering:
1. Get specific movies
```cypher
match (m:Movie)
where m.title = 'Apollo 13'
return m
```

```cypher
match (m:Movie {title: 'Apollo 13'})
return m
```

2. Find all the actor for the movie

- Any Direction
```
match (m:Movie {title: 'Apollo 13'}) - [:ACTED_IN] - (p:Person)
return m, p
```

- Incoming Relationship
```
match (m:Movie {title: 'Apollo 13'}) <- [:ACTED_IN] - (p:Person)
return m, p
```

- Outgoing Relation ship

```
match (p:Person {name: 'Tom Hanks'}) - [:ACTED_IN] -> (m:Movie)
return m, p
```

- Find Apollo 13 actor/actress movies
```
match (m:Movie {title: 'Apollo 13'}) <- [:ACTED_IN] - (p:Person) - [:ACTED_IN] - (other:Movie)
return m, p, other
```

Find any actor who directed other movies
```
match (m:Movie {title: 'Apollo 13'}) <- [:ACTED_IN] - (p:Person) - [:DIRECTED] - (other:Movie)
return m, p, other
```