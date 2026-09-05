# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE:
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


<img width="675" height="440" alt="image" src="https://github.com/user-attachments/assets/9b816f8e-3e47-4549-988b-886b5e41b52d" />


<img width="536" height="457" alt="image" src="https://github.com/user-attachments/assets/b745116a-4983-4b50-ad8c-b137c70c366e" />



## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.
