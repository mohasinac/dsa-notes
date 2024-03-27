# Sort an array with three types of elements

Given an array A[] consisting 0s, 1s and 2s. The task is to write a function that sorts the given array. The functions should put all 0s first, then all 1s and all 2s in last.

Examples:

    Input: {0, 1, 2, 0, 1, 2}
    Output: {0, 0, 1, 1, 2, 2}

    Input: {0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1}
    Output: {0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2}

#### Approach 1:

- Keep three indices low = 1, mid = 1 and high = N and there are four ranges, 1 to low (the range containing 0), low to mid (the range containing 1), mid to high (the range containing unknown elements) and high to N (the range containing 2).
- Traverse the array from start to end and mid is less than high. (Loop counter is i)
- If the element is 0 then swap the element with the element at index low and update low = low + 1 and mid = mid + 1
- If the element is 1 then update mid = mid + 1
- If the element is 2 then swap the element with the element at index high and update high = high - 1 and update i = i - 1. As the swapped element is not processed
- Print the array.

Code:

        void sort012(int a[], int arr_size)
        {
            int lo = 0;
            int hi = arr_size - 1;
            int mid = 0;

            // Iterate till all the elements
            // are sorted
            while (mid <= hi) {
                switch (a[mid]) {

                // If the element is 0
                case 0:
                    swap(a[lo++], a[mid++]);
                    break;

                // If the element is 1 .
                case 1:
                    mid++;
                    break;

                // If the element is 2
                case 2:
                    swap(a[mid], a[hi--]);
                    break;
                }
            }
        }

#### Approach 2:

- Keep three counter c0 to count 0s, c1 to count 1s and c2 to count 2s
- Traverse through the array and increase the count of c0 if the element is 0,increase the count of c1 if the element is 1 and increase the count of c2 if the element is 2
- Now again traverse the array and replace first c0 elements with 0, next c1 elements with 1 and next c2 elements with 2.

Code:

    void sortArr(int arr[], int n)
    {
        int i, cnt0 = 0, cnt1 = 0, cnt2 = 0;

        // Count the number of 0s, 1s and 2s in the array
        for (i = 0; i < n; i++) {
            switch (arr[i]) {
            case 0:
                cnt0++;
                break;
            case 1:
                cnt1++;
                break;
            case 2:
                cnt2++;
                break;
            }
        }

        // Update the array
        i = 0;

        // Store all the 0s in the beginning
        while (cnt0 > 0) {
            arr[i++] = 0;
            cnt0--;
        }

        // Then all the 1s
        while (cnt1 > 0) {
            arr[i++] = 1;
            cnt1--;
        }

        // Finally all the 2s
        while (cnt2 > 0) {
            arr[i++] = 2;
            cnt2--;
        }

        // Print the sorted array
        printArr(arr, n);
    }
