# A-Star

## How to install
Add these 2 lines in your html file:
```html
<script src="p5.js"></script>
<script src="pathfinder.js"></script>
```

## How to use
### Declaring
First of all you have to declare an instance of the Pathfinder class like this:
```javascript
let pathfinder = new Pathfinder(60, 30, 20, true, Pathfinder.euclideanDistance);
```
The line above creates an 60x30 grid with 20pixel nodes where each node is walkable. The 4th parameter specifies whether the path can move diagonally or not. The 5th parameter is used to specify the distance function used. There are 2 built-in ones:  
- Pathfinder.euclideanDistance
- Pathfinder.manhattanDistance  

However, you can build your own. The function must take take (x1, y1, x2, y2) as arguements and return a number
### Adding unwalkable nodes
You can start adding unwalkable nodes like this:
```javascript
pathfinder.addUnwalkableNode(15, 8);
```
The line above declares that the pathfinder can not walk on the node with position (x=15, y=8).  

You can also create rectangles with:  
```javascript
pathfinder.addUnwalkableRect(20, 13, 5, 10);
```  
This creates an unwalkable rectangle in position (x=20, y=13) with 5 width and 10 height
**Note** that adding obstacles is optional.
### Finding path
Firstly you should specify what the start and target nodes are. You can do so with:
```javascript
pathfinder.setStartNode(5, 3);
pathfinder.setTargetNode(25, 14);
```
You can start finding paths simply by:
```javascript
let nodesList = pathfinder.getPath();
```
This will return a list of all the nodes that make up the path. The start position is (x=5, y=3) and the target position is (x=25, y=14). You can then access the position of the nodes with
```javascript
nodesList[i].x
nodesList[i].y
```
**Note** that if the target node is unreachable then an empty list is returned.  
**Note** that if the target node happens to be an unwalkable node then an empty list is returned.
### Visualizing
There are a couple of functions that handle this and you have 2 options.
1) Simple way:  
```javascript
pathfinder.drawEverything();
```
**Note** that this should be called after the ```pathfinder.getPath()``` has been called.

2) Advanced way:  
```javascript
node.draw(); // Draws a single node with the correct color
pathfinder.drawUnwalkableNodes(); // Draws all unwalkable nodes
pathfinder.drawClosedTiles(); // Draws all the nodes in the closed list
pathfinder.drawOpenTiles(); // Draws all the nodes in the open list
pathfinder.drawPathTiles(); // Draws all the nodes generated by the path
```
