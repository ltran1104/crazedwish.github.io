---
layout: post
title: Egg Drop Solution
---
Solution to Google Problem from the First Computer Science Club Meeting
Dr. Richard W. McHard

The problem below, posed by Google, was stated at the first Computer Science Club Meeting, held Friday, October 6, 2017.

Suppose there is a building with 100 floors.  Suppose further that there is a highest floor from which you can drop an egg without it breaking.  If you drop an egg from that floor, or from any lower floor, you are guaranteed that the egg will not be broken or damaged.  If you drop an egg from any higher floor, you are guaranteed that the egg will break.  Suppose you have two eggs.  Given the two eggs, find the minimum number of drops of an egg to find the highest floor from which you can drop an egg without it breaking.  It is OK if both eggs break, as long as you know the answer as soon as that happens.  You cannot drop an egg after it is broken, but you can keep using an egg for testing if it is not broken.

The problem statement tempts us to assume that there is at least one floor from which an egg will not break if dropped, and at least one floor from which an egg will break if dropped.  This would imply that an egg would not break if dropped from floor 1, and an egg would break if dropped from floor 100.  This assumption is not necessary; our solution is floor 100 if an egg does not break if dropped from any floor, and we can say that the solution is floor 0 (nonexistent) if an egg breaks if dropped from floor 1.

The solution, shown below, uses at most 14 egg drops.  An explanation is given after the table.

0	14	27	39	50	60	69	77	84	90	95	99	100
	1	15	28	40	51	61	70	78	85	91	96
	2	16	29	41	52	62	71	79	86	92	97
	3	17	30	42	53	63	72	80	87	93	98
	4	18	31	43	54	64	73	81	88	94
	5	19	32	44	55	65	74	82	89
	6	20	33	45	56	66	75	83
	7	21	34	46	57	67	76
	8	22	35	47	58	68
	9	23	36	48	59
	10	24	37	49
	11	25	38
	12	26
	13

Go to the floors indicated in the top row, from left to right (skipping 0), and drop an egg until it breaks.  Then go to the floors listed below this floor, from top to bottom, and drop the remaining unbroken egg until it breaks.  If the second egg breaks just after the first egg breaks (e.g., 50 breaks, then 40 breaks), the highest floor at which an egg will not break if dropped is the head of the previous column (e.g., 39).  If the second egg breaks any later (e.g., 50 breaks, 40 does not break, 41 breaks), the highest floor at which an egg will not break if dropped is the preceding entry in the sequence (e.g., 40).  If the second egg does not break (e.g., 50 breaks but 49 does not break), the last entry in the sequence (e.g., 49) is the highest floor at which an egg will not break if dropped.  The number of floors in the sequence is the number of drops.  This handles the case in which an egg never breaks, since the last egg never breaks and 100 is the last entry in the sequence.  Furthermore, if there is an initial column with 0 as its only entry, this handles the case in which an egg always breaks; the solution (floor 0) is not an actual floor.

How can we approach this problem?  A “brute force” way is to start at floor 1 and drop an egg at each floor, moving up one floor at a time, until an egg breaks for the first time.  The solution is the floor immediately below the floor where this occurs.  But a moment’s reflection will suggest there must be a better way to solve this problem – after all, we could solve the problem this way with just one egg!

Since we have two eggs, we consider a variation of “divide and conquer” to solve this problem.  Systematically skip over some floors and drop one of the eggs at chosen floors until it breaks.  Then go back to the most recent floor where the egg did not break and test the second egg at all the floors in between.  As before, the solution is the floor just below the floor where this second egg breaks.

As a first approach, we might consider testing at fixed floor multiples; e.g., at floors 10, 20, 30, . . . .  But a moment’s reflection will tell us that we can afford to skip more floors at the beginning, since we only have to test the first egg once to find out that the solution is in the set of floors before the first drop, whereas we must test the first egg twice to find out that the solution is between the first two trial floors for the first egg.  In fact, we want to find out how to select test floors for the first egg so that the number of tests using the first egg plus the number of tests for the second egg remains the same.

So if we want to drop an egg at most t times, the first floor that we test with the first egg should be at floor t.  Then, if the egg breaks at floor t, we have the other egg to test floors 1, 2, . . . , t – 1.  But if the egg does not break at floor t, we cannot move all the way out to floor 2 * t, because if the first egg breaks there, we had to use 2 tests to find that out.  We don’t have t – 1 tests left.  So the second floor that we test with the first egg can only be t – 1 floors past the first floor that we test with the first egg.  This is floor t + (t – 1).  If the first egg breaks here, we have used 2 tests and we can use the remaining egg to test the floors t + 1, t + 2, . . . , t + (t – 2), requiring a total of 2 + (t – 2) = 2 * t tests.

This generalizes as follows.  Our third drop of the first egg can only be (t – 2) floors past the second drop, or floor t + (t – 1) + (t – 2), so we can test floor t + (t – 1) + 1 through floor t + (t – 1 ) + (t – 3) with the second egg, a total of t drops of the two eggs.  In general, if the first egg breaks at drop d, the floor where we did this drop must have been floor t + (t – 1) + . . . + (t – d + 1), requiring t – d drops of the second egg.  We cannot have more than t drops, so drops of the first egg must stop when d = t; i.e., at floor t + (t – 1) + . . . + (t – t + 1) = t + (t – 1) +  . . . + 1, leaving t – t = 0 drops for the second egg.

By a well-known formula from algebra, t + (t – 1) + . . . + (t – t + 1) = t + (t – 1) +  . . . + 1 = t * (t + 1) / 2.  Furthermore, this number must be at least 100 if we are to cover all possible floors.  For a moment, we introduce a simplifying assumption that there is at least one floor where an egg will not break when dropped, and at least one floor where an egg will break when dropped.  This implies that floor 1 and floor 100 do not have to be tested.  Then we must have t * (t + 1) / 2 >= 98, and so t * (t + 1) >= 196.

It happens that 196 = 142 = 14 * 14, so t = 13 is too small; 13 * 14 < 14 * 14 = 196.  But t = 14 works:
14 * 15 >= 14 * 14 = 196.

In fact, 14 * 15 = 210 > 200, so 14 + 13 + 12 + . . . + 1 = 14 * 15 / 2 = 105 > 100.  Thus 14 is the minimum number of drops required to find the highest floor where the egg won’t break when it is dropped.  Furthermore, we don’t need to assume that an egg will not break at floor 1, or that an egg will break at floor 100.

Code that implements this solution is shown on the following page.
```java
import java.util.*;

public class GoogleEggProblem
{
	public static void main(String args[]) 
	{
		Scanner scan = new Scanner(System.in);
		System.out.print("highest = ");
		int highest = scan.nextInt();
		int previous = 0;
		int current = 0;
		int count = 0;
		boolean broke1 = false;
		// drop the first egg
		for(int delta = 14; delta > 0 && !broke1; delta--)
		{
			current = previous + delta;
			if(current > 100)
			{
				current = 100;
				delta = 0;
			}
			count++; // count the egg to be dropped
			System.out.println(current); // and print the floor
			if(current <= highest) // drop the first egg
			{
				previous = current;
			}
			else
			{
				broke1 = true;
			}
		}
		// drop the second egg
		int floor;
		boolean broke2 = false;
		for(floor = previous + 1; floor < current && !broke2;)
		{
			count++; // count the egg to be dropped
			System.out.println(floor); // and print the floor
			if(floor <= highest) // drop the second egg
			{
				floor++;
			}
			else
			{
				broke2 = true;
			}
		}
		if(!broke1)
		{
			floor = 100;
		}
		else
		{
			floor--;
		}
		System.out.println("solution = " + floor);
		System.out.println("highest  = " + highest);
		System.out.println("drops    = " + count);
	}
}
```
This approach generalizes in the obvious way.  If there are f floors, you want to find the smallest t such that t * (t + 1) / 2 >= f.  This value of t is the smallest number of drops of 2 eggs required to find the highest of the f floors at which an egg will not break if dropped.

A more interesting generalization question is:  what happens if we add more eggs?


