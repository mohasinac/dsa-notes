[home](./../readme.md) || [back](./rotateArrByD.md)

# Leaders in an Array problem

Write a program to print all the LEADERS in the array. An element is a leader if it is greater than all the elements to its right side. And the rightmost element is always a leader.

For example:

    Input: arr[] = {16, 17, 4, 3, 5, 2},
    Output: 17, 5, 2

    Input: arr[] = {1, 2, 3, 4, 5, 2},
    Output: 5, 2

Approach 1:

- Use two loops.
- The outer loop runs from 0 to size – 1 and one by one pick all elements from left to right.
- The inner loop compares the picked element to all the elements on its right side.
  - If the picked element is greater than all the elements to its right side, then the picked element is the leader.

Code:

    void printLeaders(int arr[], int size)
    {
        for (int i = 0; i < size; i++)
        {
            int j;
            for (j = i+1; j < size; j++)
            {
                if (arr[i] <=arr[j])
                    break;
            }
            if (j == size) // the loop didn't break
                cout << arr[i] << " ";
        }
    }

Approach 2:

The idea is to scan all the elements from right to left in an array and keep track of the maximum till now. When the maximum changes its value, print it.

- We start from the last index position. The last position is always a leader, as there are no elements towards its right.
- And then we iterate on the array till we reach index position = 0.
  - Each time we keep a check on the maximum value
  - Every time we encounter a maximum value than the previous maximum value encountered, we either print or store the value as it is the leader

Code:

    void printLeaders(int arr[], int size)
    {
        int max_from_right = arr[size-1];

        /* Rightmost element is always leader */
        cout << max_from_right << " ";

        for (int i = size-2; i >= 0; i--)
        {
            if (max_from_right < arr[i])
            {
                max_from_right = arr[i];
                cout << max_from_right << " ";
            }
        }
    }

representation:

    int arr[] = {16, 17, 4, 3, 5, 2};

    maximum from right : 2, i : 4, arr[i] : 5



    maximum from right : 5, i : 3, arr[i] : 3



    maximum from right : 5, i : 2, arr[i] : 4



    maximum from right : 5, i : 1, arr[i] : 17



    maximum from right : 17, i : 0, arr[i] : 16

[next](./maxDiffWithOrderArray.md)
