## Meeting with Guodong, Ziyi & Xiyang

For shortest path, vertex with multiple labels should be supported (because source and target vertex may have multiple labels so any one of them can be in the path).  
Edges with single labels -> Only this should be supported (multiple labels must not be supported)  

Weight type for property of the Edge -> Only INT or DOUBLE. Only +ve weights for edge weights (This will be initial design), and only support edge property as weights  
on the path, and not node property as weights (because the syntax of Memgraph which supports this is a bit unclear, the property of the destination vertex gets ignored).  

### Syntax for Shortest Path

_MATCH (a:person), (b:person) WHERE a.name='Alice' AND b.name='Bob' WITH **SHORTESTPATH(a, knows, b) AS p RETURN p**_  
This will require creating a separate Data type called `Path` (NO separate `Node` and `Relationship` is required, we will keep the IDs inside the `Path`)  
This is for unweighted shortest path, an extension of this syntax where we take the weight property as input for weighted will be there.  
If we consider the plan for this query, it should be something like this:  
Scan -> Filter -> Cartesian Product -> Shortest Path Physical Operator

### Data Type for Path

The Path data type is required and will be composed of alternate node and edge IDs, -
[source_vertex_ID, edge_rel_1_ID, vertex_2_ID, ... , dest_vertex_ID]  
`PATH` == `LIST[uint64_t]`  

### Path forward (steps to implement shortest path)

Initial implementation will be based only on _single source_ and _single target_.  

1) Create the `Path` data type

As discussed above, create with the same template

2) Implement the basic shortest path operator:

`shortestPath(ValueVector<nodeID_t> src, ValueVector<nodeID_t> dst, table_ID relLabel, rel_property_ID weightProperty)`  
Here the `src` and `dst` will contain just 1 node ID. The storage API will be used to read from the tables.  

3) Concept proof for large scale datasets:

After we have the "baseline", we will keep testing for larger and larger datasets to see how performant it is and decide the next step forward.
