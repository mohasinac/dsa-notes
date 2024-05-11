# Check for Palindrome in Cpp

A palindrome is a word, phrase, number, or other sequences of characters which reads the same forward and backward (ignoring spaces, punctuation, and capitalization). In this article, we'll discuss how to check if a given string is a palindrome or not in C++.

#### Method 1:

Using Iterators One approach to check if a string is a palindrome is to use iterators to iterate over the characters in the string and compare them. Here's an example of how to use iterators to check if a string is a palindrome:

    bool isPalindrome(string input) {
        string::iterator begin = input.begin();
        string::iterator end = input.end() - 1;
        while (begin < end) {
            if (*begin != *end) {
                return false;
            }
            begin++;
            end--;
        }
        return true;
    }

#### Method 2:

Using the string.rbegin() and string.rend() function Another approach to check if a string is a palindrome is to use the string.rbegin() and string.rend() function. This will give you the reverse iterator to the beginning and end of the string respectively.

    bool isPalindrome(string input) {
        for (int i = 0; i < input.length(); i++) {
            if(input[i] != input[input.length() - i - 1])
                return false;
        }
        return true;
    }
