# Check for Anagram

Given two strings, check whether two strings are an anagram of each other. Two strings are said to be an anagram of each other if they are just permutations of each other. That is, the set of characters in both the strings must be the same, only the order of characters can be different.

    Input: string1 = "abcd"
        string2 = "bcad"
    Output: Yes

    Input: string1 = "listen"
        string2 = "silent"
    Output: Yes

#### Method 1

Sorting. A simple way to solve this problem is to sort both of the arrays. Since, both the arrays, contain same set of characters, therefore after sorting both of the strings, the strings must become identical.

After sorting, we can use the equals() method to check if both of the strings are equal or not and return true or false accordingly.

    bool areAnagram(string str1, string str2)
    {
        // Get lengths of both strings
        int n1 = str1.length();
        int n2 = str2.length();

        // If length of both strings is not same, then they
        // cannot be anagram
        if (n1 != n2)
            return false;

        // Sort both the strings
        sort(str1.begin(), str1.end());
        sort(str2.begin(), str2.end());

        // Compare sorted strings
        for (int i = 0; i < n1; i++)
            if (str1[i] != str2[i])
                return false;

        return true;
    }

# Method 2

his method assumes that the set of possible characters in both strings is small. In the following implementation, it is assumed that the characters are stored using 8 bit and there can be 256 possible characters.

1.  Create count arrays of size 256 for both strings. Initialize all values in count arrays as 0.
1.  Iterate through every character of both strings and increment the count of character in the corresponding count arrays.
1.  Compare count arrays. If both count arrays are same, then return true

        bool areAnagram(char* str1, char* str2)
        {
            // Create 2 count arrays and initialize all values as 0
            int count1[NO_OF_CHARS] = { 0 };
            int count2[NO_OF_CHARS] = { 0 };
            int i;

            // For each character in input strings, increment count
            // in the corresponding count array
            for (i = 0; str1[i] && str2[i]; i++) {
                count1[str1[i]]++;
                count2[str2[i]]++;
            }

            // If both strings are of different length. Removing
            // this condition will make the program fail for strings
            // like "aaca" and "aca"
            if (str1[i] || str2[i])
                return false;

            // Compare count arrays
            for (i = 0; i < NO_OF_CHARS; i++)
                if (count1[i] != count2[i])
                    return false;

            return true;
        }
