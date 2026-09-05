# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE:
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

<img width="757" height="563" alt="image" src="https://github.com/user-attachments/assets/6847540f-804c-4f7a-81a0-6837c2caf537" />


## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.
