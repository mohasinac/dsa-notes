# Naive Pattern Searching Algorithm

Given a text txt[0..n-1] and a pattern pat[0..m-1], write a function search(char pat[], char txt[]) that prints all occurrences of pat[] in txt[]. You may assume that n > m.

Examples:

    Input:  txt[] = "THIS IS A TEST TEXT"
            pat[] = "TEST"
    Output: Pattern found at index 10

    Input:  txt[] =  "AABAACAADAABAABA"
            pat[] =  "AABA"
    Output: Pattern found at index 0
            Pattern found at index 9
            Pattern found at index 12

![Alt text](Pattern-Searching-2-1.png)

Pattern searching is an important problem in computer science. When we do search for a string in notepad/word file or browser or database, pattern searching algorithms are used to show the search results.

Naive Pattern Searching: The idea is to slide the pattern over text one by one and check for a match. If a match is found, then slides by 1 again to check for subsequent matches.

That is check for the match of the first character of the pattern in the string, if it matches then check for the subsequent characters of the pattern with the respective characters of the string. If a mismatch is found then move forward in the string.

Code:

    void search(char* pat, char* txt)
    {
        int M = strlen(pat);
        int N = strlen(txt);

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            int j;

            /* For current index i, check for pattern match */
            for (j = 0; j < M; j++)
                if (txt[i + j] != pat[j])
                    break;

            if (j == M) // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
                cout << "Pattern found at index "
                    << i << endl;
        }
    }
