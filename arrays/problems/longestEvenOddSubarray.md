[home](../../readme.md) || [back](./maximumSubarraySum.md)

# Longest Even Odd Subarray

Given an array a[] of N integers, the task is to find the length of the longest Alternating Even Odd subarray present in the array.

Examples:

    Input: a[] = {1, 2, 3, 4, 5, 7, 9}
    Output: 5
    Explanation:
    The subarray {1, 2, 3, 4, 5} has alternating even and odd elements.

- The idea is to consider every subarray and find the length of even and odd subarrays.

Follow the steps below to solve the problem:

- Iterate for every subarray from i = 0
- Make a nested loop, iterate from j = i + 1
- Now, check if a[j – 1] is even and a[j] is odd or a[j – 1] is odd and a[j] is even then increment count
- Maintain an answer variable which calculates max count so far

        int longestEvenOddSubarray(int a[], int n)
        {
            // Length of longest
            // alternating subarray
            int ans = 1;

            // Iterate in the array
            for (int i = 0; i < n; i++) {
                int cnt = 1;
                // Iterate for every subarray
                for (int j = i + 1; j < n; j++) {
                    if ((a[j - 1] % 2 == 0 && a[j] % 2 != 0)
                        || (a[j - 1] % 2 != 0 && a[j] % 2 == 0))
                        cnt++;
                    else
                        break;
                }
                // store max count
                ans = max(ans, cnt);
            }
            // Length of 'ans' can never be 1
            // since even odd has to occur in pair or more
            // so return 0 if ans = 1
            if (ans == 1)
                return 0;
            return ans;
        }

optimization:

By simply storing the nature of the previous element we encounter( odd or even) and comparing it with the next element.

Follow the steps below to solve the problem:

- Initialize a variable maxLength to 0, to keep the track of maximum length of the alternating subarray obtained.
- Initialize a variable currLen to 1 considering first element as the part of alternating subarray.
- Starting with element at index 1, compare every element with it’s previous. If there nature are different, increment the currLen variable.
- Otherwise, reset the currLen to 1 again so that, this current element is considered in new alternating subarray.
- Keep storing the max length of subarray in maxLength before resetting the currLen.
- Return the found max length of subarray.

        int maxEvenOdd(int arr[], int n)
        {
            if (n == 0)
                return 0;

            int maxLength = 0;

            int currLen = 1;

            for (int i = 1; i < n; i++) {
                // everytime we check if previous
                // element has opposite even/odd
                // nature or not
                if (arr[i] % 2 != arr[i-1] % 2)
                    currLen++;
                else
                {
                    // store max in maxLength
                    maxLength = max(maxLength, currLen);
                    // reset value when pattern is broken
                    currLen = 1;
                }
            }
            // since, even-odd should occur in pair
            if(maxLength == 1)
                return 0;
            return maxLength;
        }

[next](./maxCircularSum.md)
