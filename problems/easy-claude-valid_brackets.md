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

## solution

Approach

Use a stack. Walk through the string:

On an opening bracket, push it.
On a closing bracket, pop the top of the stack. If the stack is empty or the popped bracket doesn’t match, return false.
At the end, the string is valid only if the stack is empty (no unclosed openers).

Time: O(n), one pass. Space: O(n) worst case, e.g. "(((((".

TypeScript
typescript
function isValid(s: string): boolean {
  const closeToOpen: Record<string, string> = {
    ")": "(",
    "]": "[",
    "}": "{",
  };
  const stack: string[] = [];

  for (const ch of s) {
    if (ch in closeToOpen) {
      // pop() returns undefined on an empty stack, which never matches
      if (stack.pop() !== closeToOpen[ch]) return false;
    } else {
      stack.push(ch);
    }
  }

  return stack.length === 0;
}

// Quick checks
console.log(isValid("()[]{}")); // true
console.log(isValid("([)]"));   // false
console.log(isValid("(("));     // false
console.log(isValid(""));       // true
Rust
rust
pub fn is_valid(s: &str) -> bool {
    let mut stack: Vec<char> = Vec::new();

    for ch in s.chars() {
        match ch {
            '(' | '[' | '{' => stack.push(ch),
            ')' | ']' | '}' => {
                let expected = match ch {
                    ')' => '(',
                    ']' => '[',
                    _ => '{',
                };
                // pop() returns None on an empty stack, which never matches
                if stack.pop() != Some(expected) {
                    return false;
                }
            }
            _ => {} // constraints say this can't happen
        }
    }

    stack.is_empty()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn examples() {
        assert!(is_valid("()[]{}"));
        assert!(is_valid("{[]}"));
        assert!(is_valid(""));
        assert!(!is_valid("([)]"));
        assert!(!is_valid("(("));
        assert!(!is_valid(")"));
    }
}
Notes on the two implementations
Both rely on the same trick: popping from an empty stack yields “nothing” (undefined / None), which can never equal a real bracket, so the empty-stack case is handled without a separate check.
In Rust, Vec<char> works fine here. For raw performance on ASCII-only input you could iterate over s.bytes() and use Vec<u8>, but char is clearer for an interview.
Likely interviewer follow-ups
Early exit optimization: if s.length is odd, return false immediately. Why does this work?
Space optimization: if only one bracket type existed, you could replace the stack with a single counter. Why does that break with multiple types?
Extension: how would you return the index of the first offending bracket instead of a boolean?