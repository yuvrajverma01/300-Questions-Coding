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
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; a ----------- b  
start -------------------------- end

Case 2:  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; a ----------------------------- b  
start -------------------------- end

Case 3:  
a ----------------------------- b  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; start -------------------------- end

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

Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it.  

1  
1 1  
1 2 1  
1 3 3 1  
1 4 6 4 1  

**Input:**<br>
n = 5
<br>

**Output:**<br>
[[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

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

Step 1: Traverse the array backwards from **n-2** and check which a[i] < a[i+1]  
Step 2: If **i < 0** then reverse the array  
Step 3: Traverse backwards from **n-1** till **>i** and check if a[j] > a[i]  
Step 4: Swap the a[i] with a[j]  
Step 5: Reverse the array after a[i]  

```C++

vector<int> nextPermutation(int N, vector<int> arr){
    int i=0;
    int j = 0;
    N = arr.size();
    for(i=N-2; i>=0; i--) {
        if(arr[i] < arr[i+1]) {
            break;
        }
    }
    
    if(i<0) {
        reverse(arr.begin(), arr.end());
    } else {
        for(j = N-1; j>i; j--) {
            if(arr[j] > arr[i]) {
                break;
            }
        }
        swap(arr[i], arr[j]);
        reverse(arr.begin() + i + 1, arr.end());
    }
    return arr;
}

```

---

### [Inversion of Array](https://www.geeksforgeeks.org/counting-inversions/)

Given an array of integers. Find the Inversion Count in the array.  

**Inversion Count**: For an array, inversion count indicates how far (or close) the array is from being sorted. If array is already sorted then the inversion count is 0. If an array is sorted in the reverse order then the inversion count is the maximum. 
Formally, two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j.

**Input:**
<br>
N = 5  
arr[] = {2, 4, 1, 3, 5}
<br>

**Output:**
<br>
3
<br>

**Explanation:** The sequence 2, 4, 1, 3, 5 
has three inversions (2, 1), (4, 1), (4, 3).


```python

def mergeSort(arr, n):
    temp = [0]*n
    return _mergeSort(arr, temp, 0, n-1)

def _mergeSort(arr, temp, left, right):
    mid = 0
    count = 0

    if(right>left):
        mid = (right+left)//2
    
        count += _mergeSort(arr, temp, left, mid)
        count += _mergeSort(arr, temp, mid+1, right)

        count += merge(arr, temp, left, mid+1, right)
    return count

def merge(arr, temp, left, mid, right):
    i = left #Index for left subarray
    j = mid+1  #Index for right subarray
    k = left #Index for resultant merging array
    count = 0

    while((i<=mid) and (j<=right)):
        if arr[i]<=arr[j]:
            temp[k] = arr[i]
            k += 1
            i += 1
        else:
            temp[k] = arr[j]
            k += 1
            j += 1
            count = count + (mid-i)
    
    while (i<=mid-1):
        temp[k] = arr[i]
        k += 1
        i += 1
    while (j<=right):
        temp[k] = arr[j]
        k += 1
        j += 1
    for i in range(left, right+1):
        arr[i] = temp[i]
    return count

arr = [1, 2, 3]
n = len(arr)
print(mergeSort(arr, n))

```

---

### [Stock Buy and Sell](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

**Input:**
<br>
prices = [7,1,5,3,6,4]
<br>

**Output:**
<br>
5
<br>

**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.  

The theory is try to **sell out at max price** and keep **storing minimum** and check the difference between the **maximum and minimum**. 

**arr** = [3, 1, 4, 8, 7, 2, 5]  
  
min = [3 or **8**, 1 or **8**, 4 or **8**, **8** or 7, **7** or 5, 2 or **5**, **5**]
  
**max** = [8, 8, 8, 8, 7, 5, 5]

Step 1: Make minimum = arr[0] to store **current minimum value of stock**  
Step 2: Put the **arr[i] - minimum** into a **profit variable**  
Step 3: Then calculate **maximum of minimum element and profit** to find the **maximum profit in a certain window**

```C++

int maxProfit(vector<int>& arr) {
    int minimum = arr[0];
    int maximum = 0;
    int n = arr.size();
    for(int i=0; i<n; i++) {
        minimum = min(minimum, arr[i]);
        int profit = arr[i] - minimum;
        maximum = max(maximum, profit);
        
    }
    
    return maximum;
}

```

---
### [Rotate Matrix](https://www.geeksforgeeks.org/rotate-a-matrix-by-90-degree-in-clockwise-direction-without-using-any-extra-space/)

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Input:**
<br>
matrix = [[1,2,3],[4,5,6],[7,8,9]]
<br>

**Output:**
<br>
[[7,4,1],[8,5,2],[9,6,3]]
<br>

**Explanation:** 

Step 1: Make transpose of the matrix by **swapping arr[i][j] with arr[j][i]**  
Step 2: Then horizontally shift the matrix  
i. Run for loop from of **i from 0 to n**  
ii. Run for loop from of **j from 0 to n/2**  
Step 3: Then **swap arr[i][n - 1 -j] with arr[i][j]**  

```C++

void rotate(vector<vector<int>>& arr) {
    int n = arr.size();
    for(int i=0; i<n; i++) {
        for(int j=i; j<n; j++) {
            swap(arr[i][j], arr[j][i]);
        }
    }

    for(int i=0; i<n; i++) {
        for(int j=0; j<n/2; j++) {
            swap(arr[i][n - 1 -j], arr[i][j]);
        }
    }
}

```

---


### [Pow(x, n)](https://leetcode.com/problems/powx-n/)

Implement pow(x, n), which calculates x raised to the power n (i.e., x<sup>n</sup>).  

**Input:**
<br>
x = 2.00000  
n = 10
<br>

**Output:**
<br>
1024.00000
<br>

**Explanation:** 

If power is even  
2<sup>10</sup> = (2 x 2)<sup>5</sup> = (4)<sup>5</sup>  
(4)<sup>5</sup> - now the power has become positive so,  
x becomes x = x*(x)<sup>n-1</sup>  
<br>

if **n** is **even**:  
x = x*x
n = n/2  
<br>

if **n** is **odd**:  
ans = ans*x;
n = n-1  

```C++

double myPow(double x, int m) {
    long long n = m;
    double ans = 1.0;

    if(n<0) {
        n = (-1)*n;
    }

    while(n) {
        if(n%2 == 0) {
            x = x*x;
            n = n/2;
        } else {
            ans = ans*x;
            n = n-1;
        }
    }

    if(m<0) {
        ans = 1/ans;
    }

    return ans;
}

```

---

### [Majority Element(>n/2 times)](https://www.geeksforgeeks.org/majority-element/)

The majority element is the element that appears more than **⌊n / 2⌋** times. You may assume that the majority element always exists in the array.

**Input:**
<br>
nums = [2,2,1,1,1,2,2]
<br>

**Output:**
<br>
2
<br>

**Explanation:** 

Step 1: This is **Moore Voting Algorithm**  
Step 2: There are multiple blocks of elements where count becomes 0  
<br>
Prefix &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Suffix  
________ | ________ | ________ | ________ | ________ 
<br>
Step 3: If the element doesn't becomes majority in prefix, then it is bound to become majority in the last block i.e. Suffix.

```python

def majorityElement(arr):
    ele = 0
    count = 0

    for i in range(len(arr)):
        if count==0:
            ele = arr[i]

        if arr[i] == ele:
            count += 1
        else:
            count -= 1
    
    return ele

```

---

### [Majority Element(>n/3 times)](https://www.geeksforgeeks.org/n3-repeated-number-array-o1-space/)

Given an integer array of size n, find all elements that appear more than **⌊ n/3 ⌋** times.

**Input:**
<br>
arr = [1 , 1, 1, 3, 3 , 2, 2, 2]
<br>

**Output:**
<br>
[1, 2]
<br>

**Explanation:** 

Step 1: This is **Boyre Moore Voting Algorithm**  
Step 2: As **n/3 only gives 2** as maximum remainder so there must be **at max 2 majority elements** in an array that have counts greater tha **n/3.**  
Step 3: Instead of ele now there will be num1, num2, c1, c2 to store two elements.

```python

def majorityElement(arr):
    num1 = -1
    num2 = -1
    c1 = 0
    c2 = 0

    for i in range(len(arr)):
        if arr[i] == num1:
            c1 += 1
        elif arr[i] == num2:
            c2 += 1
        elif c1 == 0:
            num1 = arr[i]
            c1 = 1
        elif c2 == 0:
            num2 = arr[i]
            c2 = 1
        else:
            c1 -= 1
            c2 -= 1

    temp = []
    c1 = 0
    c2 = 0
    for i in range(len(arr)):
        if arr[i] == num1:
            c1 += 1
        if arr[i] == num2:
            c2 += 1
        
    if c1 > len(arr)//3:
        temp.append(num1)
    if (c2 > len(arr)//3) and (num1 != num2):
        temp.append(num1)
        
    
    return temp

```

---

### [Grid Unique Paths](https://www.interviewbit.com/problems/grid-unique-paths/)

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

---

### [Reverse Pairs](https://leetcode.com/problems/reverse-pairs/)

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

---

### [Equilibrium Point](https://www.geeksforgeeks.org/equilibrium-index-of-an-array/)

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

---

### [Chocolate Distribution Problem](https://practice.geeksforgeeks.org/problems/chocolate-distribution-problem/0)

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

---

### [Convert Array into Zig Zag Formation](https://practice.geeksforgeeks.org/problems/convert-array-into-zig-zag-fashion/0)

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

---

### [Trapping Rain Water](https://practice.geeksforgeeks.org/problems/trapping-rain-water/0)

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

---

### [Transpose of Matrix](https://practice.geeksforgeeks.org/problems/transpose-of-matrix/0)

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

---

### [Print Matrix in snake Pattern](https://www.geeksforgeeks.org/print-matrix-snake-pattern/)

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

---

### [Print a given matrix in spiral form](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)

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

---

### [Is Sudoku Valid](https://www.geeksforgeeks.org/check-if-given-sudoku-solution-is-valid-or-not/)

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

---

### [Count zeros in a sorted matrix](https://www.geeksforgeeks.org/count-zeros-in-a-row-wise-and-column-wise-sorted-matrix/)

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

---

### [Squares in a Matrix](https://www.geeksforgeeks.org/count-number-of-squares-in-a-rectangle/)

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

---

### [A Boolean Matrix Question](https://www.geeksforgeeks.org/a-boolean-matrix-question/)

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

---

### [Search in row-wise and column-wise sorted](https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/) 
### [Find the row with maximum number of 1s](https://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/)

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

---

### [Count pairs Sum in matrices](https://www.geeksforgeeks.org/count-pairs-two-sorted-matrices-given-sum/)

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

---

### [Median In a Row-Wise sorted Matrix](https://www.geeksforgeeks.org/find-median-row-wise-sorted-matrix/)

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

---

### [Nuts and Bolts Problem](https://practice.geeksforgeeks.org/problems/nuts-and-bolts-problem/0)

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

---

### [Check if there is a subarray with 0 sum](https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/)

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

---

### [Longest Sub-Array with Sum K ](https://www.geeksforgeeks.org/longest-sub-array-sum-k/)

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

---

### [Longest subarray with sum divisible by K](https://www.geeksforgeeks.org/longest-subarray-sum-divisible-k/)

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

---

### [Largest subarray with equal 1s and 0s](https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/)

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

---

### [Longest common span with same number of 1s and 0s among two arrays](https://www.geeksforgeeks.org/longest-span-sum-two-binary-arrays/)

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

---

### [Find mximum sum in any subarray of size k](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)

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

---

### [Count distinct elements in every window of size k](https://www.geeksforgeeks.org/count-distinct-elements-in-every-window-of-size-k/)

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

---

### [Check for subarray with given sum](https://www.geeksforgeeks.org/find-subarray-with-given-sum/)

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

---

### [Boolean Matrix Problem](https://practice.geeksforgeeks.org/problems/boolean-matrix-problem/0)

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

---

### [Linear Search](https://www.geeksforgeeks.org/linear-search/)

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

---

### [Facing the sun](https://practice.geeksforgeeks.org/problems/facing-the-sun/0)

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

---

### [Magnet Array Problem](https://practice.geeksforgeeks.org/problems/magnet-array-problem/0#:~:text=Given%20N%20Magnets%20which%20are,%2C%20d%20being%20the%20distance).)

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

---

### [Binary Search](https://www.geeksforgeeks.org/binary-search/)

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

---

### [Floor in a Sorted Array](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)

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

---

### [Count occurrences in a sorted array](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/)

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

---

### [Search in a sorted and rotated](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)

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

---

### [Find the missing number](https://www.geeksforgeeks.org/find-the-missing-number/)

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

---

### [Missing element of AP](https://practice.geeksforgeeks.org/problems/missing-element-of-ap/0)

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

---

### [Square root of a number](https://www.geeksforgeeks.org/find-square-root-number-upto-given-precision-using-binary-search/)

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

---

### [Find Transition Point in a Sorted Binary Array](https://www.geeksforgeeks.org/find-transition-point-binary-array/)

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

---

### [Last index of One](https://www.geeksforgeeks.org/find-last-index-character-string/)

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

---

### [Peak element](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)

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

---

### [Allocate minimum number of pages](https://www.geeksforgeeks.org/allocate-minimum-number-pages/)

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

---

### [Common elements in three sorted](https://www.geeksforgeeks.org/find-common-elements-three-sorted-arrays/)

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

---

### [Smallest Positive missing number](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)

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

---

### [Check if array is sorted](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)

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

---

### [Sort a binary array](https://www.geeksforgeeks.org/sort-binary-array-using-one-traversal/)

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

---

### [Sort an array of 0s, 1s and 2s (B, E, D too)](https://www.geeksforgeeks.org/sort-an-array-of-0s-1s-and-2s/)

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

---

### [Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/)

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

---

### [Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/)

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

---

### [Selection Sort](https://www.geeksforgeeks.org/selection-sort/)

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

---

### [Quick Sort](https://www.geeksforgeeks.org/quick-sort/)

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

---

### [Merge Sort](https://www.geeksforgeeks.org/merge-sort/)

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

---

### [Sort an array when two halves are sorted](https://practice.geeksforgeeks.org/problems/sort-the-half-sorted/0)

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

---

### [Relative Sorting](https://leetcode.com/problems/relative-sort-array/)

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

---

### [Sorting elements by frequency](https://www.geeksforgeeks.org/sort-elements-by-frequency/)

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

---

### [Minimum Swaps to Sort](https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/)

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

---

### [Triplet Sum in Array](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)

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

---

### [Triplet Family](https://www.geeksforgeeks.org/find-triplet-sum-two-equals-third-element/)

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

---

### [Count the triplets](https://www.geeksforgeeks.org/count-triplets-such-that-one-of-the-numbers-can-be-written-as-sum-of-the-other-two/)

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

---

### [Nth root of an integer](https://www.geeksforgeeks.org/n-th-root-number/)

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

---

### [Matrix Median](https://www.geeksforgeeks.org/n-th-root-number/)

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

---

### [Find the element that appears once in sorted array, and rest element appears twice](https://www.geeksforgeeks.org/find-the-element-that-appears-once-in-a-sorted-array/)

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

---

### [Search element in a sorted/pivot where it is rotated](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)

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

---

### [Median of 2 sorted arrays](https://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes/)

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

---

### [Kth element of 2 sorted arrays](https://www.geeksforgeeks.org/k-th-element-two-sorted-arrays/)

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

---

### [Allocate Minimum of Pages](https://www.geeksforgeeks.org/allocate-minimum-number-pages/)

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

---

### [Aggresive Cows](https://www.spoj.com/problems/AGGRCOW/)

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

---

### [Bishu and Soldiers](https://www.hackerearth.com/problem/algorithm/bishu-and-soldiers-227/)

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

---

### [Painter's Partition Problem](https://www.geeksforgeeks.org/painters-partition-problem/)

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

---

### [Print a Linked List](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)

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

---

### [Length of a linked list](https://www.geeksforgeeks.org/find-length-of-a-linked-list-iterative-and-recursive/)

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

---

### [Node at a given index in linked list](https://www.geeksforgeeks.org/write-a-function-to-get-nth-node-in-a-linked-list/)

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

---

### [Middle of a linked list](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)

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

---

### [n-th node from end of a linked list](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)

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

---

### [Delete a node](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)

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

---

### [Remove every k’th node](https://www.geeksforgeeks.org/remove-every-k-th-node-linked-list/)

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

---

### [Delete N nodes after M nodes of a linked list](https://www.geeksforgeeks.org/delete-n-nodes-after-m-nodes-of-a-linked-list/)

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

---

### [Delete without head pointer](https://www.geeksforgeeks.org/delete-a-node-from-linked-list-without-head-pointer/)

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

---

### [Rearrange a linked list](https://www.geeksforgeeks.org/rearrange-a-linked-list-such-that-all-even-and-odd-positioned-nodes-are-together/)

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

---

### [Segregate even and odd (Using only one traversal)](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)

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

---

### [Reorder List](https://leetcode.com/problems/reorder-list/)

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

---

### [Polynomial Addition](https://www.geeksforgeeks.org/adding-two-polynomials-using-linked-list/)

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

---

### [Insert in a Sorted List](https://www.geeksforgeeks.org/given-a-linked-list-which-is-sorted-how-will-you-insert-in-sorted-way/)

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

---

### [Swap nodes in pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

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

---

### [Reverse a linked list](https://www.geeksforgeeks.org/reverse-a-linked-list/)

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

---

### [Reverse a Linked List in groups of given size](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)

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

---

### [Check for palindrome](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)

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

---

### [Flattening a linked list](https://www.geeksforgeeks.org/flattening-a-linked-list/)

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

---

### [Get intersection point](https://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/)

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

---

### [Remove duplicates from sorted list](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)

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

---

### [Remove duplicates from unsorted lists](https://www.geeksforgeeks.org/remove-duplicates-from-an-unsorted-linked-list/)

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

---

### [Sort a linked list of 0s, 1s and 2s](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/)

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

---

### [Circular Linked List](https://www.geeksforgeeks.org/circular-linked-list/)

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

---

### [Detect loop in a linked list](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)

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

---

### [Find length of Loop](https://www.geeksforgeeks.org/find-length-of-loop-in-linked-list/)

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

---

### [Remove loop in a linked list](https://www.geeksforgeeks.org/detect-and-remove-loop-in-a-linked-list/)

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

---

### [Add two numbers represented by linked lists](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/)

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

---

### [Clone a linked list with random pointers](https://www.geeksforgeeks.org/a-linked-list-with-next-and-arbit-pointer/)

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

---

### [Add 1 to a number represented as linked list](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)

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

---

### [Add two numbers represented as linked list](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/)

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

---

### [Multiply two linked lists](https://www.geeksforgeeks.org/multiply-two-numbers-represented-linked-lists/)

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

---

### [Merge two sorted linked lists](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

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

---

### [Merge Sort on Linked List](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

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

---

### [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

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

---

### [Union of Two Linked Lists](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)

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

---

### [Insert a node in Doubly linked list](https://www.geeksforgeeks.org/doubly-linked-list/)

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

---

### [Delete node in Doubly Linked List](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)

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

---

### [Circular Linked List Traversal](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)

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

---

### [Split a Circular Linked List into two halves](https://www.geeksforgeeks.org/split-a-circular-linked-list-into-two-halves/)

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

---

### [Insert in Sorted way in a Sorted DLL](https://www.geeksforgeeks.org/insert-value-sorted-way-sorted-doubly-linked-list/)

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

---

### [QuickSort on Doubly Linked List](https://www.geeksforgeeks.org/quicksort-for-linked-list/)

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

---

### [Merge Sort on Doubly Linked List](https://www.geeksforgeeks.org/merge-sort-for-doubly-linked-list/)

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

---

### [Rotate doubly Linked List by N nodes](https://practice.geeksforgeeks.org/problems/rotate-doubly-linked-list-by-p-nodes/1)

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

---

### [XOR Linked List](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)

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

---

### [Implement Stacks using Arrays](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)

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

---

### [Implement Queues using Arrays](https://www.geeksforgeeks.org/array-implementation-of-queue-simple/)

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

---

### [Implement Stacks using Queue](https://www.geeksforgeeks.org/implement-stack-using-queue/)

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

---

### [Implement Queue using Stack](https://www.geeksforgeeks.org/queue-using-stacks/)

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

---

### [Check for balanced Parenthesis](https://practice.geeksforgeeks.org/problems/parenthesis-checker/0)

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

---

### [Next Greater Element](https://practice.geeksforgeeks.org/problems/next-larger-element-1587115620/1)

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

---

### [Get minimum element from stack](https://practice.geeksforgeeks.org/problems/get-minimum-element-from-stack/1)

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

---

### [Sort a Stack](https://www.geeksforgeeks.org/sort-a-stack-using-recursion/)

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

---

### [Next Smaller Element](https://www.geeksforgeeks.org/next-smaller-element/)

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

---

### [LRU Cache](https://www.geeksforgeeks.org/lru-cache-implementation/)

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

---

### [Circular tour](https://www.geeksforgeeks.org/find-a-tour-that-visits-all-stations/)

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

---

### [Find maximum of minimums of every window size]()

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

---

### [Largest Rectangle in Histogram (One Pass)](https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-set-1/)

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

---

### [Largest Rectangle in Histogram (Two Pass)](https://www.geeksforgeeks.org/largest-rectangle-under-histogram/)

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

---

### [Sliding Window Maximum - Priority Queue Method](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)

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

---

### [Implement Min Stack](https://leetcode.com/problems/min-stack/)

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

---

### [Rotten Orange (BFS)](https://leetcode.com/problems/rotting-oranges/)

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

---

### [Stock Span Problem](https://www.geeksforgeeks.org/the-stock-span-problem/)

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

---

### [The Celebrity Problem](https://www.geeksforgeeks.org/the-celebrity-problem/)

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

---

### [Implement Queue using Linked List](https://www.geeksforgeeks.org/queue-linked-list-implementation/)

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

---

### [Implement Stack using Linked List](https://www.geeksforgeeks.org/implement-a-stack-using-singly-linked-list/)

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

---

### Rest Day! You have succesfully grinded for 50 days. Let's go king for another 50 days. You got this :crown:.

---

### [Inorder Traversal](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

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

---

### [Preorder Traversal](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

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

---

### [Postord Traversal](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

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

---

### [Left View of Binary Tree](https://www.geeksforgeeks.org/print-left-view-binary-tree/)

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

---

### [Bottom View of Binary Tree](https://www.geeksforgeeks.org/bottom-view-binary-tree/)

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

---

### [Top View of Binary Tree](https://www.geeksforgeeks.org/print-nodes-top-view-binary-tree/)

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

---

### [Level Order Traversal](https://www.geeksforgeeks.org/level-order-tree-traversal/)

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

---

### [Height of Binary Tree](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/)

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

---

### [Diameter of Binary Tree](https://www.geeksforgeeks.org/diameter-of-a-binary-tree/)

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

---

### [Check if Binary Tree is height balanced or not](https://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/)

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

---

### [LCA in Binary Tree](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)

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

---

### [Check if two trees are identical or not](https://www.geeksforgeeks.org/write-c-code-to-determine-if-two-trees-are-identical/)

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

---

### [Maximum path sum ](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

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

---

### [Construct Binary Tree from inorder and preorder](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)

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

---

### [Construct Binary Tree from Inorder and Postorder](https://www.geeksforgeeks.org/construct-a-binary-tree-from-postorder-and-inorder/)

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

---

### [Symmetric Binary Tree ](https://www.geeksforgeeks.org/symmetric-tree-tree-which-is-mirror-image-of-itself/)

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

---

### [Flatten Binary Tree to LinkedList](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

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

---

### [Check if Binary Tree is mirror of itself or not ](https://www.geeksforgeeks.org/check-if-two-trees-are-mirror/)

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

---

### [Populate Next Right pointers of Tree](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

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

---

### [Search given Key in BST ](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)

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

---

### [Construct BST from given keys](https://www.techiedelight.com/construct-balanced-bst-given-keys/)

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

---

### [Check is a BT is BST or not  ](https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)

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

---

### [Find LCA of two nodes in BST ](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-search-tree/)

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

---

### [Find the inorder predecessor/successor of a given Key in BST](https://www.geeksforgeeks.org/inorder-predecessor-successor-given-key-bst/)

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

---

### [Floor and Ceil in a BST ](https://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/)

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

---

### [Find K-th smallest element in BST](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)

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

---

### [Find K-th largest element in BST](https://www.geeksforgeeks.org/kth-largest-element-in-bst-when-modification-to-bst-is-not-allowed/)

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

---

### [Find a pair with a given sum in BST ](https://www.geeksforgeeks.org/find-pair-given-sum-bst/#:~:text=We%20traverse%20binary%20search%20tree,otherwise%20it%20doesn't%20exist.)

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

---

### [BST iterator ](https://leetcode.com/problems/binary-search-tree-iterator/)

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

---

### [Size of the largest BST in a Binary Tree ](https://www.geeksforgeeks.org/largest-bst-binary-tree-set-2/)

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

---

### [Serialize and deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

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

---

### [Binary Tree to Double Linked List](https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)

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

---

### [Find median in a stream of running integers](https://www.geeksforgeeks.org/median-of-stream-of-running-integers-using-stl/)

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

---

### [K-th largest element in a stream](https://www.geeksforgeeks.org/kth-largest-element-in-a-stream/)

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

---

### [Distinct numbers in Window](https://www.interviewbit.com/problems/distinct-numbers-in-window/)

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

---

### [K-th largest element in an unsorted array](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)

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

---

### [Depth First Traversal](https://practice.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)

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

---

### [Breadth First Traversal](https://practice.geeksforgeeks.org/problems/bfs-traversal-of-graph/1)

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

---

### [Detect cycle in undirected graph](https://practice.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1/)

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

---

### [Detect cycle in a directed graph](https://practice.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

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

---

### [Topological sort](https://practice.geeksforgeeks.org/problems/topological-sort/1)

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

---

### [Find the number of islands](https://practice.geeksforgeeks.org/problems/find-the-number-of-islands/1)

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

---

### [Implementing Dijkstra](https://practice.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/1)

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

---

### [Minimum Swaps](https://practice.geeksforgeeks.org/problems/minimum-swaps/1)

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

---

### [Strongly Connected Components](https://practice.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1)

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

---

### [Shortest Source to Destination Path](https://practice.geeksforgeeks.org/problems/shortest-source-to-destination-path/0)

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

---

### [Find whether path exist](https://practice.geeksforgeeks.org/problems/find-whether-path-exist/0)

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

---

### [Minimum Cost Path](https://practice.geeksforgeeks.org/problems/minimum-cost-path/0)

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

---

### [Circle of Strings](https://practice.geeksforgeeks.org/problems/circle-of-strings/0)

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

---

### [Floyd Warshall](https://practice.geeksforgeeks.org/problems/implementing-floyd-warshall/0)

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

---

### [Bellman Ford Algo](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)

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

---

### [MST using Prim’s Algo](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)

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

---

### [MST using Kruskal’s Algo](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)

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

---

### [Alien Dictionary](https://practice.geeksforgeeks.org/problems/alien-dictionary/1)

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

---

### [Minimum Operations](https://practice.geeksforgeeks.org/problems/find-optimum-operation/0)

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

---

### [Max length chain](https://practice.geeksforgeeks.org/problems/max-length-chain/1)

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

---

### [Minimum number of Coins](https://practice.geeksforgeeks.org/problems/-minimum-number-of-coins/0)

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

---

### [Longest Common Substring](https://practice.geeksforgeeks.org/problems/longest-common-substring/0)

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

---

### [Longest Increasing Subsequence](https://practice.geeksforgeeks.org/problems/longest-increasing-subsequence/0)

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

---

### [Longest Common Subsequence](https://practice.geeksforgeeks.org/problems/longest-common-subsequence/0)

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

---

### [0 – 1 Knapsack Problem](https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem/0)

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

---

### [Maximum sum increasing subsequence](https://practice.geeksforgeeks.org/problems/maximum-sum-increasing-subsequence/0)

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

---

### [Minimum number of jumps](https://practice.geeksforgeeks.org/problems/minimum-number-of-jumps/0)

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

---

### [Edit Distance](https://practice.geeksforgeeks.org/problems/edit-distance/0)

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

---

### [Coin Change Problem](https://practice.geeksforgeeks.org/problems/coin-change/0)

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

---

### [Subset Sum Problem](https://practice.geeksforgeeks.org/problems/subset-sum-problem/0)

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

---

### [Box Stacking](https://practice.geeksforgeeks.org/problems/box-stacking/1)

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

---

### [Rod Cutting](https://practice.geeksforgeeks.org/problems/cutted-segments/0)

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

---

### [Path in Matrix](https://www.geeksforgeeks.org/find-the-longest-path-in-a-matrix-with-given-constraints/)

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

---

### [Minimum sum partition](https://practice.geeksforgeeks.org/problems/minimum-sum-partition/0)

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

---

### [Count number of ways to cover a distance](https://practice.geeksforgeeks.org/problems/count-number-of-hops/0)

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

---

### [Egg Dropping Puzzle](https://practice.geeksforgeeks.org/problems/egg-dropping-puzzle/0)

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

---

### [Optimal Strategy for a Game](https://practice.geeksforgeeks.org/problems/optimal-strategy-for-a-game/0)

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

---

### [Word Break](https://www.geeksforgeeks.org/word-break-problem-dp-32/)

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

---

### [Palindrome Partitioning (MCM Variation)](https://www.geeksforgeeks.org/palindrome-partitioning-dp-17/)

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

---

### [Subset Sums](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)

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

---

### [Subset - II](https://leetcode.com/problems/subsets-ii/)

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

---

### [Combination Sum - 1](https://leetcode.com/problems/combination-sum/)

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

---

### [Combination Sum - 2](https://leetcode.com/problems/combination-sum-ii/)

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

---

### [Palindrome Partioning](https://leetcode.com/problems/palindrome-partitioning/)

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

---

### [Kth - Permutation Sequence](https://www.geeksforgeeks.org/find-the-k-th-permutation-sequence-of-first-n-natural-numbers/)

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

---

### [Print all permutations of a string/array](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)

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

---

### [N Queens Problem](https://www.geeksforgeeks.org/n-queen-problem-backtracking-3/)

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

---

### [Sudoku Solver](https://www.geeksforgeeks.org/sudoku-backtracking-7/)

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

---

### [M colouring problem](https://www.geeksforgeeks.org/m-coloring-problem-backtracking-5/)

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

---

### [Rat in a Maze](https://www.geeksforgeeks.org/rat-in-a-maze-backtracking-2/)

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

---

### [Flood Fill Algorithm](https://practice.geeksforgeeks.org/problems/flood-fill-algorithm/0)

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

---

### [Special Keyboard](https://practice.geeksforgeeks.org/problems/special-keyboard/0)

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

---

### [Josephus Problem]()

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

---

### [Handshakes Problem]()

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

---

### [Tower of Hanoi]()

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

---

### [Relative Sorting](https://practice.geeksforgeeks.org/problems/relative-sorting/0)

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

---

### [Sorting Elements of an Array by Frequency](https://practice.geeksforgeeks.org/problems/sorting-elements-of-an-array-by-frequency/0)

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

---

### [Largest subarray with 0 sum](https://practice.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)

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

---

### [Common elements](https://practice.geeksforgeeks.org/problems/common-elements/0)

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

---

### [Find all four sum numbers](https://practice.geeksforgeeks.org/problems/find-all-four-sum-numbers/0)

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

---

### [Swapping pairs make sum equal](https://practice.geeksforgeeks.org/problems/swapping-pairs-make-sum-equal/0)

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

---

### [Count distinct elements in every window](https://practice.geeksforgeeks.org/problems/count-distinct-elements-in-every-window/1)

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

---

### [Array Pair Sum Divisibility Problem](https://practice.geeksforgeeks.org/problems/array-pair-sum-divisibility-problem/0)

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

---

### [Longest consecutive subsequence](https://practice.geeksforgeeks.org/problems/longest-consecutive-subsequence/0)

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

---

### [Array Subset of another array](https://practice.geeksforgeeks.org/problems/array-subset-of-another-array/0)

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

---

### [Find all pairs with a given sum](https://practice.geeksforgeeks.org/problems/find-all-pairs-whose-sum-is-x/0)

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

---

### [Find first repeated character](https://practice.geeksforgeeks.org/problems/find-first-repeated-character/0)

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

---

### [Zero Sum Subarrays](https://practice.geeksforgeeks.org/problems/zero-sum-subarrays/0)

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

---

### [Minimum indexed character](https://practice.geeksforgeeks.org/problems/minimum-indexed-character/0)

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

---

### [Check if two arrays are equal or not](https://practice.geeksforgeeks.org/problems/check-if-two-arrays-are-equal-or-not/0)

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

---

### [Uncommon characters](https://practice.geeksforgeeks.org/problems/uncommon-characters/0)

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

---

### [Smallest window in a string containing all the characters of another string](https://practice.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string/0)

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

---

### [First element to occur k times](https://practice.geeksforgeeks.org/problems/first-element-to-occur-k-times/0)

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

---

### [Check if frequencies can be equal](https://practice.geeksforgeeks.org/problems/check-frequencies/0)

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

---

### [Longest substring without repeat](https://www.geeksforgeeks.org/length-of-the-longest-substring-without-repeating-characters/)

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

---

### [Count number of subarrays with given XOR](https://www.geeksforgeeks.org/count-number-subarrays-given-xor/)

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

---

### [Find first set bit](https://practice.geeksforgeeks.org/problems/find-first-set-bit/0)

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

---

### [Rightmost different bit](https://practice.geeksforgeeks.org/problems/rightmost-different-bit/0)

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

---

### [Check whether K-th bit is set or not](https://practice.geeksforgeeks.org/problems/check-whether-k-th-bit-is-set-or-not/0)

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

---

### [Toggle bits given range](https://practice.geeksforgeeks.org/problems/toggle-bits-given-range/0)

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

---

### [Set kth bit](https://practice.geeksforgeeks.org/problems/set-kth-bit/0)

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

---

### [Power of 2](https://practice.geeksforgeeks.org/problems/power-of-2/0)

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

---

### [Bit Difference](https://practice.geeksforgeeks.org/problems/bit-difference/0)

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

---

### [Rotate Bits](https://practice.geeksforgeeks.org/problems/rotate-bits/0)

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

---

### [Swap all odd and even bits](https://practice.geeksforgeeks.org/problems/swap-all-odd-and-even-bits/0)

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

---

### [Count total set bits](https://practice.geeksforgeeks.org/problems/count-total-set-bits/0)

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

---

### [Power Set](https://www.geeksforgeeks.org/power-set/)

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

---

### [Longest Consecutive 1’s](https://practice.geeksforgeeks.org/problems/longest-consecutive-1s/0)

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

---

### [Sparse Number](https://practice.geeksforgeeks.org/problems/number-is-sparse-or-not/0)

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

---

### [Alone in a couple](https://practice.geeksforgeeks.org/problems/alone-in-couple/0)

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

---

### [Maximum subset XOR](https://practice.geeksforgeeks.org/problems/maximum-subset-xor/1)

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

---

### [Activity Selection](https://practice.geeksforgeeks.org/problems/activity-selection/0)

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

---

### [N meetings in one room](https://practice.geeksforgeeks.org/problems/n-meetings-in-one-room/0)

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

---

### [Coin Piles](https://practice.geeksforgeeks.org/problems/coin-piles/0)

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

---

### [Maximize Toys](https://practice.geeksforgeeks.org/problems/maximize-toys/0)

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

---

### [Page Faults in LRU](https://practice.geeksforgeeks.org/problems/page-faults-in-lru/0)

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

---

### [Largest number possible](https://practice.geeksforgeeks.org/problems/largest-number-possible/0)

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

---

### [Minimize the heights](https://practice.geeksforgeeks.org/problems/minimize-the-heights/0)

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

---

### [Minimize the sum of product](https://practice.geeksforgeeks.org/problems/minimize-the-sum-of-product/0)

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

---

### [Huffman Decoding](https://practice.geeksforgeeks.org/problems/huffman-decoding-1/1)

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

---

### [Minimum Spanning Tree](https://practice.geeksforgeeks.org/problems/minimum-spanning-tree/1)

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

---

### [Shop in Candy Store](https://practice.geeksforgeeks.org/problems/shop-in-candy-store/0)

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

---

### [Geek collects the balls](https://practice.geeksforgeeks.org/problems/geek-collects-the-balls/0)

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

---

### [Find the element that appears once in sorted array](https://practice.geeksforgeeks.org/problems/find-the-element-that-appears-once-in-sorted-array/0)

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

---

### [Search in a Rotated Array](https://practice.geeksforgeeks.org/problems/search-in-a-rotated-array/0)

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

---

### [Binary Search](https://practice.geeksforgeeks.org/problems/binary-search/1)

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

---

### [Sum of Middle Elements of two sorted arrays](https://practice.geeksforgeeks.org/problems/sum-of-middle-elements-of-two-sorted-arrays/0)

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

---

### [Quick Sort](https://practice.geeksforgeeks.org/problems/quick-sort/1)

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

---

### [Merge Sort](https://practice.geeksforgeeks.org/problems/merge-sort/1)

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

---

### [K-th element of two sorted Arrays](https://practice.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array/0)

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

---

### [Write your own power function](https://www.geeksforgeeks.org/write-you-own-power-without-using-multiplication-and-division/)

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

---

### [Program for n-th Fibonacci Number](https://www.techiedelight.com/program-to-find-nth-fibonacci-number/)

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

---

### [Median of two sorted arrays](https://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes/)

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

---

### [Karatsuba Algorithm](https://www.geeksforgeeks.org/karatsuba-algorithm-for-fast-multiplication-using-divide-and-conquer-algorithm/)

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

---


