<!-- 

---

### 

.

**Input:**
<br>

<br>

**Output:**
<br>

<br>

**Explanation:** 

Step 1: 
Step 2:
Step 3: 

```


```
 -->

# 300 Questions-Code
---

### [Kadane's Algorithm](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0)

Given an array arr of N integers. Find the contiguous sub-array(containing at least one number) which has the maximum sum and return its sum.

**Input:**<br>
N = 5
arr[] = {1,2,3,-2,5}
<br>

**Output:**<br>
9

```C++

int maxSubarraySum(int arr[], int n) {

        int current = 0;                      //This stores value of current elements
        int maximum = INT_MIN;                //The maximum value of a sub array is kept here
        for(int i=0; i<n; i++) {
            current = current + arr[i];       //Add arr[i] in current to store sum of next element
            if(current>maximum) {             //If current > maximum, store current in maximum
                maximum = current;             
            }
            if(current < 0) {                 //Edge Case
                current = 0;
            }
        }
        return maximum;
    }

```

---

### [Merge Overlapping Intervals](https://www.geeksforgeeks.org/merging-intervals/)

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

**Input:**<br> intervals = [[1,3],[2,6],[8,10],[15,18]]
<br>

**Output:**<br> [[1,6],[8,10],[15,18]]<br>
**Explanation:** Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

Case 1:
           a ----------- b
start -------------------------- end

Case 2:
                   a ----------------------------- b
start -------------------------- end

Case 3:
a ----------------------------- b
              start -------------------------- end

```python

def mergeoverlappingintervals(arr, n):
    answer = []
    arr.sort()
    start = arr[0][0]
    end = arr[0][1]

    for i in range(1, n):
        # Case 1 - Start and End remains same
        if (arr[i][0]>=start and arr[i][1]<=end):
            continue
        # Case 2 - Start remains same but b becomes End
        elif (arr[i][0]>=start and arr[i][1]>=end and arr[i][0]<=end):
            end = arr[i][1]
        # Case 3 - a becomes Start but End remains same
        elif (arr[i][0]<=start and arr[i][1]<=end and arr[i][0]<=end):
            start = arr[i][0]
        else:
            answer.append([start, end])
            start = arr[i][0]
            end = arr[i][1]
    answer.append([start, end])
    return answer

```

---

### [Duplicates in an array](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/)

Given an array a[] of size N which contains elements **from 0 to N-1**, you need to find all the elements occurring more than once in the given array.

**Input:**
<br>
N = 5
a[] = {2,3,1,2,3}
<br>

**Output:**<br> 2 3 

Step 1: First check all the values that are present in an array then go to that values as indexes and increment by the size of array.
Step 2: Now check which value exists more than once by dividing with the size of array.

```python

def printRepeating(arr, n):
 
    for i in range(0, n):
        index = arr[i] % n
        arr[index] += n
 
    for i in range(0, n):
        if (arr[i]/n) >= 2:
            print(i)

```

---

### [Set Matrix Zeros](https://leetcode.com/problems/set-matrix-zeroes/)

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's, and return the matrix.

**Input:**
<br> 
matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
<br> 

**Input:**
<br>
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]

Step 1: Iterate through first column to check if it has 0 or not.

**0** | 1 | 2 | 0  
---|---|---|---
3 |   |   |   
1 |   |   |   

Step 2: Iterate through 2nd column. If any element is 0 in the matrix make the values at index 0 in first row and column.

**0** | 1 | 2 | **0**
---|---|---|---
3 |   |   |   
1 |   |   |   

Step 3: Traverse backwards and if the first row and column contains 0, set the value of arr[i][j] = 0.

**0** | **1** | **2** | **0**  
---|---|---|---
**3** | 4 | 5 | **2**  
**1** | 3 | 1 | **5**  

```python

def setZeroes(arr):
    row = len(arr)
    col = len(arr[0])
    #Flag is to check wether the first column has 0 or not
    flag = True               

    for i in range(row):
        if(arr[i][0] == 0):
            flag = False

        for j in range(1, col): 
            if(arr[i][j] == 0):
                arr[i][0] = arr[0][j] = 0
    
    for i in range(row-1, -1, -1):
        for j in range(col-1, 0, -1):
            if(arr[i][0] == 0 or arr[0][j] == 0):
                arr[i][j] = 0
        if flag == False:
            arr[i][0] = 0

    return arr

```

---

### [Pascal Triangle](https://leetcode.com/problems/pascals-triangle/)



```python

def pascalstriangle(n):
    flag = 1
    temp = []
    arr = []
    for i in range(n):
        temp = []
        for j in range(i+1):
            if(j==0 or i==0):
                flag = 1
                temp.append(flag)
            else:
                flag = flag*(i-j+1)//j
                temp.append(flag)
        arr.append(temp)
    return arr

```

---

### [Next Permutation](https://practice.geeksforgeeks.org/problems/next-permutation/0)

Implement the next permutation, which rearranges the list of numbers into Lexicographically next greater permutation of list of numbers. If such arrangement is not possible, it must be rearranged to the lowest possible order i.e. sorted in an ascending order. You are given an list of numbers arr[ ] of size N.

**Input:**
<br>
N = 6
arr = {1, 2, 3, 6, 5, 4}
<br>

**Output:**
<br>
{1, 2, 4, 3, 5, 6}
<br>

**Explanation:** The next permutation of the 
given array is {1, 2, 4, 3, 5, 6}.

Step 1: 
Step 2:
Step 3: 

```


```



