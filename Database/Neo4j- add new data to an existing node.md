---
Created by: Shudipto Trafder
Created time: 2023-10-19T12:29
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:10
tags:
  - Graph
  - neo4j
---
Goal;

1. Add new company_id into an existing node

```Shell
MATCH (n:Candidate {cid: $cid}) SET n.company_id = $company_id"
```

  

```Python
from neo4j import GraphDatabase
import psycopg2

# Neo4j connection details
neo4j_uri = "bolt://localhost:7687"
neo4j_user = ""
neo4j_password = ""

# PostgreSQL connection details
pg_host = "localhost"
pg_database = ""
pg_user = ""
pg_password = ""

# Batch size for fetching data from Neo4j
batch_size = 100

# Cypher query to fetch data from Neo4j in batches
neo4j_query = "MATCH (n:Candidate) RETURN n SKIP $skip LIMIT $limit"

# PostgreSQL query to fetch company_id based on candidate_id
# select company_id from t_candidate_cvs where cid = {cid}
pg_query = "SELECT company_id FROM t_candidate_cvs WHERE cid = %s"


# Neo4j driver class
class Neo4jDriver:
    def __init__(self, uri, user, password):
        self.driver = GraphDatabase.driver(uri, auth=(user, password))

    def close(self):
        self.driver.close()

    def fetch_data(self, skip, limit):
        with self.driver.session() as session:
            result = session.run(neo4j_query, skip=skip, limit=limit)
            return [record["n"] for record in result]


# PostgresSQL connection function
def get_pg_connection():
    return psycopg2.connect(
        host=pg_host, database=pg_database, user=pg_user,
        password=pg_password,
        port=5432,
    )


# Main function to update Neo4j nodes with company_id from PostgresSQL
def update_neo4j_nodes():
    neo4j_driver = Neo4jDriver(neo4j_uri, neo4j_user, neo4j_password)
    pg_connection = get_pg_connection()

    skip = 0
    while True:
        print(f"Fetching data from Neo4j with skip={skip} and limit={batch_size}")
        # Fetch data from Neo4j in batches
        neo4j_data = neo4j_driver.fetch_data(skip, batch_size)
        if not neo4j_data:
            break

        print(f"Updating {len(neo4j_data)} nodes in Neo4j")
        for node in neo4j_data:
            candidate_id = node.get("cid")  # Assuming 'cid' is the candidate_id property in Neo4j
            with pg_connection.cursor() as cursor:
                cursor.execute(pg_query, (candidate_id,))
                company_id = cursor.fetchone()

            if company_id:
                # Update Neo4j node with company_id
                with neo4j_driver.driver.session() as session:
                    session.run("MATCH (n:Candidate {cid: $cid}) SET n.company_id = $company_id",
                                cid=candidate_id, company_id=company_id[0])

        print(f"Updated {len(neo4j_data)} nodes in Neo4j")
        skip += batch_size

    neo4j_driver.close()
    pg_connection.close()


if __name__ == "__main__":
    update_neo4j_nodes()
```

Automate Notes  
Bidirectional Links  
Code-Clipboard  
Day Review  
Enhancement  
Templates  
Tagging