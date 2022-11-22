## Query Syntax

There seem to be 2 formats being supported:

1) CALL and YIELD syntax  (graph data science library)

`CALL gds.graph.project(
'myGraph2',
'Loc',
'ROAD',
{
relationshipProperties: 'cost'
}
)`  
A Graph Projection is created first, with the type of source and destination nodes specified, and the type of edge required.  
In this example *Loc* is the node type, *ROAD* is the edge type, and the property *cost* of ROAD will be used to measure cost.  
Essentially keeps a subset of the entire graph for using next.  
This graph projection is created because the implementation is *homogeneous*, it cannot distinguish between different types of nodes and vertices.  
If 2 edges with the same cost property existed it would have considered either of them when finding the shortest path.  

`MATCH (source:Loc {name: 'A'}), (target:Loc {name: 'F'})  
CALL gds.shortestPath.dijkstra.stream('myGraph2', {  
sourceNode: source,  
targetNode: target,  
relationshipWeightProperty: 'cost'  
})  
YIELD index, sourceNode, targetNode, totalCost, nodeIds, costs, path  
RETURN  
index,  
gds.util.asNode(sourceNode).name AS sourceNodeName,  
gds.util.asNode(targetNode).name AS targetNodeName,  
totalCost,  
[nodeId IN nodeIds | gds.util.asNode(nodeId).name] AS nodeNames,  
costs,  
nodes(path) as path  
ORDER BY index`  
Using CALL the function is invoked and using YIELD which variables are required is specified.  
Multiple variables are returned and only the required ones can be filtered. Also returns the `Path` variable. In this format there is no one single 
explicitly bound variable and instead multiple variables. The total cost is of type `float`.   

2) Bound variable syntax (shortestPath call)

`MATCH p = shortestPath((A)-[:ROAD*]->(F)) WHERE A.name = 'A' and F.name = 'F' WITH length(p) > 1 return p;`  
Here 'p' is the bound variable, its type is `Path`. Does a bidirectional BFS.  
Doesn't consider the weight of the Edges, just finds the "shortest hop" meaning least no. of edges between the source and the destination.  

## Edge and Weight

For case 2), the edge is to be specified in the Match pattern (undirected or directed can be indicated there). This case doesn't consider +ve or -ve edge weights.  
It just considers the least no. of edges required to get from source and destination.  
For case 1), `relationshipWeightProperty` is used to specify the property as weight of path. There is _no_ facility to _define it on the fly_.  
+ve Edge weight is supported for the following implementations:
- Delta-Stepping Single-Source Shortest Path (find the shortest path, but if multiple shortest paths are there, no guarantee which one will be shown)
- Dijkstra source-target shortest path (single thread algo, delta is multithreaded)
- Dijkstra single-source shortest path
- A* shortest path (heuristics to find next node)
- Yen's algorithm shortest path (top k shortest paths)  
Negative weights is not supported for any of the shortest path algorithms in the library. They recommend normalizing the -ve weights and then apply  
their library algos.  

## Algorithms supported

Along with the above mentioned (all +ve weighted edges), APSP is also supported.  

## Query type allowed (sssd, ssad, etc.)  

single source-single target, single source-all targets, all source-all targets, single source-single target-top k shortest path  
arbitrary target nodes is not supported

## Return type (`Path` or `Double`)

An explicit `Path` is used, consists of the source node, target node, and `Segments`. Each segment represents an edge on the path, has the backward node,  
forward node and the edge weight specified. Also the length property (no. of edges present in the path).   
`Float` is being used to represent the `Total cost` metric for the path.  
