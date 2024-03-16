[back](../recursion.md)

# Josephus Problem

There are n people standing in a circle waiting to be executed. The counting out begins at some point in the circle and proceeds around the circle in a fixed direction. In each step, a certain number of people are skipped and the next person is executed. The elimination proceeds around the circle (which is becoming smaller and smaller as the executed people are removed), until only the last person remains, who is given freedom. Given the total number of persons n and a number k which indicates that k-1 persons are skipped and kth person is killed in a circle. The task is to choose the place in the initial circle so that you are the last one remaining and so survive.

For example,

if n = 5 and k = 2, then the safe position is 3.

    Firstly, the person at position 2 is killed.

    Then the person at position 4 is killed.

    Then the person at position 1 is killed.

    Finally, the person at position 5 is killed. So the person at position 3 survives.

The problem has following recursive structure.

    josephus(n, k) = (josephus(n - 1, k) + k-1) % n + 1
    josephus(1, k) = 1

Code:

        int josephus(int n, int k)
        {
        if (n == 1)
            return 1;
        else
            /* The position returned by josephus(n - 1, k) is adjusted because the recursive call josephus(n - 1, k) considers the original position k%n + 1 as position 1 */

            return ((josephus(n - 1, k) + k-1) % n )+ 1;
        }

Representation :

        n=5 and k=2

            J(5,2)
                -> J(4,2)+1 % 5 + 1
                    -> J(3,2)+1  % 4 + 1
                        -> J(2,2)+1 % 3 + 1
                            ->J(1,2)+1 % 2 + 1
                                => 1
                            => 1+1 % 2 + 1 = 2 % 2 + 1 = 1
                        => 1+1 % 3 + 1 = 3
                    => 3 + 1 % 4 + 1 = 1
                => 1+1 % 5 + 1 = 2 % 5 + 1 = 3
            => 3

        Answer: 3
