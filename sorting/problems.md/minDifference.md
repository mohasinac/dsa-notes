# Minimum Difference in an Array

Find minimum difference between any two elements (pair) in given array

Given an unsorted array, find the minimum difference between any pair in the given array.

Examples :

    Input: {1, 5, 3, 19, 18, 25}
    Output: 1
    Explanation: Minimum difference is between 18 and 19

    Input: {30, 5, 20, 9}
    Output: 4
    Explanation: Minimum difference is between 5 and 9

    Input: {1, 19, -4, 31, 38, 25, 100}
    Output: 5
    Explanation: Minimum difference is between 1 and -4

#### Approach 1

A simple solution is to use two loops two generate every pair of elements and compare them to get the minimum difference

    int findMinDiff(int arr[], int n)
    {
        // Initialize difference as infinite
        int diff = INT_MAX;

        // Find the min diff by comparing difference
        // of all possible pairs in given array
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (abs(arr[i] - arr[j]) < diff)
                    diff = abs(arr[i] - arr[j]);

        // Return min diff
        return diff;
    }

#### Approach 2

Sort the array in non decreasing order and find difference between adjacent elements

    int findMinDiff(int arr[], int n)
    {
        // Sort array in non-decreasing order
        sort(arr, arr + n);

        // Initialize difference as infinite
        int diff = INT_MAX;

        // Find the min diff by comparing adjacent
        // pairs in sorted array
        for (int i = 0; i < n - 1; i++)
            if (arr[i + 1] - arr[i] < diff)
                diff = arr[i + 1] - arr[i];

        // Return min diff
        return diff;
    }
