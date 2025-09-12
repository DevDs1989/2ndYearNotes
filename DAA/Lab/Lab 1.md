Name: Devesh Chandra Srivastava
Sap ID: 590017127
Subject: [[Design and Analysis of Algorithms (DAA)]]

# Experiment 1: Implement the iterative and recursive Binary search tree and compare their performance

### Code
```c
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int recursive_binary_search(int arr[], int left, int right, int target) {
    if (left > right) {
        return -1;
    }
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) {
        return mid;
    } else if (arr[mid] > target) {
        return recursive_binary_search(arr, left, mid - 1, target);
    } else {
        return recursive_binary_search(arr, mid + 1, right, target);
    }
}

int iterative_binary_search(int arr[], int size, int target) {
    int left = 0;
    int right = size - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

void sort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {

    printf("Name: Devesh\nSap Id: 590017127\n");
    int size;
    printf("Enter the number of elements to insert:");
    scanf("%d", &size);
    int *arr = (int *)malloc(size * sizeof(int));
    for (int i = 0; i < size; i++) {
        arr[i] = i * 2;
    }
    for (int i = 0; i < size; i++) {
        arr[i] = rand() % (size * 2);
    }
    int target;
    target = arr[rand() % size];
    sort(arr, size);

    clock_t start, end;
    double cpu_time_used;

    start = clock();
    int result_recursive = recursive_binary_search(arr, 0, size - 1, target);
    end = clock();
    cpu_time_used = ((double)(end - start)) / CLOCKS_PER_SEC;
    if (result_recursive != -1) {
        printf("Recursive: Element found at index %d\n", result_recursive);
    } else {
        printf("Recursive: Element not found\n");
    }
    printf("Recursive Binary Search took %f seconds\n", cpu_time_used);

    start = clock();
    int result_iterative = iterative_binary_search(arr, size, target);
    end = clock();
    cpu_time_used = ((double)(end - start)) / CLOCKS_PER_SEC;
    if (result_iterative != -1) {
        printf("Iterative: Element found at index %d\n", result_iterative);
    } else {
        printf("Iterative: Element not found\n");
    }
    printf("Iterative Binary Search took %f seconds\n", cpu_time_used);

    free(arr);
    return 0;
}

```

### Results
![[Pasted image 20250905013336.png]]