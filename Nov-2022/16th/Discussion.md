### Meeting with Semih summary

Focus is on Shortest Path algorithms in Relational context, Kuzu being a relational system at its core (a relational graph database).  
Look at some other systems like Neo4j, TigerGraph, Memgraph, especially from the query perspective.

Front end stuff - query language support, syntax for shortest path  
How from the query language is the shortest path query being expressed ?  
The edges, weights, any assumptions about the weights (is -ve allowed or only +ve weights) ? Are all the edges just '1' as in is it just a shortest hop query ?  
What kind of algorithms are being supported (A*, Dijkstra, Bellman-Ford, Bi-directional BFS) ?  
Is the edge weight a static property of the edge table (like a column) ? Or can it be defined on the fly ?  
Type of the query that is allowed, which type:

- single source, single destination (sssd)
- ss, all destinations (ssad)
- all pairs shortest path (quadratic in output)
- ss, multiple destinations (ssmd)
- arbitrary (any other type supported)

What is being returned after the query finishes executing ? Output type: Kuzu doesn't have a `Path` type, is that required ?  
Is the output being "_bound_" to a variable ? Is the return value a _cost_ value i.e Double type ?  


