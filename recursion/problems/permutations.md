[back](../recursion.md)

# Printing all Permutations

Given a string, print all permutations of it.

        Input : str = "ABC"
        Output : ABC ACB BAC BCA CAB CBA

- We iterate from first to last index.
- For every index i, we swap the i-th character with the first index. This is how we fix characters at the current first index.
- Then we recursively generate all permutations beginning with fixed characters (by parent recursive calls).
- After we have recursively generated all permutations with the first character fixed, then we move the first character back to its original position so that we can get the original string back and fix the next character at first position.

![alt text](NewPermutation.gif)

Code:

    void permute(string &str, int l, int r)
    {
        if (l == r)
        {

            cout << str << " ";
            return ;
        }
        else
        {
            for (int i = l; i <= r; i++)
            {
                swap(str[l], str[i]);
                permute(str, l+1, r);
                swap(str[l], str[i]);
            }
        }
    }
