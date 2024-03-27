# Lomuto Partition

Lomuto partition

omuto’s Partition Algorithm (unstable algorithm)

Lomutopartition(arr[], lo, hi)

    pivot = arr[hi]
    i = lo     // place for swapping
    for j := lo to hi – 1 do
        if arr[j] <= pivot then
            swap arr[i] with arr[j]
            i = i + 1
    swap arr[i] with arr[hi]
    return i

QuickSort(arr[], l, r)

If r > l

1. Find the partition point of the array
   - m =Lomutopartition(a,l,r)
2. Call Quicksort for less than partition point
   - Call Quicksort(arr, l, m-1)
3. Call Quicksort for greater than the partition point
   - Call Quicksort(arr, m+1, r)

Code:

    static int sort(int numbers[], int start, int last)
        {
            int pivot = numbers[last];
            int index = start - 1;
            int temp = 0;

            for (int i = start; i < last; ++i)
            {
                if (numbers[i] < pivot) {
                    ++index;

                    // swap the position
                    temp = numbers[index];
                    numbers[index] = numbers[i];
                    numbers[i] = temp;
                }
            }

            int pivotposition = ++index;

            temp = numbers[index];
            numbers[index] = pivot;
            numbers[last] = temp;

            return pivotposition;
        }

        static void quicksort(int numbers[], int start, int end)
        {
            if (start < end)
            {
                int pivot_position = sort(numbers, start, end);
                quicksort(numbers, start, pivot_position - 1);
                quicksort(numbers, pivot_position + 1, end);
            }
        }
