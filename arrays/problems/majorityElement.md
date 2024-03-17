[home](../../readme.md) || [back](./maxCircularSum.md)

# Majority Element

Find the majority element in the array. A majority element in an array A[] of size n is an element that appears more than n/2 times (and hence there is at most one such element).

Examples :

    Input : {3, 3, 4, 2, 4, 4, 2, 4, 4}
    Output : 4
    Explanation: The frequency of 4 is 5 which is greater than the half of the size of the array size.

Follow the steps below to solve the given problem:

- Create a variable to store the max count, count = 0
- Traverse through the array from start to end.
- For every element in the array run another loop to find the count of similar elements in the given array.
- If the count is greater than the max count update the max count and store the index in another variable.
- If the maximum count is greater than half the size of the array, print the element. Else print there is no majority element.

Code:

    void findMajority(int arr[], int n)
    {
        int maxCount = 0;
        int index = -1; // sentinels
        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = 0; j < n; j++) {
                if (arr[i] == arr[j])
                    count++;
            }

            // update maxCount if count of
            // current element is greater
            if (count > maxCount) {
                maxCount = count;
                index = i;
            }
        }

        // if maxCount is greater than n/2
        // return the corresponding element
        if (maxCount > n / 2)
            cout << arr[index] << endl;

        else
            cout << "No Majority Element" << endl;
    }

#### Majority Element Using Moore’s Voting Algorithm:

This is a two-step process:

1. The first step gives the element that may be the majority element in the array. If there is a majority element in an array, then this step will definitely return majority element, otherwise, it will return candidate for majority element.
2. Check if the element obtained from the above step is the majority element. This step is necessary as there might be no majority element.

- Loop through each element and maintains a count of the majority element, and a majority index, maj_index
- If the next element is the same then increment the count if the next element is not the same then decrement the count.
- if the count reaches 0 then change the maj_index to the current element and set the count again to 1.
- Now again traverse through the array and find the count of the majority element found.
- If the count is greater than half the size of the array, print the element
- Else print that there is no majority element

        int findCandidate(int a[], int size)
        {
            int maj_index = 0, count = 1;
            for (int i = 1; i < size; i++) {
                if (a[maj_index] == a[i])
                    count++;
                else
                    count--;
                if (count == 0) {
                    maj_index = i;
                    count = 1;
                }
            }
            return a[maj_index];
        }

        /* Function to check if the candidate
        occurs more than n/2 times */
        bool isMajority(int a[], int size, int cand)
        {
            int count = 0;
            for (int i = 0; i < size; i++)

                if (a[i] == cand)
                    count++;

            if (count > size / 2)
                return 1;

            else
                return 0;
        }

        /* Function to print Majority Element */
        void printMajority(int a[], int size)
        {
            /* Find the candidate for Majority*/
            int cand = findCandidate(a, size);

            /* Print the candidate if it is Majority*/
            if (isMajority(a, size, cand))
                cout << " " << cand << " ";

            else
                cout << "No Majority Element";
        }

[next](./minimumGroupFlips.md)
