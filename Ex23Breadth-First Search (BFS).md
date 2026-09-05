# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE:
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

<img width="892" height="482" alt="image" src="https://github.com/user-attachments/assets/d434edf8-fcc1-42f3-9057-62d4ae2b0208" />


## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.
