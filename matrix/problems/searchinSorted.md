# Search in Row-wise and Column-wise sorted matrix

Given an n x n matrix and a number x, find the position of x in the matrix if it is present in it. Otherwise, print "Not Found". In the given matrix, every row and column is sorted in increasing order. The designed algorithm should have linear time complexity.

Example:

    Input: mat[4][4] = { {10, 20, 30, 40},
                                   15, 25, 35, 45},
                                   {27, 29, 37, 48},
                                 {32, 33, 39, 50}}
               x = 29
    Output: Found at (2, 1)
    Explanation: Element at (2,1) is 29


    Input : mat[4][4] = { {10, 20, 30, 40},
                                    {15, 25, 35, 45},
                                   {27, 29, 37, 48},
                                  {32, 33, 39, 50}};
              x = 100
    Output : Element not found
    Explanation: Element 100 is not found

#### Approach 1

The simple idea is to traverse the array and to search elements one by one.

Algorithm:

- Run a nested loop, outer loop for row and inner loop for the column
- Check every element with x and if the element is found then print "element found"
- If the element is not found, then print "element not found".

Code:

    int search(int mat[4][4], int n, int x)
    {
        if (n == 0)
            return -1;

        // traverse through the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                // if the element is found
                if (mat[i][j] == x) {
                    cout << "Element found at (" << i << ", "
                        << j << ")\n";
                    return 1;
                }
        }

        cout << "n Element not found";
        return 0;
    }

#### Approach 2

The simple idea is to remove a row or column in each comparison until an element is found. Start searching from the top-right corner of the matrix.

There are three possible cases.

1. The given number is greater than the current number: This will ensure that all the elements in the current row are smaller than the given number as the pointer is already at the right-most elements and the row is sorted. Thus, the entire row gets eliminated and continues the search for the next row. Here, elimination means that a row needs not be searched.
1. The given number is smaller than the current number: This will ensure that all the elements in the current column are greater than the given number. Thus, the entire column gets eliminated and continues the search for the previous column, i.e. the column on the immediate left.
1. The given number is equal to the current number: This will end the search.

Algorithm:

1. Let the given element be x, create two variable i = 0, j = n-1 as index of row and column
1. Run a loop until i = n
1. Check if the current element is greater than x then decrease the count of j. Exclude the current column.
1. Check if the current element is less than x then increase the count of i. Exclude the current row.
1. If the element is equal, then print the position and end.

Code:

    int search(int mat[4][4], int n, int x)
    {
        if (n == 0)
            return -1;

        int smallest = mat[0][0], largest = mat[n - 1][n - 1];
        if (x < smallest || x > largest)
            return -1;

        // set indexes for top right element
        int i = 0, j = n - 1;
        while (i < n && j >= 0)
        {
            if (mat[i][j] == x)
            {
                cout << "Element found at "
                    << i << ", " << j;
                return 1;
            }
            if (mat[i][j] > x)
                j--;

            // Check if mat[i][j] < x
            else
                i++;
        }

        cout << "n Element not found";
        return 0;
    }
