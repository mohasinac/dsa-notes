# Inversion count in Array using Merge Sort

Inversion Count for an array indicates – how far (or close) the array is from being sorted. If the array is already sorted, then the inversion count is 0, but if the array is sorted in reverse order, the inversion count is the maximum.

Given an array arr[]. The task is to find the inversion count of arr[]. Where two elements arr[i] and arr[j] form an inversion if a[i] > a[j] and i < j.

Examples:

    Input: arr[] = {8, 4, 2, 1}
    Output: 6
    Explanation: Given array has six inversions: (8, 4), (4, 2), (8, 2), (8, 1), (4, 1), (2, 1).

    Input: arr[] = {1, 20, 6, 4, 5}
    Output: 5
    Explanation: Given array has five inversions: (20, 6), (20, 4), (20, 5), (6, 4), (6, 5).

- The idea is similar to merge sort, divide the array into two equal or almost equal halves in each step until the base case is reached.
- Create a function merge that counts the number of inversions when two halves of the array are merged,
  - Create two indices i and j, i is the index for the first half, and j is an index of the second half.
  - If a[i] is greater than a[j], then there are (mid – i) inversions because left and right subarrays are sorted, so all the remaining elements in left-subarray (a[i+1], a[i+2] … a[mid]) will be greater than a[j].
- Create a recursive function to divide the array into halves and find the answer by summing the number of inversions in the first half, the number of inversions in the second half and the number of inversions by merging the two.
  - The base case of recursion is when there is only one element in the given half.
- Print the answer.

        function mergeAndCount(arr,l,m,r)
            {

                // Left subarray
                let left = [];
                for(let i = l; i < m + 1; i++)
                {
                    left.push(arr[i]);

                }

                // Right subarray
                let right = [];
                for(let i = m + 1; i < r + 1; i++)
                {
                    right.push(arr[i]);
                }
                let i = 0, j = 0, k = l, swaps = 0;
                while (i < left.length && j < right.length)
                {
                    if (left[i] <= right[j])
                    {
                        arr[k++] = left[i++];
                    }
                    else
                    {
                        arr[k++] = right[j++];
                        swaps += (m + 1) - (l + i);
                    }
                }
                while (i < left.length)
                {
                    arr[k++] = left[i++];
                }
                while (j < right.length)
                {
                    arr[k++] = right[j++];
                }
                return swaps;
            }

            // Merge sort function
            function mergeSortAndCount(arr, l, r)
            {

                // Keeps track of the inversion count at a
                // particular node of the recursion tree
                let count = 0;
                if (l < r)
                {
                    let m = Math.floor((l + r) / 2);

                    // Total inversion count = left subarray count
                    // + right subarray count + merge count

                    // Left subarray count
                    count += mergeSortAndCount(arr, l, m);

                    // Right subarray count
                    count += mergeSortAndCount(arr, m + 1, r);

                    // Merge count
                    count += mergeAndCount(arr, l, m, r);
                }
                return count;
            }
