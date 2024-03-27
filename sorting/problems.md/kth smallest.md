# Kth Smallest Element

Given an array and a number k where k is smaller than the size of the array, we need to find the k'th smallest element in the given array. It is given that all array elements are distinct.

Examples:

    Input: arr[] = {7, 10, 4, 3, 20, 15}, k = 3
    Output: 7

    Input: arr[] = {7, 10, 4, 3, 20, 15}, k = 4
    Output: 10

We have discussed a similar problem to print k largest elements.

#### Approach 1

A simple solution is to sort the given array using an O(N log N) sorting algorithm like Merge Sort, Heap Sort, etc, and return the element at index k-1 in the sorted array.
The Time Complexity of this solution is O(N log N)

Code:

    int kthSmallest(int arr[], int n, int k)
    {
        // Sort the given array
        sort(arr, arr + n);

        // Return k'th element in the sorted array
        return arr[k - 1];
    }

#### Approach 2

We can find k'th smallest element in time complexity better than O(N Log N). A simple optimization is to create a Min Heap of the given n elements and call extractMin() k times.

#### TODO: implement code for min heap
