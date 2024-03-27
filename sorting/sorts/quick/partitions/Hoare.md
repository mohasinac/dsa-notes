# Hoare's Partition

Hoare’s Partition Scheme works by initializing two indexes that start at two ends, the two indexes move toward each other until an inversion is (A smaller value on the left side and a greater value on the right side) found. When an inversion is found, two values are swapped and the process is repeated.

Algorithm:

Hoarepartition(arr[], lo, hi)

    pivot = arr[lo]
    i = lo - 1  // Initialize left index
    j = hi + 1  // Initialize right index

    // Find a value in left side greater
    // than pivot
    do
        i = i + 1
    while arr[i] < pivot

    // Find a value in right side smaller
    // than pivot
    do
        j--;
    while (arr[j] > pivot);

    if i >= j then
        return j

    swap arr[i] with arr[j]

Code:

    static int partition(int[] arr, int low, int high)
        {
            int pivot = arr[low];
            int i = low - 1, j = high + 1;

            while (true)
            {
                // Find leftmost element greater
                // than or equal to pivot
                do {
                    i++;
                } while (arr[i] < pivot);

                // Find rightmost element smaller
                // than or equal to pivot
                do {
                    j--;
                } while (arr[j] > pivot);

                // If two pointers met.
                if (i >= j)
                    return j;

                // swap(arr[i], arr[j]);
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;

            }
        }
