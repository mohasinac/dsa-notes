# Reverse words in a given string

Reverse words in a given string

Let the input string be “i like this program very much”. The function should change the string to “much very program this like i”

![Alt text](reverse-Words.jpg)

    void reverseWords(string s)
    {

        // temporary vector to store all words
        vector<string> tmp;
        string str = "";
        for (int i = 0; i < s.length(); i++) {

            // Check if we encounter space
            // push word(str) to vector
            // and make str NULL
            if (s[i] == ' ') {
                tmp.push_back(str);
                str = "";
            }

            // Else add character to
            // str to form current word
            else
                str += s[i];
        }

        // Last word remaining,add it to vector
        tmp.push_back(str);

        // Now print from last to first in vector
        int i;
        for (i = tmp.size() - 1; i > 0; i--)
            cout << tmp[i] << " ";
        // Last word remaining,print it
        cout << tmp[0] << endl;
    }
