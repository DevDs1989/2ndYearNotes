**Name:** Devesh Chandra Srivastava
**SAP ID:** 590017127
**Subject:** [[Design and Analysis of Algorithms (DAA)]]

### Code
```c
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

typedef struct Matrix {
        int rows, cols;
        int **data;
} Matrix;

void init_matrix(Matrix *m, int rows, int cols) {
    m->rows = rows;
    m->cols = cols;
    m->data = (int **)malloc(rows * sizeof(int *));
    for (int i = 0; i < rows; i++) {
        m->data[i] =
            (int *)calloc(cols, sizeof(int));o
    }
}

void free_matrix(Matrix *m) {
    for (int i = 0; i < m->rows; i++) {
        free(m->data[i]);
    }
    free(m->data);
}

void print_matrix(Matrix *m, int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d ", m->data[i][j]);
        }
        printf("\n");
    }
}

void standard_multiply(Matrix *a, Matrix *b, Matrix *result) {
    for (int i = 0; i < a->rows; i++) {
        for (int j = 0; j < b->cols; j++) {
            result->data[i][j] = 0;
            for (int k = 0; k < a->cols; k++) {
                result->data[i][j] += a->data[i][k] * b->data[k][j];
            }
        }
    }
}

void add_matrix(Matrix *a, Matrix *b, Matrix *result, int size) {
    for (int i = 0; i < size; i++)
        for (int j = 0; j < size; j++)
            result->data[i][j] = a->data[i][j] + b->data[i][j];
}

void sub_matrix(Matrix *a, Matrix *b, Matrix *result, int size) {
    for (int i = 0; i < size; i++)
        for (int j = 0; j < size; j++)
            result->data[i][j] = a->data[i][j] - b->data[i][j];
}

// Only for square matrices with size as power of 2
void strassen_multiply(Matrix *a, Matrix *b, Matrix *result) {
    int n = a->rows;
    if (n == 1) {
        result->data[0][0] = a->data[0][0] * b->data[0][0];
        return;
    }
    int k = n / 2;

    Matrix a11, a12, a21, a22, b11, b12, b21, b22;
    Matrix m1, m2, m3, m4, m5, m6, m7, aResult, bResult;
    init_matrix(&a11, k, k);
    init_matrix(&a12, k, k);
    init_matrix(&a21, k, k);
    init_matrix(&a22, k, k);
    init_matrix(&b11, k, k);
    init_matrix(&b12, k, k);
    init_matrix(&b21, k, k);
    init_matrix(&b22, k, k);
    init_matrix(&m1, k, k);
    init_matrix(&m2, k, k);
    init_matrix(&m3, k, k);
    init_matrix(&m4, k, k);
    init_matrix(&m5, k, k);
    init_matrix(&m6, k, k);
    init_matrix(&m7, k, k);
    init_matrix(&aResult, k, k);
    init_matrix(&bResult, k, k);

    for (int i = 0; i < k; i++) {
        for (int j = 0; j < k; j++) {
            a11.data[i][j] = a->data[i][j];
            a12.data[i][j] = a->data[i][j + k];
            a21.data[i][j] = a->data[i + k][j];
            a22.data[i][j] = a->data[i + k][j + k];

            b11.data[i][j] = b->data[i][j];
            b12.data[i][j] = b->data[i][j + k];
            b21.data[i][j] = b->data[i + k][j];
            b22.data[i][j] = b->data[i + k][j + k];
        }
    }
    add_matrix(&a11, &a22, &aResult, k);
    add_matrix(&b11, &b22, &bResult, k);
    strassen_multiply(&aResult, &bResult, &m1);

    add_matrix(&a21, &a22, &aResult, k);
    strassen_multiply(&aResult, &b11, &m2);

    sub_matrix(&b12, &b22, &bResult, k);
    strassen_multiply(&a11, &bResult, &m3);

    sub_matrix(&b21, &b11, &bResult, k);
    strassen_multiply(&a22, &bResult, &m4);

    add_matrix(&a11, &a12, &aResult, k);
    strassen_multiply(&aResult, &b22, &m5);

    sub_matrix(&a21, &a11, &aResult, k);
    add_matrix(&b11, &b12, &bResult, k);
    strassen_multiply(&aResult, &bResult, &m6);

    sub_matrix(&a12, &a22, &aResult, k);
    add_matrix(&b21, &b22, &bResult, k);
    strassen_multiply(&aResult, &bResult, &m7);

    Matrix c11, c12, c21, c22;
    init_matrix(&c11, k, k);
    init_matrix(&c12, k, k);
    init_matrix(&c21, k, k);
    init_matrix(&c22, k, k);

    add_matrix(&m1, &m4, &aResult, k);
    sub_matrix(&aResult, &m5, &bResult, k);
    add_matrix(&bResult, &m7, &c11, k);

    add_matrix(&m3, &m5, &c12, k);
    add_matrix(&m2, &m4, &c21, k);
    sub_matrix(&m1, &m2, &aResult, k);
    add_matrix(&aResult, &m3, &bResult, k);
    add_matrix(&bResult, &m6, &c22, k);

    for (int i = 0; i < k; i++) {
        for (int j = 0; j < k; j++) {
            result->data[i][j] = c11.data[i][j];
            result->data[i][j + k] = c12.data[i][j];
            result->data[i + k][j] = c21.data[i][j];
            result->data[i + k][j + k] = c22.data[i][j];
        }
    }

    free_matrix(&a11);
    free_matrix(&a12);
    free_matrix(&a21);
    free_matrix(&a22);
    free_matrix(&b11);
    free_matrix(&b12);
    free_matrix(&b21);
    free_matrix(&b22);
    free_matrix(&m1);
    free_matrix(&m2);
    free_matrix(&m3);
    free_matrix(&m4);
    free_matrix(&m5);
    free_matrix(&m6);
    free_matrix(&m7);
    free_matrix(&aResult);
    free_matrix(&bResult);
    free_matrix(&c11);
    free_matrix(&c12);
    free_matrix(&c21);
    free_matrix(&c22);
}

void fill_matrix_with_number(Matrix *m, int n, int num) {
    for (int i = 0; i < m->rows; i++)
        for (int j = 0; j < m->cols; j++)
            if (i < n && j < n)
                m->data[i][j] = num;
            else
                m->data[i][j] = 0;
}

int next_power_of_two(int n) {
    int res = 1;
    while (res < n)
        res <<= 1;
    return res;
}

int main(int argc, char *argv[]) {
    int n = argc > 1 ? atoi((char *)argv[1]) : 4;
    int N = next_power_of_two(n);

    printf("name: devesh\nsap id: 590017127\n");
    printf("Size of matrix: %d x %d\n", n, n);

    Matrix a, b, result_standard, result_strassen;
    init_matrix(&a, N, N);
    init_matrix(&b, N, N);
    init_matrix(&result_standard, N, N);
    init_matrix(&result_strassen, N, N);

    fill_matrix_with_number(&a, n, 1);
    fill_matrix_with_number(&b, n, 1);

    clock_t start, end;
    double time_standard, time_strassen;

    start = clock();
    standard_multiply(&a, &b, &result_standard);
    end = clock();
    time_standard = (double)(end - start) / CLOCKS_PER_SEC;

    start = clock();
    strassen_multiply(&a, &b, &result_strassen);
    end = clock();
    time_strassen = (double)(end - start) / CLOCKS_PER_SEC;

    printf("Time taken by Standard Multiplication: %f seconds\n",
           time_standard);
    printf("Time taken by Strassen Multiplication: %f seconds\n",
           time_strassen);

    // Uncomment to print matrix
    printf("Standard Result\n");
    print_matrix(&result_standard, n);
    printf("Strassen Result\n");
    print_matrix(&result_strassen, n);



    free_matrix(&a);
    free_matrix(&b);
    free_matrix(&result_standard);
    free_matrix(&result_strassen);

    return 0;
}

```
### Result

![[Pasted image 20250911234514.png]]