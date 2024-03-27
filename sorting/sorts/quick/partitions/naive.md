# Naive Partition

1.  Naive partition

Algorithm:

Naivepartition(arr[],l,r)

1. Make a Temporary array temp[r-l+1] length
2. Choose last element as a pivot element
3. Run two loops:

   - Store all the elements in the temp array that are less than pivot element
   - Store the pivot element
   - Store all the elements in the temp array that are greater than pivot element.

4. Update all the elements of arr[] with the temp[] array

QuickSort(arr[], l, r)

- If r > l

  1. Find the partition point of the array
     - m = Naivepartition(a,l,r)
  2. Call Quicksort for less than partition point

     - call Quicksort(arr, l, m-1)

  3. Call Quicksort for greater than the partition point
     - Call Quicksort(arr, m+1, r)

Code:

    static int partition(int a[], int start, int high)
        {
            // Creating temporary
            int temp[] = new int[(high - start) + 1];

            // Choosing a pivot
            int pivot = a[high];
            int index = 0;

            // smaller number
            for (int i = start; i <= high; ++i) {
                if (a[i] < pivot)
                {
                    temp[index++] = a[i];
                }
            }

            // pivot position
            int position = index;

            // Placing the pivot to its original position
            temp[index++] = pivot;

            for (int i = start; i <= high; ++i)
            {
                if (a[i] > pivot)
                {
                    temp[index++] = a[i];
                }
            }

            // Change the original array
            for (int i = start; i <= high; ++i) {
                a[i] = temp[i - start];
            }

            // return the position of the pivot
            return position;
        }

        static void quicksort(int numbers[], int start, int end)
        {
            if (start < end) {
                int point = partition(numbers, start, end);

                quicksort(numbers, start, point - 1);
                quicksort(numbers, point + 1, end);
            }
        }
