documentation: https://fxdocs.github.io/docs/html5/
![[javafx_graph_arch.png]]
Stage -> Scene -> root
All elements in the JavaFX scene graph are represented as `Node` objects. 
There are three types of nodes: root, branch and leaf. 
The root node is the only node that does not have a parent and is directly contained by a scene, which can be seen in the figure above. 
The difference between a branch and a leaf is that a leaf node does not have children.
A node can have maximum one parent
