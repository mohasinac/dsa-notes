# Median of a Row Wise Sorted Matrix

We are given a row-wise sorted matrix of size r*c, we need to find the median of the matrix given. It is assumed that r*c is always odd.

Examples:

    Input : 1 3 5
            2 6 9
            3 6 9
    Output : Median is 5
    If we put all the values in a sorted
    array A[] = 1 2 3 3 5 6 6 9 9)

    Input: 1 3 4
        2 5 6
        7 8 9
    Output: Median is 5

An efficient approach for this problem is to use a binary search algorithm. The idea is that for a number to be median there should be exactly (n/2) numbers that are less than this number. So, we try to find the count of numbers less than all the numbers. Below is the step by step algorithm for this approach:

Algorithm:

- First, we find the minimum and maximum elements in the matrix. The minimum element can be easily found by comparing the first element of each row, and similarly, the maximum element can be found by comparing the last element of each row.
- Then we use binary search on our range of numbers from minimum to maximum, we find the mid of the min and max and get a count of numbers less than or equal to our mid. And accordingly change the min or max.
- For a number to be median, there should be (r\*c)/2 numbers smaller than that number. So for every number, we get the count of numbers less than that by using upper_bound() in each row of the matrix, if it is less than the required count, the median must be greater than the selected number, else the median must be less than or equal to the selected number.

Code:

    // function to find median in the matrix
    int binaryMedian(int m[][MAX], int r ,int c)
    {
        int min = INT_MAX, max = INT_MIN;
        for (int i=0; i<r; i++)
        {
            // Finding the minimum element
            if (m[i][0] < min)
                min = m[i][0];

            // Finding the maximum element
            if (m[i][c-1] > max)
                max = m[i][c-1];
        }

        int desired = (r * c + 1) / 2;
        while (min < max)
        {
            int mid = min + (max - min) / 2;
            int place = 0;

            // Find count of elements smaller than mid
            for (int i = 0; i < r; ++i)
                place += upper_bound(m[i], m[i]+c, mid) - m[i];
            if (place < desired)
                min = mid + 1;
            else
                max = mid;
        }
        return min;
    }
