[home](../../readme.md) || [back](./stockBuySell.md)

# Trapping Rain Water

Given an array of N non-negative integers arr[] representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

Example:

    Input: arr[]   = {3, 0, 2, 0, 4}
    Output: 7
    Explanation: Structure is like below.
    We can trap “3 units” of water between 3 and 2,
    “1 unit” on top of bar 2 and “3 units” between 2 and 4.

![alt text](Untitled-Diagram811.png)

The basic intuition of the problem is as follows:

- An element of the array can store water if there are higher bars on the left and the right.
- The amount of water to be stored in every position can be found by finding the heights of bars on the left and right sides.
- The total amount of water stored is the summation of the water stored in each index.

### Approach 1:

Traverse every array element and find the highest bars on the left and right sides. Take the smaller of two heights. The difference between the smaller height and the height of the current element is the amount of water that can be stored in this array element.

- Traverse the array from start to end:
  - For every element:
    - Traverse the array from start to that index and find the maximum height (a) and
    - Traverse the array from the current index to the end, and find the maximum height (b).
- The amount of water that will be stored in this column is min(a,b) – array[i], add this value to the total amount of water stored
- Print the total amount of water stored.

        int maxWater(int arr[], int n)
        {
            // To store the maximum water
            // that can be stored
            int res = 0;

            // For every element of the array
            for (int i = 1; i < n - 1; i++) {

                // Find the maximum element on its left
                int left = arr[i];
                for (int j = 0; j < i; j++)
                    left = max(left, arr[j]);

                // Find the maximum element on its right
                int right = arr[i];
                for (int j = i + 1; j < n; j++)
                    right = max(right, arr[j]);

                // Update the maximum water
                res = res + (min(left, right) - arr[i]);
            }

            return res;
        }

### Approach 2

In previous approach, for every element we needed to calculate the highest element on the left and on the right.

So, to reduce the time complexity:

- For every element we can precalculate and store the highest bar on the left and on the right (say stored in arrays left[] and right[]).
- Then iterate the array and use the precalculated values to find the amount of water stored in this index,

  - which is the same as ( min(left[i], right[i]) – arr[i] )

        int findWater(int arr[], int n)
        {
            // left[i] contains height of tallest bar to the
            // left of i'th bar including itself
            int left[n];

            // Right [i] contains height of tallest bar to
            // the right of ith bar including itself
            int right[n];

            // Initialize result
            int water = 0;

            // Fill left array
            left[0] = arr[0];
            for (int i = 1; i < n; i++)
                left[i] = max(left[i - 1], arr[i]);

            // Fill right array
            right[n - 1] = arr[n - 1];
            for (int i = n - 2; i >= 0; i--)
                right[i] = max(right[i + 1], arr[i]);

            // Calculate the accumulated water element by element
            // consider the amount of water on i'th bar, the
            // amount of water accumulated on this particular
            // bar will be equal to min(left[i], right[i]) - arr[i]
            // .
            for (int i = 1; i < n - 1; i++) {
                int var = min(left[i - 1], right[i + 1]);
                if (var > arr[i]) {
                    water += var - arr[i];
                }
            }

            return water;
        }

e.g.

arr[] = {3, 0, 2, 0, 4}

left[] : 3 3 3 3 4
right[] : 4 4 4 4 4

i :1 , arr[i] :0, water: 3,
i :2 , arr[i] :2, water: 4,
i :3 , arr[i] :0, water: 7,

Answer: 7

[next](./maximumSubarraySum.md)
