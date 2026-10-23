# valid brackets problem

Claude generated

## problem

Exercise 1: Valid Brackets (Easy)
Problem

Given a string s containing only the characters (, ), [, ], {, and }, determine whether it is valid.

A string is valid if:

Every opening bracket is closed by the same type of bracket.
Brackets are closed in the correct order.
Every closing bracket has a matching opening bracket before it.
Examples
Input	Output	Why
"()"	true	Simple match
"()[]{}"	true	Three matched pairs in sequence
"{[]}"	true	Properly nested
"(]"	false	Wrong closing type
"([)]"	false	Closed in the wrong order
"(("	false	Unclosed brackets
")"	false	Closing bracket with nothing to match
""	true	Empty string is valid
Constraints
0 <= s.length <= 10^4
s consists only of the six bracket characters above.
Things to think about before coding
What data structure naturally models “the most recent unclosed thing”?
What edge cases can make a naive approach fail? (Try ")(" and "((".)
What’s the best time and space complexity you can achieve?