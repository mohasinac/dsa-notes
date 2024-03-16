[back](./../contents.md)

1.  Recursion Introduction:

    Recursion is a way to solve a problem or way to write a program in which a function calls itself directly or indirectly.

    - Direct vs Indirect Recursion:

      In direct recursion, function calls itself while in indirect recursion the function fun1 calls another function fun2 which calls the fun1 function.

      Direct Recursion:

             void fun1() {
                 ...
                 ...
                 fun1();
                 ...
             }

      Indirect Recursion:

            void fun1() {
                ...
                ...
                fun2();
                ...
            }

            void fun2() {

                ...
                ...
                fun1();
                ...
            }

    - In a recursive program, the solution to the base case is provided and the solution of bigger problem is expressed in terms of smaller problems.

    - the smaller problems whose solutions are easy are generally known as **base cases**

    - without a base case , a function will recursively call themselves without any breaking condition, leading to StackOverflow or Segmentation Fault.

    - When any function is called from main(), the memory is allocated to it on stack. A recursive function calls itself, the memory for the called function is allocated on top of memory allocated to the calling function and a different copy of local variables is created for each function call. When the base case is reached, the function returns its value to the function by whom it is called and memory is de-allocated and the process continues.

    - Typical Structure of a Recursive Function

            ... fun(...) {
                Base Cases
                ... ...
                Recursive Call (i.e. call to fun())
                with atleast one change in parameter
                ... ...
            }

    - example :

      ![alt text](recursion.jpg)

    - **Disadvantage of Recursion**: Note that both recursive and iterative programs have the same problem-solving powers, i.e., every recursive program can be written iteratively and vice versa. A recursive program has greater space requirements than an iterative program as all functions will remain in the stack until the base case is reached. A recursive program also has greater time requirements because of function calls and return overhead.

    - **Advantages of Recursion**: Recursion provides a clean and simple way to write code. Some problems are inherently recursive like tree traversals, Tower of Hanoi, etc. For such problems, it is preferred to write recursive code. We can write such codes also iteratively with the help of the stack data structure.

2.  Print N to 1 Using Recursion:

    Given a number N, the task is to print the numbers from N to 1.

        void PrintReverseOrder(int N)
        {
            // if N is less than 1
            // then return void function
            if (N <= 0) {
                return;
            }
            else {
                cout << N << " ";

                // recursive call of the function
                PrintReverseOrder(N - 1);
            }
        }

3.  Print 1 to N Using Recursion:

    Given a number N, the task is to print the numbers from 1 to N.

        void printNos(unsigned int n)
        {
            if(n > 0)
            {
                printNos(n - 1);
                cout << n << " ";
            }
            return;
        }

4.  Tail Recursion:

    Tail Recursion: A recursive function is said to be following Tail Recursion if it invokes itself at the end of the function. That is, if all of the statements are executed before the function invokes itself then it is said to be following Tail Recursion.

    e.g.

        void printN(int N)
        {
            if(N==0)
                return;
            else
                cout<<N<<" ";

            printN(N-1);
        }

    - The tail-recursive functions are considered better than non-tail recursive functions as tail-recursion can be optimized by the compiler.
      The idea used by compilers to optimize tail-recursive functions is simple, since the recursive call is the last statement, there is nothing left to do in the current function, so saving the current function’s stack frame is of no use.

    Consider the following function to calculate factorial of N. Although it looks like Tail Recursive at first look, it is a non-tail-recursive function. If we take a closer look, we can see that the value returned by fact(N-1) is used in fact(N), so the call to fact(N-1) is not the last thing done by fact(N).

        int fact(int N)
        {
            if (N == 0)
                return 1;

            return N*fact(N-1);
        }

    The above function can be written as a Tail Recursive function. The idea is to use one more argument and accumulate the factorial value in the second argument. When N reaches 0, return the accumulated value.

        int factTR(int N, int a)
        {
            if (N == 0)
                return a;

            return factTR(N-1, N*a);
        }

5.  Natural Number Sum using Recursion:

    Given a number n, find sum of first n natural numbers. To calculate the sum, we will use a recursive function recur_sum().

    Examples :

        Input : 3
        Output : 6
        Explanation : 1 + 2 + 3 = 6

    Code:

        int recurSum(int n)
        {
            if (n <= 1)
                return n;
            return n + recurSum(n - 1);
        }

6.  Palindrome Check using Recursion:

    Given a string, write a recursive function that checks if the given string is a palindrome or not.

    Examples:

        Input : malayalam
        Output : Yes
        Reverse of malayalam is also
        malayalam.

        Input : max
        Output : No
        Reverse of max is not max.

    - Apoproach 1:

      The idea of a recursive function is simple:

      1.  If there is only one character in string
          return true.
      2.  Else compare first and last characters
          and recur for remaining substring.

                     bool isPalRec(char str[], int s, int e)
                     {

                         // If there is only one character
                         if (s == e)
                         return true;

                         // If first and last
                         // characters do not match
                         if (str[s] != str[e])
                         return false;

                         // If there are more than
                         // two characters, check if
                         // middle substring is also
                         // palindrome or not.
                         if (s < e + 1)
                         return isPalRec(str, s + 1, e - 1);

                         return true;
                     }

                     bool isPalindrome(char str[])
                     {
                         int n = strlen(str);

                         // An empty string is
                         // considered as palindrome
                         if (n == 0)
                             return true;

                         return isPalRec(str, 0, n - 1);
                     }

    - Approach 2:

      Basically while traversing check whether ith and n-i-1th index are equal or not.

      If there are not equal return false and if they are equal then continue with the recursion calls.

                bool isPalindrome(string s, int i){

                    if(i > s.size()/2){
                        return true ;
                    }

                    return s[i] == s[s.size()-i-1] && isPalindrome(s, i+1) ;

                }

7.  Sum of Digits Using Recursion:

    Given a number, we need to find sum of its digits using recursion.

    Examples:

        Input : 12345
        Output : 15

        Input : 45632
        Output :20

    Code:

                    int sum_of_digit(int n)
                    {
                        if (n == 0)
                        return 0;
                        return (n % 10 + sum_of_digit(n / 10));
                    }

8.  Rope Cutting Problem [>>](./problems/ropecuttingProblem.md)

9.  Generate Subsets [>>](./problems/generateSubsets.md)

10. Tower of Hanoi [>>](./problems/towerOfHanoi.md)

11. Josephus Problem [>>](./problems/josephusProblem.md)

12. Printing all Permutations [>>](./problems/permutations.md)
