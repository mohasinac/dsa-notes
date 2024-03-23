[back](./searching.md) | [home](./../readme.md)

# Sample Problems on Searching

## Missing and Repeating Number

Given an unsorted array of size n. Array elements are in the range from 1 to n. One number from set {1, 2, …n} is missing and one number occurs twice in the array. Our task is to find these two numbers.

    Input
    [2, 3, 2, 1, 5]
    Output
    4 2

#### Approach 1:

Use Sorting Follow the given steps-

1.  Sort the input array.
2.  Traverse the array and check for missing and repeating.

        function repeating_missing(arr, n){
            let sorted = arr.sort();
            let current = arr[0];
            let repeating = null, missing = null;
            for(let i=1;i<n;i++>){
                if(arr[i] === arr[i-1]){
                    repeating = arr[i];
                }
                if(arr[i] !== arr[i-1]+1){
                    missing = arr[i-1]+1;
                }
            }
            return repeating , missing;
        }

Time Complexity : O(nLogn)
Auxiliary Space: O(1)

#### Approach 2:

Use Hashing We can create a auxiliary array to count the elements in the Array. We traverse the auxiliary array for finding out missing and repeating number in the array. Can we optimize the space ?

Pseudo Code

    //n : size of array
    void repeating_missing(arr, n)
    {
    count[n+1] = {0}
    for (i=0 to n-1 )
    count[a[i]]++

        for (i=1 to n) {
            if (count[i] == 0 )
                missing = i
            if (count[i] == 2 )
                repeating = i
        }
        print(repeating, missing)

    }

#### Approach 3

Use Negative Indexing Traverse the array. While traversing, use the absolute value of every element as an index and make the value at this index as negative to mark it visited. If something is already marked negative then this is the repeating element. To find missing, traverse the array again and look for a positive value.

Pseudo Code

    //n : size of array
    void repeating_missing(arr, n)
    {
        for ( i=0 to n-1 ) {
            temp = arr[abs(arr[i])- 1]
            if (temp < 0 ) {
                repeating = abs(arr[i])
                break
            }
            arr[abs(arr[i])- 1] = -arr[abs[arr(i)]- 1]
        }

        for (i=0 to n-1) {
            if (arr[i] > 0 )
                missing = i+1
        }
        print(repeating, missing)
    }

## Count number of Occurences in Sorted Array

Given a sorted array arr[ ] and a number x, We have to count the occurrences of x in arr[ ].

    Input : [1, 1, 2, 2, 2, 2, 3] , x = 2
    Output : 4

#### Approach 1:

Linear Search We can traverse the array and count the number of occurences of x in the given input array. Time Complexity : O(n)

#### Approach 2:

Binary Search We can solve this problem using binary search by reducing the effective search space in each step. We will be using these steps -

- Use Binary search to get the index of the first occurrence of x in arr[ ]. Let the index of the first occurrence be i.
- Use Binary search to get the index of the last occurrence of x in arr[ ]. Let the index of the last occurrence be j.
- Return the count as difference between first and last indices (j – i + 1);

Pseudo Code

    int first_index(arr, low, high, x, n)
    {

        if(high >= low)
        {
            mid = (low + high)/2  /*low + (high - low)/2*/
            if( ( mid == 0 || x > arr[mid-1]) && arr[mid] == x) :
                return mid
            else if(x > arr[mid]) :
                return first_index(arr, (mid + 1), high, x, n)
            else :
                return first_index(arr, low, (mid -1), x, n)
        }
    }

    int last_index(arr, low, high, x, n):
    {
        if (high >= low)
        {
            int mid = (low + high)/2  /*low + (high - low)/2*/
            if( ( mid == n-1 || x < arr[mid+1]) && arr[mid] == x )
                return mid
            else if(x < arr[mid]) :
                return last_index(arr, low, (mid -1), x, n)
            else :
                return last_index(arr, (mid + 1), high, x, n)
        }
    }

    int count_occurences(arr, n, x)
    {
        i = first_index(arr, 0, n-1, x, n)
        j = last_index(arr, 0, n-1, x, n)
        count = j-i + 1
        return count
    }

Time Complexity : O(Log(n))

## Find the index of first 1 in a sorted array of 0’s and 1’s

We are given an sorted boolean array, We have to find out the index of first 1 in the Array

    Input : arr[] = [0, 0, 0, 0, 0, 0, 1, 1, 1, 1]
    Output : 6
    The index of first 1 in the array is 6.

Code:

        int indexOfFirstOne(arr[], low, high)
        {
            while (low <= high)
            {
                int mid = (low + high) / 2

                if (arr[mid] == 1 && (mid == 0 || arr[mid - 1] == 0)) :
                    return mid
                else if (arr[mid] == 1) :
                    high = mid - 1
                else :
                    low = mid + 1
            }
        }

## Find Peak element in Unsorted Array

Given an array arr[] of integers. Find a peak element i.e. an element that is not smaller than its neighbors.

For corner elements, we need to consider only one neighbor.

Example:

    Input: array[]= {5, 10, 20, 15}
    Output: 20
    Explanation: The element 20 has neighbors 10 and 15, both of them are less than 20.

    Input: array[] = {10, 20, 15, 2, 23, 90, 67}
    Output: 20 or 90
    Explanation: The element 20 has neighbors 10 and 15, both of them are less than 20, similarly 90 has neighbors 23 and 67.

#### Approach 1

The array can be traversed and the element whose neighbors are less than that element can be returned.

    int findPeak(int arr[], int n)
    {
    // first or last element is peak element
    if (n == 1)
    return 0;
    if (arr[0] >= arr[1])
    return 0;
    if (arr[n - 1] >= arr[n - 2])
    return n - 1;

        // check for every other element
        for (int i = 1; i < n - 1; i++) {

            // check if the neighbors are smaller
            if (arr[i] >= arr[i - 1] && arr[i] >= arr[i + 1])
                return i;
        }

    }

#### Approach 2

- Using Binary Search, check if the middle element is the peak element or not.
- If the middle element the peak element terminate the while loop and print middle element.
- then check if the element on the right side is greater than the middle element then there is always a peak element on the right side.
- If the element on the left side is greater than the middle element then there is always a peak element on the left side.

        int findPeak(int arr[], int n)
        {
        int l = 0;
        int r = n-1;
        int mid;

                while (l <= r) {

                    // finding mid by binary right shifting.
                    mid = (l + r) >> 1;

                    // first case if mid is the answer
                    if ((mid == 0 || arr[mid - 1] <= arr[mid])
                        and (mid == n - 1 || arr[mid + 1] <= arr[mid]))
                        break;

                    // move the right pointer
                    if (mid > 0 and arr[mid - 1] > arr[mid])
                        r = mid - 1;

                    // move the left pointer
                    else
                        l = mid + 1;
                }

                return mid;

        }

## Square root

Given an integer X, find its square root. If X is not a perfect square, then return floor(√x).

Examples :

    Input: x = 4
    Output: 2
    Explanation: The square root of 4 is 2.

    Input: x = 11
    Output: 3
    Explanation:  The square root of 11 lies in between 3 and 4 so floor of the square root is 3.

#### approach 1

To find the floor of the square root, try with all-natural numbers starting from 1. Continue incrementing the number until the square of that number is greater than the given number.

        int floorSqrt(int x)
        {
            // Base cases
            if (x == 0 || x == 1)
                return x;

            // Starting from 1, try all numbers until
            // i*i is greater than or equal to x.
            int i = 1, result = 1;
            while (result <= x) {
                i++;
                result = i * i;
            }
            return i - 1;
        }

#### approach 2

The idea is to find the largest integer i whose square is less than or equal to the given number. The values of i \* i is monotonically increasing, so the problem can be solved using binary search.

Below is the implementation of the above idea:

- Base cases for the given problem are when the given number is 0 or 1, then return X;
- Create some variables, for storing the lower bound say l = 0, and for upper bound r = X / 2 (i.e, The floor of the square root of x cannot be more than x/2 when x > 1).
- Run a loop until l <= r, the search space vanishes
- Check if the square of mid (mid = (l + r)/2 ) is less than or equal to X, If yes then search for a larger value in the second half of the search space, i.e l = mid + 1, update ans = mid
- Else if the square of mid is more than X then search for a smaller value in the first half of the search space, i.e r = mid – 1
- Finally, Return the ans

        int floorSqrt(int x)
        {
            // Base cases
            if (x == 0 || x == 1)
                return x;

            // Do Binary Search for floor(sqrt(x))
            int start = 1, end = x / 2, ans;
            while (start <= end) {
                int mid = (start + end) / 2;

                // If x is a perfect square
                int sqr = mid * mid;
                if (sqr == x)
                    return mid;

                // Since we need floor, we update answer when
                // mid*mid is smaller than x, and move closer to
                // sqrt(x)

                /*
                if(mid*mid<=x)
                        {
                                start = mid+1;
                                ans = mid;
                        }
                    Here basically if we multiply mid with itself so
                there will be integer overflow which will throw
                tle for larger input so to overcome this
                situation we can use long or we can just divide
                    the number by mid which is same as checking
                mid*mid < x

                */
                if (sqr <= x) {
                    start = mid + 1;
                    ans = mid;
                }
                else // If mid*mid is greater than x
                    end = mid - 1;
            }
            return ans;
        }

## Search in an Infinite Sized Array

The problem can be solved based on the following observation:

- Since array is sorted we apply binary search but the length of array is infinite so that we take start = 0 and end = 1 .
- After that check value of target is greater than the value at end index,if it is true then change newStart = end + 1 and newEnd = end +(end – start +1)\*2 and apply binary search .
- Otherwise , apply binary search in the old index values.

        int binarySearch(int arr[], int target, int start, int end)
        {
            while (start <= end) {

                int mid = start + (end - start) / 2;

                if (target < arr[mid]) {
                    end = mid - 1;
                }
                else if (target > arr[mid]) {
                    start = mid + 1;
                }
                else {
                    // ans found
                    return mid;
                }
            }
            return -1;
        }


        // an algorithm that finds an element in an
        // array of infinite size

        int findPos(int arr[], int target)
        {
            // first find the range
            // first start with a box of size 2
            int start = 0;
            int end = 1;

            // condition for the target to lie in the range
            while (target > arr[end]) {
                int temp = end + 1; // this is my new start
                // double the box value
                // end = previous end + sizeofbox*2
                end = end + (end - start + 1) * 2;
                start = temp;
            }
            return binarySearch(arr, target, start, end);
        }

## Median of Two Sorted Arrays

Given two sorted arrays, a[] and b[], the task is to find the median of these sorted arrays, where N is the number of elements in the first array, and M is the number of elements in the second array.

This is an extension of median of two sorted arrays of equal size problem. Here we handle arrays of unequal size also.

Examples:

    Input: a[] = {-5, 3, 6, 12, 15}, b[] = {-12, -10, -6, -3, 4, 10}
    Output: The median is 3.
    Explanation: The merged array is: ar3[] = {-12, -10, -6, -5 , -3, 3, 4, 6, 10, 12, 15}.
    So the median of the merged array is 3

    Input: a[] = {2, 3, 5, 8}, b[] = {10, 12, 14, 16, 18, 20}
    Output: The median is 11.
    Explanation : The merged array is: ar3[] = {2, 3, 5, 8, 10, 12, 14, 16, 18, 20}

The given two arrays are sorted, so we can utilize the ability of Binary Search to divide the array and find the median. Median means the point at which the whole array is divided into two parts. Hence since the two arrays are not merged so to get the median we require merging which is costly. Hence instead of merging, we will use a modified binary search algorithm to efficiently find the median.

Illustration:

     A[ ] = { -5, 3, 6, 12, 15 }, n = 5  &  B[ ] = { -12, -10, -6, -3, 4, 10} , m = 6

        realmidinmergedarray = 6.
        start = 0 and end = 5 => mid = 2
        leftAsize = 2 and leftBsize = 4
            leftA = 3
            leftB = -3
            rightA = 6
            rightB = 4
         A[ ] = { -5, 3, 6, 12, 15 } &  B[ ] = { -12, -10, -6, -3, 4, 10}
        As leftA <= rightB and leftB <= rightA, so the condition holds and 3 is returned as the median

- If we would have merged the two arrays, the median is the point that will divide the sorted merged array into two equal parts. So the actual median point in the merged array would have been (M+N+1)/2;
- We divide A[] and B[] into two parts. We will find the mid value and divide the first array A[] into two parts and simultaneously choose only those elements from left of B[] array such that the sum of the count of elements in the left part of both A[] and B[] will result in the left part of the merged array.
- Now we have 4 variables indicating four values two from array A[] and two from array B[].
- leftA -> Rightmost element in left part of A.
- leftb -> Rightmost element in left part of B
- rightA -> Leftmost element in right part of A
- rightB -> Leftmost element in right part of B
- Hence to confirm that the partition was correct we have to check if leftA<=rightB and leftB<=rightA. This is the case when the sum of two parts of A and B results in the left part of the merged array.
- If the condition fails we have to find another midpoint in A and then left part in B[].
- If we find leftA > rightB. means we have to decrease the size of A’s partition and shift to lesser value in A[].
- So update the right pointer of to mid-1 else we will increase the left pointer to mid+1.
- Repeat the above steps with new partitions till we get the answers.
- If leftA ≤ rightB and leftB ≤ rightA, then we get the correct partition and our answer depends on the total size of the merged array (i.e. M+N). If (M+N) is even we take max(leftA, leftB) and min(rightA, rightB), add them and divide by 2 to get our answer, else we will just return the maximum of leftA and leftB.

        double Median(vector<int>& A, vector<int>& B)
        {
        int n = A.size();
        int m = B.size();
        if (n > m)
        return Median(B, A); // Swapping to make A smaller

                int start = 0;
                int end = n;
                int realmidinmergedarray = (n + m + 1) / 2;

                while (start <= end) {
                    int mid = (start + end) / 2;
                    int leftAsize = mid;
                    int leftBsize = realmidinmergedarray - mid;
                    int leftA
                        = (leftAsize > 0)
                            ? A[leftAsize - 1]
                            : INT_MIN; // checking overflow of indices
                    int leftB
                        = (leftBsize > 0) ? B[leftBsize - 1] : INT_MIN;
                    int rightA
                        = (leftAsize < n) ? A[leftAsize] : INT_MAX;
                    int rightB
                        = (leftBsize < m) ? B[leftBsize] : INT_MAX;

                    // if correct partition is done
                    if (leftA <= rightB and leftB <= rightA) {
                        if ((m + n) % 2 == 0)
                            return (max(leftA, leftB)
                                    + min(rightA, rightB))
                                / 2.0;
                        return max(leftA, leftB);
                    }
                    else if (leftA > rightB) {
                        end = mid - 1;
                    }
                    else
                        start = mid + 1;
                }
                return 0.0;

        }

## Allocate Minimum Pages

Given a number of pages in N different books and M students. The books are arranged in ascending order of the number of pages. Every student is assigned to read some consecutive books. The task is to assign books in such a way that the maximum number of pages assigned to a student is minimum.

Example :

Input : pages[] = {12, 34, 67, 90} , m = 2

Output : 113

Explanation: There are 2 number of students. Books can be distributed in following fashion :

1.  [12] and [34, 67, 90]
    Max number of pages is allocated to student ‘2’ with 34 + 67 + 90 = 191 pages
2.  [12, 34] and [67, 90] Max number of pages is allocated to student ‘2’ with 67 + 90 = 157 pages
3.  [12, 34, 67] and [90] Max number of pages is allocated to student ‘1’ with 12 + 34 + 67 = 113 pages
    Of the 3 cases, Option 3 has the minimum pages = 113.

#### Approach 1

         int sum(int arr[],int b, int e){
             int s=0;
             for(int i=b;i<=e;i++)
                 s+=arr[i];
             return s;
         }

         int minPages(int arr[],int n, int k){
             if(k==1)
                 return sum(arr,0,n-1);
             if(n==1)
                 return arr[0];
             int res=INT_MAX;
             for(int i=1;i<n;i++){
                 res=min(res,max(minPages(arr,i,k-1),sum(arr,i,n-1)));
             }
             return res;
         }

#### Approach 2

A Binary Search method for solving the book allocation problem:

Case 1: When no valid answer exists:

- If the number of students is greater than the number of books (i.e, M > N), In this case at least 1 student will be left to which no book has been assigned.

Case 2: When a valid answer exists:

- The maximum possible answer could be when there is only one student. So, all the book will be assigned to him and the result would be the sum of pages of all the books.

- The minimum possible answer could be when number of student is equal to the number of book (i.e, M == N) , In this case all the students will get at most one book. So, the result would be the maximum number of pages among them (i.e, minimum(pages[])).

- Hence, we can apply binary search in this given range and each time we can consider the mid value as the maximum limit of pages one can get. And check for the limit if answer is valid then update the limit accordingly.

- Initialise the start to minimum(pages[]) and end = sum of pages[],
- Do while start <= end
  - Calculate the mid and check if mid number of pages can assign any student by satisfying the given condition such that all students will get at least one book. Follow the steps to check for validity.
    - Initialise the studentsRequired = 1 and curr_sum = 0 for sum of consecutive pages of book
    - Iterate over all books or say pages[]
      - Add the pages to curr_sum and check curr_sum > curr_min then increment the count of studentRequired by 1.
        Check if the studentRequired > M, return false.
    - Return true.
  - If mid is valid then, update the result and move the end = mid – 1
  - Otherwise, move the start = mid + 1
- Finally, return the result.

        // Utility function to check if current minimum value
        // is feasible or not.
        bool isPossible(int arr[], int n, int m, int curr_min)
        {
            int studentsRequired = 1;
            int curr_sum = 0;

            // iterate over all books
            for (int i = 0; i < n; i++) {
                // check if current number of pages are greater
                // than curr_min that means we will get the result
                // after mid no. of pages
                if (arr[i] > curr_min)
                    return false;

                // count how many students are required
                // to distribute curr_min pages
                if (curr_sum + arr[i] > curr_min) {
                    // increment student count
                    studentsRequired++;

                    // update curr_sum
                    curr_sum = arr[i];

                    // if students required becomes greater
                    // than given no. of students,return false
                    if (studentsRequired > m)
                        return false;
                }

                // else update curr_sum
                else
                    curr_sum += arr[i];
            }
            return true;
        }

        // function to find minimum pages
        int findPages(int arr[], int n, int m)
        {
            long long sum = 0;

            // return -1 if no. of books is less than
            // no. of students
            if (n < m)
                return -1;

            // Count total number of pages
            for (int i = 0; i < n; i++)
                sum += arr[i];

            // initialize start as 0 pages and end as
            // total pages
            int start = 0, end = sum;
            int result = INT_MAX;

            // traverse until start <= end
            while (start <= end) {
                // check if it is possible to distribute
                // books by using mid as current minimum
                int mid = (start + end) / 2;
                if (isPossible(arr, n, m, mid)) {
                    // update result to current distribution
                    // as it's the best we have found till now.
                    result = mid;

                    // as we are finding minimum and books
                    // are sorted so reduce end = mid -1
                    // that means
                    end = mid - 1;
                }

                else
                    // if not possible means pages should be
                    // increased so update start = mid + 1
                    start = mid + 1;
            }

            // at-last return minimum no. of pages
            return result;
        }
