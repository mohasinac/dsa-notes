# KMP Algorithm for Pattern Searching

Given a text txt[0..N-1] and a pattern pat[0..M-1], write a function search(char pat[], char txt[]) that prints all occurrences of pat[] in txt[]. You may assume that N > M.

Examples:

    Input:  txt[] = "THIS IS A TEST TEXT", pat[] = "TEST"
    Output: Pattern found at index 10

    Input:  txt[] =  "AABAACAADAABAABA"
              pat[] =  "AABA"
    Output: Pattern found at index 0, Pattern found at index 9, Pattern found at index 12

The KMP matching algorithm uses degenerating property (pattern having the same sub-patterns appearing more than once in the pattern) of the pattern and improves the worst-case complexity to O(n).

The basic idea behind KMP’s algorithm is:

1. whenever we detect a mismatch (after some matches), we already know some of the characters in the text of the next window.
2. We take advantage of this information to avoid matching the characters that we know will anyway match.

Example:

    Matching Overview

    txt = " | AAAA | ABAAABA"
    pat = "AAAA"

    We compare first window of txt with pat

    txt = "A| AAAA| BAAABA"
    pat = "AAAA"  [Initial position]
    We find a match. This is same as Naive String Matching.

    In the next step, we compare next window of txt with pat.

    txt = "AAAAABAAABA"
    pat =  "AAAA" [Pattern shifted one position]

An important question arises from the above explanation, how to know how many characters to be skipped. To know this,

we pre-process pattern and prepare an integer array lps[] that tells us the count of characters to be skipped

Preprocessing Overview:

- KMP algorithm preprocesses pat[] and constructs an auxiliary lps[] of size m (same as the size of the pattern) which is used to skip characters while matching.
- name lps indicates the longest proper prefix which is also a suffix. A proper prefix is a prefix with a whole string not allowed. For example, prefixes of "ABC" are "", "A", "AB" and "ABC". Proper prefixes are "", "A" and "AB". Suffixes of the string are "", "C", "BC", and "ABC".
- We search for lps in sub-patterns. More clearly we focus on sub-strings of patterns that are both prefix and suffix.
- For each sub-pattern pat[0..i] where i = 0 to m-1, lps[i] stores the length of the maximum matching proper prefix which is also a suffix of the sub-pattern pat[0..i].

       lps[i] = the longest proper prefix of pat[0..i] which is also a suffix of pat[0..i].

Note: lps[i] could also be defined as the longest prefix which is also a proper suffix. We need to use it properly in one place to make sure that the whole substring is not considered.

Examples of lps[] construction:

    For the pattern “AAAA”, lps[] is [0, 1, 2, 3]

    For the pattern “ABCDE”, lps[] is [0, 0, 0, 0, 0]

    For the pattern “AABAACAABAA”, lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]

    For the pattern “AAACAAAAAC”, lps[] is [0, 1, 2, 0, 1, 2, 3, 3, 3, 4]

    For the pattern “AAABAAA”, lps[] is [0, 1, 2, 0, 1, 2, 3]

Preprocessing Algorithm:

In the preprocessing part,

1. We calculate values in lps[]. To do that, we keep track of the length of the longest prefix suffix value (we use len variable for this purpose) for the previous index
1. We initialize lps[0] and len as 0
1. If pat[len] and pat[i] match, we increment len by 1 and assign the incremented value to lps[i].
1. If pat[i] and pat[len] do not match and len is not 0, we update len to lps[len-1]
1. See computeLPSArray () in the above code for details

#### Implementation of KMP algorithm:

Unlike the Naive algorithm, where we slide the pattern by one and compare all characters at each shift, we use a value from lps[] to decide the next characters to be matched. The idea is to not match a character that we know will anyway match.

How to use lps[] to decide the next positions (or to know the number of characters to be skipped)?

- We start the comparison of pat[j] with j = 0 with characters of the current window of text.
- We keep matching characters txt[i] and pat[j] and keep incrementing i and j while pat[j] and txt[i] keep matching.
- When we see a mismatch
  - We know that characters pat[0..j-1] match with txt[i-j...i-1] (Note that j starts with 0 and increments it only when there is a match).
  - We also know (from the above definition) that lps[j-1] is the count of characters of pat[0...j-1] that are both proper prefix and suffix.
  - From the above two points, we can conclude that we do not need to match these lps[j-1] characters with txt[i-j...i-1] because we know that these characters will anyway match.

Code:

    void KMPSearch(char* pat, char* txt)
    {
        int M = strlen(pat);
        int N = strlen(txt);

        // create lps[] that will hold the longest prefix suffix
        // values for pattern
        int lps[M];

        // Preprocess the pattern (calculate lps[] array)
        computeLPSArray(pat, M, lps);

        int i = 0; // index for txt[]
        int j = 0; // index for pat[]
        while ((N - i) >= (M - j)) {
            if (pat[j] == txt[i]) {
                j++;
                i++;
            }

            if (j == M) {
                printf("Found pattern at index %d ", i - j);
                j = lps[j - 1];
            }

            // mismatch after j matches
            else if (i < N && pat[j] != txt[i]) {
                // Do not match lps[0..lps[j-1]] characters,
                // they will match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }
    }

    // Fills lps[] for given pattern pat[0..M-1]
    void computeLPSArray(char* pat, int M, int* lps)
    {
        // length of the previous longest prefix suffix
        int len = 0;

        lps[0] = 0; // lps[0] is always 0

        // the loop calculates lps[i] for i = 1 to M-1
        int i = 1;
        while (i < M) {
            if (pat[i] == pat[len]) {
                len++;
                lps[i] = len;
                i++;
            }
            else // (pat[i] != pat[len])
            {
                // This is tricky. Consider the example.
                // AAACAAAA and i = 7. The idea is similar
                // to search step.
                if (len != 0) {
                    len = lps[len - 1];

                    // Also, note that we do not increment
                    // i here
                }
                else // if (len == 0)
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }
