[home](../../readme.md) || [back](./maxDiffWithOrderArray.md)

# Frequencies in a Sorted Array

Given a sorted array, arr[] consisting of N integers, the task is to find the frequencies of each array element.

Examples:

    Input: arr[] = {1, 1, 1, 2, 3, 3, 5, 5, 8, 8, 8, 9, 9, 10}
    Output: Frequency of 1 is: 3
            Frequency of 2 is: 1
            Frequency of 3 is: 2
            Frequency of 5 is: 2
            Frequency of 8 is: 3
            Frequency of 9 is: 2
            Frequency of 10 is: 1

- In a sorted array, the same elements occur consecutively, so the idea is to maintain a variable to keep track of the frequency of elements while traversing the array.
- Follow the steps below to solve the problem:

  - Initialize a variable, say freq as 1 to store the frequency of elements.
  - Iterate in the range [1, N-1] using the variable i and perform the following steps:
    - If the value of arr[i] is equal to arr[i-1], increment freq by 1.
    - Else print value the frequency of arr[i-1] obtained in freq and then update freq to 1.
  - Finally, after the above step, print the frequency of the last distinct element of the array as freq.

Code:

    void printFreq(vector<int>& arr, int N)
    {

        // Stores the frequency of an element
        int freq = 1;

        // Traverse the array arr[]
        for (int i = 1; i < N; i++) {

            // If the current element is equal
            // to the previous element
            if (arr[i] == arr[i - 1]) {

                // Increment the freq by 1
                freq++;
            }

            // Otherwise,
            else {
                cout << "Frequency of " << arr[i - 1]
                    << " is: " << freq << endl;
                // Update freq
                freq = 1;
            }
        }

        // Print the frequency of the last element
        cout << "Frequency of " << arr[N - 1] << " is: " << freq
            << endl;

    }

[next](./stockBuySell.md)
