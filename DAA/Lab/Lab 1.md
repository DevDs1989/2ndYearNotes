Name: Devesh Chandra Srivastava
Sap ID: 590017127
Subject: [[Design and Analysis of Algorithms (DAA)]]

# Experiment 1: Implement the iterative and recursive Binary search tree and compare their performance

### Code
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>

typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
} Node;

Node* createNode(int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

void insert(Node** root, int data) {
    Node* newNode = createNode(data);
    if (*root == NULL) {
        *root = newNode;
        return;
    }
    
    Node* current = *root;
    Node* parent = NULL;
    
    while (current != NULL) {
        parent = current;
        if (data < current->data) {
            current = current->left;
        } else {
            current = current->right;
        }
    }
    
    if (data < parent->data) {
        parent->left = newNode;
    } else {
        parent->right = newNode;
    }
}

bool search(Node* root, int data) {
    while (root != NULL) {
        if (data == root->data) {
            return true;
        } else if (data < root->data) {
            root = root->left;
        } else {
            root = root->right;
        }
    }
    return false;
}

bool recursiveSearch(Node* root, int data) {
    if (root == NULL) {
        return false;
    }
    if (data == root->data) {
        return true;
    } else if (data < root->data) {
        return recursiveSearch(root->left, data);
    } else {
        return recursiveSearch(root->right, data);
    }
}

void freeTree(Node* root) {
    if (root != NULL) {
        freeTree(root->left);
        freeTree(root->right);
        free(root);
    }
}

int main() {
    Node* root = NULL;
    int n, i, data;
    
    printf("Name: Devesh\nSap Id: 590017127\n");
    printf("Enter the number of elements to insert: ");
    scanf("%d", &n);
    
    srand(time(NULL));
    
    // Insert random elements into the BST
    for (i = 0; i < n; i++) {
        data = rand() % 10000; 
        insert(&root, data);
    }

    
    // Measure performance of iterative search
    clock_t start = clock();
    for (i = 0; i < n; i++) {
        data = rand() % 100;
        search(root, data);
    }
    clock_t end = clock();
    double iterativeTime = (double)(end - start) / CLOCKS_PER_SEC;
    
    // Measure performance of recursive search
    start = clock();
    for (i = 0; i < n; i++) {
        data = rand() % 100;
        recursiveSearch(root, data);
    }
    end = clock();
    double recursiveTime = (double)(end - start) / CLOCKS_PER_SEC;
    
    printf("Iterative search time: %f seconds\n", iterativeTime);
    printf("Recursive search time: %f seconds\n", recursiveTime);
    
    freeTree(root);
    
    return 0;
}

```

### Results
![[Pasted image 20250905013336.png]]