# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE:
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

<img width="907" height="615" alt="image" src="https://github.com/user-attachments/assets/02bd6a26-e082-4888-87e1-ad53116db74f" />


## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
