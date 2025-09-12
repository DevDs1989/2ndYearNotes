![[frontpage_page-0001.jpg]]
<br><br> 
**Submitted By:**
**Name:** Devesh Chandra Srivastava
**SAP ID:** 590017127
**Subject:** [[Design and Analysis of Algorithms (DAA)]]

# Experiment Title
N activities with their start time and end time are given, WAP to find the solution set having maximum number of non conflicting activities that can be executed within the given time, assuming only a single activity can be performed at a given time.
### Code

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
        int start, end;
} Activity;

typedef struct {
        Activity *arr;
        int size;
        int capacity;
} MinHeap;

void swap(Activity *a, Activity *b) {
    Activity temp = *a;
    *a = *b;
    *b = temp;
}

void heapifyUp(MinHeap *heap, int i) {
    while (i > 0) {
        int parent = (i - 1) / 2;
        if (heap->arr[parent].end <= heap->arr[i].end)
            break;
        6 Activity 1 : 5 8 Activity 2 : 1 3 Activity 3 : 9 12 Activity 4
            : 2 6 Activity 5 : 4 5 Activity 6
            : 7 10 swap(&heap->arr[i], &heap->arr[parent]);
        i = parent;
    }
}

void heapifyDown(MinHeap *heap, int i) {
    while (1) {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        int smallest = i;

        if (left < heap->size && heap->arr[left].end < heap->arr[smallest].end)
            smallest = left;
        if (right < heap->size &&
            heap->arr[right].end < heap->arr[smallest].end)
            smallest = right;

        if (smallest == i)
            break;

        swap(&heap->arr[i], &heap->arr[smallest]);
        i = smallest;
    }
}

void insert(MinHeap *heap, Activity activity) {
    heap->arr[heap->size] = activity;
    heapifyUp(heap, heap->size);
    heap->size++;
}

Activity extractMin(MinHeap *heap) {
    Activity min = heap->arr[0];
    heap->size--;
    if (heap->size > 0) {
        heap->arr[0] = heap->arr[heap->size];
        heapifyDown(heap, 0);
    }
    return min;
}

int main() {
    int n;
    printf("Enter number of activities: ");
    scanf("%d", &n);

    MinHeap heap;
    heap.arr = malloc(n * sizeof(Activity));
    heap.size = 0;
    heap.capacity = n;

    for (int i = 0; i < n; i++) {
        Activity a;
        printf("Activity %d (start end): ", i + 1);
        scanf("%d %d", &a.start, &a.end);
        insert(&heap, a);
    }

    int count = 0, lastEnd = -1;
    printf("\nSelected activities:\n");
    while (heap.size > 0) {
        Activity current = extractMin(&heap);
        if (current.start >= lastEnd) {
            count++;
            printf("Activity: (%d, %d)\n", current.start, current.end);
            lastEnd = current.end;
        }
    }

    printf("\nMaximum activities selected: %d\n", count);
    free(heap.arr);
    return 0;
}

```

### Result