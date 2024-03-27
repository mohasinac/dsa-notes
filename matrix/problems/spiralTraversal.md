# Spiral Traversal of Matrix

Given a 2D array, print it in spiral form. See the following examples.

Examples:

    Input:  {{1,    2,   3,   4},
                  {5,    6,   7,   8},
                 {9,   10,  11,  12},
                {13,  14,  15,  16 }}
    Output: 1 2 3 4 8 12 16 15 14 13 9 5 6 7 11 10
    Explanation: The output is matrix in spiral format.

![alt text](untitled1810.png)

#### Approach 1

Let the array have R rows and C columns. seen[r][c][/c] denotes that the cell on the r-th row and c-th column was previously visited. Our current position is (r, c), facing direction di, and we want to visit R x C total cells.
As we move through the matrix, our candidate's next position is (cr, cc). If the candidate is in the bounds of the matrix and unseen, then it becomes our next position; otherwise, our next position is the one after performing a clockwise turn.

Code:

    vector<int> spiralOrder(vector<vector<int> >& matrix)
    {
        int m = matrix.size(), n = matrix[0].size();
        vector<int> ans;

        if (m == 0)
            return ans;

        vector<vector<bool> > seen(m, vector<bool>(n, false));
        int dr[] = { 0, 1, 0, -1 };
        int dc[] = { 1, 0, -1, 0 };

        int x = 0, y = 0, di = 0;

        // Iterate from 0 to m * n - 1
        for (int i = 0; i < m * n; i++) {
            ans.push_back(matrix[x][y]);
            // on normal geeksforgeeks ui page it is showing
            // 'ans.push_back(matrix[x])' which gets copied as
            // this only and gives error on compilation,
            seen[x][y] = true;
            int newX = x + dr[di];
            int newY = y + dc[di];

            if (0 <= newX && newX < m && 0 <= newY && newY < n
                && !seen[newX][newY]) {
                x = newX;
                y = newY;
            }
            else {
                di = (di + 1) % 4;
                x += dr[di];
                y += dc[di];
            }
        }
        return ans;
    }

#### Approach 2

The problem can be solved by dividing the matrix into loops or squares or boundaries. It can be seen that the elements of the outer loop are printed first in a clockwise manner then the elements of the inner loop is printed. So printing the elements of a loop can be solved using four loops that print all the elements. Every 'for' loop defines a single direction movement along with the matrix. The first for loop represents the movement from left to right, whereas the second crawl represents the movement from top to bottom, the third represents the movement from the right to left, and the fourth represents the movement from bottom to up.

**Algorithm** :

- Create and initialize variables k - starting row index, m - ending row index, l - starting column index, n - ending column index
- Run a loop until all the squares of loops are printed.
- In each outer loop traversal print the elements of a square in a clockwise manner.
- Print the top row, i.e. Print the elements of the kth row from column index l to n, and increase the count of k.
- Print the right column, i.e. Print the last column or n-1th column from row index k to m and decrease the count of n.
- Print the bottom row, i.e. if k < m, then print the elements of m-1th row from column n-1 to l and decrease the count of m
- Print the left column, i.e. if l < n, then print the elements of lth column from m-1th row to k and increase the count of l.

Code:

    void spiralPrint(int m, int n, int a[R][C])
    {
        int i, k = 0, l = 0;

        /* k - starting row index
            m - ending row index
            l - starting column index
            n - ending column index
            i - iterator
        */

        while (k < m && l < n) {
            /* Print the first row from
                the remaining rows */
            for (i = l; i < n; ++i) {
                cout << a[k][i] << " ";
            }
            k++;

            /* Print the last column
            from the remaining columns */
            for (i = k; i < m; ++i) {
                cout << a[i][n - 1] << " ";
            }
            n--;

            /* Print the last row from
                    the remaining rows */
            if (k < m) {
                for (i = n - 1; i >= l; --i) {
                    cout << a[m - 1][i] << " ";
                }
                m--;
            }

            /* Print the first column from
                    the remaining columns */
            if (l < n) {
                for (i = m - 1; i >= k; --i) {
                    cout << a[i][l] << " ";
                }
                l++;
            }
        }
    }

#### Approach 3

The above problem can be solved by printing the boundary of the Matrix recursively. In each recursive call, we decrease the dimensions of the matrix. The idea of printing the boundary or loops is the same.

**Algorithm** :

- create a recursive function that takes a matrix and some variables (k - starting row index, m - ending row index, l - starting column index, n - ending column index) as parameters
- Check the base cases (starting index is less than or equal to ending index) and print the boundary elements in clockwise manner
- Print the top row, i.e. Print the elements of kth row from column index l to n, and increase the count of k.
- Print the right column, i.e. Print the last column or n-1th column from row index k to m and decrease the count of n.
- Print the bottom row, i.e. if k > m, then print the elements of m-1th row from column n-1 to l and decrease the count of m
- Print the left column, i.e. if l < n, then print the elements of lth column from m-1th row to k and increase the count of l.
- Call the function recursively with the values of starting and ending indices of rows and columns.

Code:

        void print(int arr[R][C], int i, int j, int m, int n)
        {
            // If i or j lies outside the matrix
            if (i >= m or j >= n)
                return;

            // Print First Row
            for (int p = j; p < n; p++)
                cout << arr[i][p] << " ";

            // Print Last Column
            for (int p = i + 1; p < m; p++)
                cout << arr[p][n - 1] << " ";

            // Print Last Row, if Last and
            // First Row are not same
            if ((m - 1) != i)
                for (int p = n - 2; p >= j; p--)
                    cout << arr[m - 1][p] << " ";

            // Print First Column,  if Last and
            // First Column are not same
            if ((n - 1) != j)
                for (int p = m - 2; p > i; p--)
                    cout << arr[p][j] << " ";

            print(arr, i + 1, j + 1, m - 1, n - 1);
        }

        print(a, 0, 0, R, C);
