**Class**: [[Design and Analysis of Algorithms (DAA)]]

**Title:** Analysis Of Algorithms

**Date:** 06-08-2025

**Time:** 08:08

**Tags:** #DAA

# Topic

- How to analyse algorithms

---
# Keywords

- Time Complexity
- Space Complexity


--- 
# Notes

## Methods of Analysis

1. Time Complexity
2. Space Complexity
3. Network
4. Power Consumption
5. CPU Registers

### Time Analysis


```
Algorithm swap(a,b){ 
temp = a;
a = b;
b = temp;
}

#Time Complexity O(1) 
#Space Complexity O(1)
```


#### Frequency Count Method

```c
Algorithm sum(arr[],n){
S = 0; # 1 unit
for(i = 0; i < n; i++){ # n + 1
S = S + A[i]; # n
}
return S; # n 
}

# time complexity: O(n)
# space complexity: O(n)


```

**Matrix Addition**
```c

algorithm sumMatrix(arr1[],arr2[],n){
sum = 0;
for(i = 0; i < n; i++){
for(j = 0; j < n; j++){
res[i,j] = arr1[i,j]+ arr2[i,j]
}
}
return res;

}

# time complexity O(n^2)
```

**Matrix Multiplication**
```c
algo matMul(A[],B[],m,n){

for(i= 0 ; i < n; i++){
for(j = 0 ; j<m; j++){
res[i,j] = 0
for(k = 0; k< n ; k++){
res[i,j] = A[i,j] * B[j,i];
}}}
return res;
}


# time compelxity O(n^3)
# space complexity O(n^2)
```



---
# Work

- [ ] 

---
