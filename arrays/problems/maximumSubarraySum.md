[home](../../readme.md) || [back](./trapperWater.md)

# Maximum Subarray Sum

Given an array arr[], the task is to find the elements of a contiguous subarray of numbers that has the largest sum.

Examples:

    Input: arr = [-2, -3, 4, -1, -2, 1, 5, -3]
    Output: [4, -1, -2, 1, 5]
    Explanation:
    In the above input the maximum contiguous subarray sum is 7 and the elements of the subarray are [4, -1, -2, 1, 5]

The idea is to use the Kadane’s Algorithm to find the maximum subarray sum and store the starting and ending index of the subarray having maximum sum and print the subarray from starting index to ending index. Below are the steps:

- Initialize 3 variables **endIndex** to 0, **currMax**, and **globalMax** to first value of the input array.
- For each element in the array starting from index(say i) 1, update currMax to max(nums[i], nums[i] + currMax) and globalMax and endIndex to i only if currMax > globalMax.
- To find the start index, iterate from endIndex in the left direction and keep decrementing the value of globalMax until it becomes 0. The point at which it becomes 0 is the start index.
- Now print the subarray between [start, end].

        void SubarrayWithMaxSum(vector<int>& nums)
        {
            // Initialize currMax and globalMax
            // with first value of nums
            int endIndex, currMax = nums[0];
            int globalMax = nums[0];

            // Iterate for all the elements
            // of the array
            for (int i = 1; i < nums.size(); ++i) {

                // Update currMax
                currMax = max(nums[i],
                            nums[i] + currMax);

                // Check if currMax is greater
                // than globalMax
                if (currMax > globalMax) {
                    globalMax = currMax;
                    endIndex = i;
                }
            }

            int startIndex = endIndex;

            // Traverse in left direction to
            // find start Index of subarray
            while (startIndex >= 0) {

                globalMax -= nums[startIndex];

                if (globalMax == 0)
                    break;

                // Decrement the start index
                startIndex--;
            }

            // Printing the elements of
            // subarray with max sum
            for (int i = startIndex;
                i <= endIndex; ++i) {

                cout << nums[i] << " ";
            }
        }

Trace:

    Finding endIndex and globalMax :

    CurrMax : -2 , nums[0] : -2, GlobalMax : -2 endindex : 0

    CurrMax : -3 , nums[1] : -3, GlobalMax : -2 endindex : 0

    CurrMax : 4 , nums[2] : 4, GlobalMax : 4 endindex : 2

    CurrMax : 3 , nums[3] : -1, GlobalMax : 4 endindex : 2

    CurrMax : 1 , nums[4] : -2, GlobalMax : 4 endindex : 2

    CurrMax : 2 , nums[5] : 1, GlobalMax : 4 endindex : 2

    CurrMax : 7 , nums[6] : 5, GlobalMax : 7 endindex : 6

    CurrMax : 4 , nums[7] : -3, GlobalMax : 7 endindex : 6

    Finding startIndex and until globalMAx === 0 :

    globalMax : 2 , nums[6] : 5, startIndex : 6

    globalMax : 1 , nums[5] : 1, startIndex : 5

    globalMax : 3 , nums[4] : -2, startIndex : 4

    globalMax : 4 , nums[3] : -1, startIndex : 3

    globalMax : 0 , nums[2] : 4, startIndex : 2

    ANSWER :[ 4 -1 -2 1 5 ]

[next](./longestEvenOddSubarray.md)
