# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE:
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

<img width="788" height="442" alt="image" src="https://github.com/user-attachments/assets/3abe0f34-3ed9-494d-a612-5f312787ca2e" />


## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.
