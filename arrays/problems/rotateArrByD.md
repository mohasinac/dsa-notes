[home](../../readme.md) || [back](../sampleProblemsArray2.md)

# Left Rotate an Array by D places

Given an array of integers arr[] of size N and an integer, the task is to rotate the array elements to the left by d positions.

Examples:

    Input:
    arr[] = {1, 2, 3, 4, 5, 6, 7}, d = 2
    Output: 3 4 5 6 7 1 2

    Input: arr[] = {3, 4, 5, 6, 7, 1, 2}, d=2
    Output: 5 6 7 1 2 3 4

1. Constant Space: ( recursive )

Code:

        void reverse(int arr[], int low, int high)
        {
            while(low < high)
            {
                swap(arr[high], arr[low]);

                low++;
                high--;
            }
        }

        void leftRotate(int arr[], int d, int n)
        {
            reverse(arr, 0, d - 1);

            reverse(arr, d, n - 1);

            reverse(arr, 0, n - 1);
        }

2.  Iterative method: ( takes extra space but efficient )

        void leftRotate(int arr[], int d, int n)
        {
            int temp[d];

            for(int i = 0; i  < d; i++)
            {
                temp[i] = arr[i];
            }

            for(int i = d; i  < n; i++)
            {
                arr[i - d] = arr[i];
            }

            for(int i = 0; i  < d; i++)
            {
                arr[n - d + i] = temp[i];
            }
        }

Representation:

    arr = 1 2 3 4 5 , d = 2

    [1 2] 3 4 5
    2 1 [3 4 5]
    [2 1 5 4 3]

Answer: 3 4 5 1 2

[next](./leadersInArray.md)
