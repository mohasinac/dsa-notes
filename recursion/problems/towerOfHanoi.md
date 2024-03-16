[back](../recursion.md)

# Tower of Hanoi

**Tower of Hanoi** is a mathematical puzzle where we have three rods (A, B, and C) and N disks.

Initially, all the disks are stacked in decreasing value of diameter i.e., the smallest disk is placed on the top and they are on rod A.

The objective of the puzzle is to move the entire stack to another rod (here considered C), obeying the following simple rules:

1. Only one disk can be moved at a time.

2. Each move consists of taking the upper disk from one of the stacks and placing it on top of another stack i.e. a disk can only be moved if it is the uppermost disk on a stack.

3. No disk may be placed on top of a smaller disk.

Examples:

    Input: 2
    Output: Disk 1 moved from A to B
    Disk 2 moved from A to C
    Disk 1 moved from B to C

    Input: 3
    Output: Disk 1 moved from A to C
    Disk 2 moved from A to B
    Disk 1 moved from C to B
    Disk 3 moved from A to C
    Disk 1 moved from B to A
    Disk 2 moved from B to C
    Disk 1 moved from A to C

Tower of Hanoi using Recursion:

The idea is to use the helper node to reach the destination using recursion. Below is the pattern for this problem:

- Shift ‘N-1’ disks from ‘A’ to ‘B’, using C.
- Shift last disk from ‘A’ to ‘C’.
- Shift ‘N-1’ disks from ‘B’ to ‘C’, using A.

![alt text](tower-of-hanoi.png)

Follow the steps below to solve the problem:

- Create a function towerOfHanoi where pass the N (current number of disk), from_rod, to_rod, aux_rod.
- Make a function call for N – 1 th disk.
- Then print the current the disk along with from_rod and to_rod
- Again make a function call for N – 1 th disk.

Code:

        void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod)
        {
            if (n == 0) {
                return;
            }
            towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);
            cout << "Move disk " << n << " from rod " << from_rod<< " to rod " << to_rod << endl;
            towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);
        }

input:

        int N = 2;

        // A, B and C are names of rods

        towerOfHanoi(N, 'A', 'C', 'B');

Representation:

                2, A, C, B
                    -> 1, A, B, C
                        -> 0, A, C, B
                            -> return
                        -> Print Move disk 1 from A to B
                        -> 0, C, B, A
                            -> return
                    -> Print Move disk 2 from A to C
                    -> 1, B, C, A
                        -> 0, B, A, C
                            -> reurn
                        -> Print Move disk 1 from B to C
                        -> 0, A, C, B
                            -> return

Homework4 : Illustrate Tower of hanoi for N = 3, A, B, C rods
