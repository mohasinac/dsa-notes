[home](../../readme.md) || [back](./leadersInArray.md)

# Maximum Difference Problem with Order

Given an array arr[] of integers, find out the maximum difference between any two elements such that larger element appears after the smaller number.

Examples :

    Input : arr = {2, 3, 10, 6, 4, 8, 1}
    Output : 8
    Explanation : The maximum difference is between 10 and 2.

    Input : arr = {7, 9, 5, 6, 3, 2}
    Output : 2
    Explanation : The maximum difference is between 9 and 7.

We take the difference with the minimum element found so far. So we need to keep track of 2 things:

- Maximum difference found so far (max_diff).
- Minimum number visited so far (min_element).

Code:

        int maxDiff(int arr[], int arr_size)
        {
            // Maximum difference found so far
            int max_diff = arr[1] - arr[0];

            // Minimum number visited so far
            int min_element = arr[0];
            for(int i = 1; i < arr_size; i++)
            {
            if (arr[i] - min_element > max_diff)
            max_diff = arr[i] - min_element;

            if (arr[i] < min_element)
            min_element = arr[i];
            }

            return max_diff;
        }

[next](./frequencyArray.md)
