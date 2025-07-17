#Median-of-two-array
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

 

Example 1:

Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
Example 2:

Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
 

Constraints:

nums1.length == m
nums2.length == n
0 <= m <= 1000
0 <= n <= 1000
1 <= m + n <= 2000
-106 <= nums1[i], nums2[i] <= 106
Solutions
Solution 1: Divide and Conquer
The problem requires the time complexity of the algorithm to be 
O
(
log
⁡
(
m
+
n
)
)
, so we cannot directly traverse the two arrays, but need to use the binary search method.

If 
m
+
n
 is odd, then the median is the 
⌊
m
+
n
+
1
2
⌋
-th number; if 
m
+
n
 is even, then the median is the average of the 
⌊
m
+
n
+
1
2
⌋
-th and the 
⌊
m
+
n
+
2
2
⌋
-th numbers. In fact, we can unify it as the average of the 
⌊
m
+
n
+
1
2
⌋
-th and the 
⌊
m
+
n
+
2
2
⌋
-th numbers.

Therefore, we can design a function 
f
(
i
,
j
,
k
)
, which represents the 
k
-th smallest number in the interval 
[
i
,
m
)
 of array 
n
u
m
s
1
 and the interval 
[
j
,
n
)
 of array 
n
u
m
s
2
. The median is the average of 
f
(
0
,
0
,
⌊
m
+
n
+
1
2
⌋
)
 and 
f
(
0
,
0
,
⌊
m
+
n
+
2
2
⌋
)
.

The implementation idea of the function 
f
(
i
,
j
,
k
)
 is as follows:

If 
i
≥
m
, it means that the interval 
[
i
,
m
)
 of array 
n
u
m
s
1
 is empty, so directly return 
n
u
m
s
2
[
j
+
k
−
1
]
;
If 
j
≥
n
, it means that the interval 
[
j
,
n
)
 of array 
n
u
m
s
2
 is empty, so directly return 
n
u
m
s
1
[
i
+
k
−
1
]
;
If 
k
=
1
, it means to find the first number, so just return the minimum of 
n
u
m
s
1
[
i
]
 and 
n
u
m
s
2
[
j
]
;
Otherwise, we find the 
⌊
k
2
⌋
-th number in the two arrays, denoted as 
x
 and 
y
. (Note, if a certain array does not have the 
⌊
k
2
⌋
-th number, then we regard the 
⌊
k
2
⌋
-th number as 
+
∞
.) Compare the size of 
x
 and 
y
:
If 
x
≤
y
, it means that the 
⌊
k
2
⌋
-th number of array 
n
u
m
s
1
 cannot be the 
k
-th smallest number, so we can exclude the interval 
[
i
,
i
+
⌊
k
2
⌋
)
 of array 
n
u
m
s
1
, and recursively call 
f
(
i
+
⌊
k
2
⌋
,
j
,
k
−
⌊
k
2
⌋
)
.
If 
x
>
y
, it means that the 
⌊
k
2
⌋
-th number of array 
n
u
m
s
2
 cannot be the 
k
-th smallest number, so we can exclude the interval 
[
j
,
j
+
⌊
k
2
⌋
)
 of array 
n
u
m
s
2
, and recursively call 
f
(
i
,
j
+
⌊
k
2
⌋
,
k
−
⌊
k
2
⌋
)
.
The time complexity is 
O
(
log
⁡
(
m
+
n
)
)
, and the space complexity is 
O
(
log
⁡
(
m
+
n
)
)
. Here, 
m
 and 
n
 are the lengths of arrays 
n
u
m
s
1
 and 
n
u
m
s
2
 respectively.
