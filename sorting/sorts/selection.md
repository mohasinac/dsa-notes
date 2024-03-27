# Selection Sort

The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array.

    The subarray which is already sorted.
    Remaining subarray which is unsorted.

In every iteration of selection sort, the minimum element (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray.

- Initialize minimum value(min_idx) to location 0
- Traverse the array to find the minimum element in the array
- While traversing if any element smaller than min_idx is found then swap both the values.
- Then, increment min_idx to point to next element
- Repeat until array is sorted

        void selectionSort(int arr[], int n)
        {
            int i, j, min_idx;

            // One by one move boundary of
            // unsorted subarray
            for (i = 0; i < n-1; i++)
            {

                // Find the minimum element in
                // unsorted array
                min_idx = i;
                for (j = i+1; j < n; j++)
                if (arr[j] < arr[min_idx])
                    min_idx = j;

                // Swap the found minimum element
                // with the first element
                swap(&arr[min_idx], &arr[i]);
            }
        }
