# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE:  12.09.2026
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node

## Algorithm
1. Define the Node structure: Create a class Node containing an integer data value, and pointers to the left and right children.
2. Construct the Binary Tree:
   a. Use a Queue to build the tree from the level-order input array.Insert the first element as the root and push it into the queue.
   b. For each subsequent pair of elements in the input, pop a node from the queue and assign them as its left and right children (ignoring placeholders like -1 for null nodes). Enqueue valid children.
3. Target the Left Subtree: Check if the root or root.left is null. If root.left is null, the count is 0.
4. Count the Nodes: Pass root.left into a recursive helper function countNodes(Node node). If the current node is null, return 0; otherwise, return 1 + countNodes(node.left) + countNodes(node.right).
5. Display the Result: Print the calculated number of nodes present in the left subtree.
  

## Program:
```
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class Node {
    int data;
    Node left, right;

    // Constructor
    public Node(int data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }

    // Method to construct a binary tree from level order input array
    public static Node constructTree(int[] levelOrder) {
        if (levelOrder.length == 0 || levelOrder[0] == -1) {
            return null;
        }

        Node root = new Node(levelOrder[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        int i = 1;
        while (!queue.isEmpty() && i < levelOrder.length) {
            Node current = queue.poll();

            // Left child
            if (i < levelOrder.length && levelOrder[i] != -1) {
                current.left = new Node(levelOrder[i]);
                queue.add(current.left);
            }
            i++;

            // Right child
            if (i < levelOrder.length && levelOrder[i] != -1) {
                current.right = new Node(levelOrder[i]);
                queue.add(current.right);
            }
            i++;
        }
        return root;
    }

    // Helper method to count total nodes in a given tree/subtree
    public static int countNodes(Node node) {
        if (node == null) {
            return 0;
        }
        return 1 + countNodes(node.left) + countNodes(node.right);
    }

    // Main method is now inside the Node class
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter the number of elements in level order input:");
        int n = scanner.nextInt();

        int[] levelOrder = new int[n];
        System.out.println("Enter the level order elements (use -1 for empty/null nodes):");
        for (int i = 0; i < n; i++) {
            levelOrder[i] = scanner.nextInt();
        }

        Node root = constructTree(levelOrder);

        int leftSubtreeCount = 0;
        if (root != null && root.left != null) {
            leftSubtreeCount = countNodes(root.left);
        }

        System.out.println("Number of nodes in the left subtree: " + leftSubtreeCount);
        scanner.close();
    }
}

```

## Output:


<img width="385" height="185" alt="image" src="https://github.com/user-attachments/assets/e9a944e4-9c88-44d9-8fa7-63b9cab074a1" />



## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.




















# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE:  12.09.2026
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
## Algorithm
1. Define a Node class with attributes for the bookID, left child, and right child.
2. Implement an insert function to construct the Binary Search Tree (BST):
  a. If the tree is empty, create a new node as the root.
  b. If the new Book ID is less than the current node's ID, recursively insert it into the left subtree.
  c. If the new Book ID is greater than the current node's ID, recursively insert it into the right subtree.
3. Implement a search function to find a target Book ID:
  a. Start from the root node.
  b. If the current node is null, return false (not found).
  c. If the current node's ID matches the target, return true (found).
  d. If the target ID is less than the current node's ID, search in the left subtree.
  e. If the target ID is greater than the current node's ID, search in the right subtree.
4. Read the input values for the list of Book IDs and the specific Book ID to search for.
5. Construct the tree by inserting the Book IDs one by one, execute the search function, and print whether the Book ID exists in the BST.


## Program:
```
/*
Program to constructs a Binary Search Tree (BST) using given Book IDs 
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.Scanner;

class Node {
    int bookID;
    Node left, right;

    public Node(int id) {
        this.bookID = id;
        this.left = this.right = null;
    }
}

class BinarySearchTree {
    Node root;

    public BinarySearchTree() {
        root = null;
    }

    // Function to insert a new Book ID into the BST
    public void insert(int id) {
        root = insertRec(root, id);
    }

    private Node insertRec(Node root, int id) {
        if (root == null) {
            root = new Node(id);
            return root;
        }
        if (id < root.bookID) {
            root.left = insertRec(root.left, id);
        } else if (id > root.bookID) {
            root.right = insertRec(root.right, id);
        }
        return root;
    }

    // Function to search for a specific Book ID in the BST
    public boolean search(int id) {
        return searchRec(root, id);
    }

    private boolean searchRec(Node root, int id) {
        if (root == null) {
            return false;
        }
        if (root.bookID == id) {
            return true;
        }
        if (id < root.bookID) {
            return searchRec(root.left, id);
        }
        return searchRec(root.right, id);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        BinarySearchTree bst = new BinarySearchTree();

        System.out.print("Enter the number of books to insert: ");
        int n = scanner.nextInt();

        System.out.println("Enter the Book IDs:");
        for (int i = 0; i < n; i++) {
            int id = scanner.nextInt();
            bst.insert(id);
        }

        System.out.print("Enter the Book ID to search for: ");
        int searchId = scanner.nextInt();

        if (bst.search(searchId)) {
            System.out.println("Book ID " + searchId + " exists in the BST.");
        } else {
            System.out.println("Book ID " + searchId + " does not exist in the BST.");
        }

        scanner.close();
    }
}
```

## Output:


<img width="537" height="220" alt="image" src="https://github.com/user-attachments/assets/86628e72-22c6-4d88-b5a7-aaf7beba3a3c" />



## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.
























# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE:  12.09.2026
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Initialize an empty queue to store the junctions to be processed and a boolean array (or set) to track the visited junctions.
2. Mark the source junction as visited and insert (enqueue) it into the queue.
3. Repeat the following steps while the queue is not empty:
   a. Remove (dequeue) the front junction from the queue and print or record it as a reachable location.
4.Iterate through all the immediate neighboring junctions connected to the currently dequeued junction.
5.Check and update: If a neighboring junction has not been visited, mark it as visited and insert it into the queue to explore later.


## Program:
```
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.*;

public class CityMapBFS {
    private int vertices; // Number of junctions
    private List<List<Integer>> adjList; // Adjacency list

    // Constructor
    public CityMapBFS(int vertices) {
        this.vertices = vertices;
        adjList = new ArrayList<>(vertices);
        for (int i = 0; i < vertices; i++) {
            adjList.add(new ArrayList<>());
        }
    }

    // Method to add a road (edge) between two junctions
    public void addEdge(int src, int dest) {
        adjList.get(src).add(dest);
        adjList.get(dest).add(src); // Assuming bidirectional roads
    }

    // Method to find and display all reachable locations using BFS
    public void findReachableLocations(int source) {
        boolean[] visited = new boolean[vertices];
        Queue<Integer> queue = new LinkedList<>();

        visited[source] = true;
        queue.add(source);

        System.out.print("Reachable locations from junction " + source + ": ");

        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (int neighbor : adjList.get(current)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 1. Get the size of the city map
        System.out.print("Enter the total number of junctions: ");
        int totalJunctions = sc.nextInt();

        CityMapBFS map = new CityMapBFS(totalJunctions);

        System.out.print("Enter the total number of roads: ");
        int totalRoads = sc.nextInt();

        // 2. Get all road connections
        System.out.println("Enter the roads as pairs of connected junctions (e.g., '0 1'):");
        for (int i = 0; i < totalRoads; i++) {
            int src = sc.nextInt();
            int dest = sc.nextInt();
            map.addEdge(src, dest);
        }

        // 3. Get the starting point
        System.out.print("Enter the source junction to start BFS from: ");
        int sourceJunction = sc.nextInt();

        // 4. Run the traversal
        map.findReachableLocations(sourceJunction);

        sc.close();
    }
}

```

## Output:


<img width="475" height="293" alt="image" src="https://github.com/user-attachments/assets/50ec33d3-4e16-4073-a4ff-f8cd9122ee44" />


## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.






















# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE: 12.09.2026
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Initialize the Graph: Represent the heritage town map using an adjacency list where each attraction (node) maps to a list of its directly connected neighboring attractions.
2. Setup BFS Structures: Create a queue to manage the traversal order, a set to keep track of visited attractions to prevent cycles, and a map to store the distance (hop count) from the starting location.
3. Execute Breadth-First Search: Enqueue the starting attraction, mark it as visited, and set its distance to 0. While the queue is not empty, dequeue the front attraction and examine all its unvisited neighbors.
4. Update Metrics: For each unvisited neighbor, mark it as visited, set its distance to current_distance + 1, and enqueue it. Maintain a count of all unique attractions visited during this traversal.
5. Return and Display Results: Retrieve the minimum hops to the target attraction from the distance map (or report if unreachable). Output the total number of reachable attractions from the starting point.


## Program:
```
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.*;

public class HeritageTownBFS {
    // Graph representation using an Adjacency List
    private Map<String, List<String>> adjacencyList;

    public HeritageTownBFS() {
        this.adjacencyList = new HashMap<>();
    }

    // Method to add a walking path between two attractions (undirected graph)
    public void addPath(String source, String destination) {
        this.adjacencyList.putIfAbsent(source, new ArrayList<>());
        this.adjacencyList.putIfAbsent(destination, new ArrayList<>());
        this.adjacencyList.get(source).add(destination);
        this.adjacencyList.get(destination).add(source); 
    }

    // Method to perform BFS to find shortest hops and total reachability
    public void analyzePaths(String start, String target) {
        if (!adjacencyList.containsKey(start)) {
            System.out.println("\nError: Starting attraction '" + start + "' does not exist in the town map.");
            return;
        }

        // BFS Data Structures
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        Map<String, Integer> distances = new HashMap<>();

        // Initialize BFS
        queue.add(start);
        visited.add(start);
        distances.put(start, 0);

        int reachableCount = 0;

        while (!queue.isEmpty()) {
            String current = queue.poll();
            reachableCount++; // Count this attraction as reachable

            List<String> neighbors = adjacencyList.getOrDefault(current, new ArrayList<>());
            for (String neighbor : neighbors) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    distances.put(neighbor, distances.get(current) + 1);
                    queue.add(neighbor);
                }
            }
        }

        // Display Shortest Path (Minimum Hops)
        System.out.println("\n================ ANALYSIS RESULTS ================");
        if (distances.containsKey(target)) {
            System.out.println("Minimum hops from [" + start + "] to [" + target + "]: " + distances.get(target));
        } else {
            System.out.println("Target attraction [" + target + "] is NOT reachable from [" + start + "].");
        }

        // Display Total Reachable Attractions (excluding the starting point itself)
        System.out.println("Total other reachable attractions from [" + start + "]: " + (reachableCount - 1));
        System.out.println("==================================================");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        HeritageTownBFS townMap = new HeritageTownBFS();

        System.out.print("Enter the number of walking paths: ");
        int numPaths = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        System.out.println("Enter each path as 'Attraction1, Attraction2' (one per line):");
        for (int i = 0; i < numPaths; i++) {
            System.out.print("Path " + (i + 1) + ": ");
            String inputLine = scanner.nextLine();
            
            // Split by comma and trim whitespaces
            String[] parts = inputLine.split(",");
            if (parts.length == 2) {
                townMap.addPath(parts[0].trim(), parts[1].trim());
            } else {
                System.out.println("Invalid format. Please enter as: LocationA, LocationB");
                i--; // Retry this step
            }
        }

        System.out.print("\nEnter the starting attraction: ");
        String startingPoint = scanner.nextLine().trim();

        System.out.print("Enter the target attraction: ");
        String destinationPoint = scanner.nextLine().trim();

        // Run analysis
        townMap.analyzePaths(startingPoint, destinationPoint);
        
        scanner.close();
    }
}

```

## Output:

<img width="853" height="278" alt="image" src="https://github.com/user-attachments/assets/f20bf03b-e24a-4aaa-a370-075452a66e83" />



## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.





















# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE:12.09.2026
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1. Initialize the graph representation: Represent the network of city blocks as an adjacency matrix or adjacency list, where vertices are blocks and edge weights represent travel times.
2. Define the starting vertex (EV's current location) and a set of vertices representing charging stations.Setup distance tracking: Create a distance array dist[] initialized to infinity (\(\infty \)) for all blocks, except the source block which is set to 0. Create a boolean array visited[] initialized to false for all blocks to track processed locations.
3. Iterate through vertices: Loop through all blocks in the network. In each iteration, select an unvisited block \(u\) that has the minimum travel time value in dist[], and mark it as visited.
4. Update neighbor distances: For the selected block \(u\), update the distance of all its unvisited adjacent blocks \(v\). If the current distance to \(u\) plus the travel time from \(u\) to \(v\) is less than the existing dist[v], update dist[v] with this smaller value.
5. Find the nearest station: Compare the computed shortest travel times in dist[] for all designated charging station vertices. Identify the station with the smallest distance value and output both the destination and the minimum travel time.
 

## Program:
```
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.Arrays;
import java.util.Scanner;

public class EVShorterRouteUserInput {

    public static void findNearestChargingStation(int[][] graph, int V, int source, int[] chargingStations) {
        int[] dist = new int[V]; 
        boolean[] visited = new boolean[V]; 

        // Initialize all distances as INFINITY and visited[] as false
        Arrays.fill(dist, Integer.MAX_VALUE);
        Arrays.fill(visited, false);

        // Distance from source to itself is always 0
        dist[source] = 0;

        // Find shortest path for all vertices
        for (int count = 0; count < V - 1; count++) {
            int u = minDistance(dist, visited, V);
            if (u == -1) break; // Remaining vertices are unreachable

            visited[u] = true;

            for (int v = 0; v < V; v++) {
                if (!visited[v] && graph[u][v] != 0 && dist[u] != Integer.MAX_VALUE 
                        && dist[u] + graph[u][v] < dist[v]) {
                    dist[v] = dist[u] + graph[u][v];
                }
            }
        }

        // Determine the nearest charging station from the user-provided list
        int nearestStation = -1;
        int minTime = Integer.MAX_VALUE;

        for (int station : chargingStations) {
            if (station >= 0 && station < V && dist[station] < minTime) {
                minTime = dist[station];
                nearestStation = station;
            }
        }

        // Print results
        System.out.println("\n--- EV Routing Results ---");
        System.out.println("Current EV Location (Block): " + source);
        if (nearestStation != -1 && minTime != Integer.MAX_VALUE) {
            System.out.println("Nearest Charging Station found at Block: " + nearestStation);
            System.out.println("Shortest Travel Time: " + minTime + " minutes");
        } else {
            System.out.println("No reachable charging station found from your location.");
        }
    }

    private static int minDistance(int[] dist, boolean[] visited, int V) {
        int min = Integer.MAX_VALUE;
        int minIndex = -1;

        for (int v = 0; v < V; v++) {
            if (!visited[v] && dist[v] <= min) {
                min = dist[v];
                minIndex = v;
            }
        }
        return minIndex;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the total number of blocks in the city: ");
        int V = scanner.nextInt();

        int[][] graph = new int[V][V];
        System.out.println("\nEnter the adjacency matrix for travel times between blocks (" + V + "x" + V + "):");
        System.out.println("(Enter 0 if there is no direct road between two blocks)");
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                graph[i][j] = scanner.nextInt();
            }
        }

        System.out.print("\nEnter the current block location of the EV (0 to " + (V - 1) + "): ");
        int currentBlock = scanner.nextInt();

        System.out.print("Enter the number of charging stations available: ");
        int numStations = scanner.nextInt();

        int[] chargingStations = new int[numStations];
        System.out.print("Enter the block numbers of the charging stations separated by spaces: ");
        for (int i = 0; i < numStations; i++) {
            chargingStations[i] = scanner.nextInt();
        }

        // Execute routing algorithm
        findNearestChargingStation(graph, V, currentBlock, chargingStations);

        scanner.close();
    }
}

```

## Output:

<img width="467" height="393" alt="image" src="https://github.com/user-attachments/assets/1cc7c93a-65dd-453c-8197-6f4c87f3ed2f" />



## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
