# How to Think About and Prepare for Algorithm Problems

This is a short, opinionated orientation for the coding problems in this repository. It is deliberately **not exhaustive**; treat it as an annotated reading list. Skim it to see the shape of the territory, then follow the linked sources — they are the real authority — at your own pace.

The guidance is language-agnostic; the concrete demonstrations use **TypeScript** and **Rust**, the two languages used throughout this repo.

## 1. Use a repeatable method, not intuition

Strong problem-solvers follow the same loop, popularized by [George Pólya's *How to Solve It*](https://en.wikipedia.org/wiki/How_to_Solve_It) and adapted for interviews by [Gayle Laakmann McDowell in *Cracking the Coding Interview*](https://www.crackingthecodinginterview.com/):

1. **Understand** — restate the inputs, outputs, and constraints in your own words.
2. **Plan** — find an algorithm on paper before typing; start with brute force.
3. **Implement** — translate the plan into clean code.
4. **Review** — test edge cases, then analyze and optimize.

Pólya's book is the classic source of the "understand → devise a plan → carry it out → look back" cycle; McDowell's book shows that same cycle applied specifically to software interviews.

## 2. Measure what you write: complexity and correctness

Before optimizing, be able to *say* how fast and how much memory an algorithm uses.

- **Big O notation** describes how runtime and space grow with input size. Start with the [Wikipedia article on Big O notation](https://en.wikipedia.org/wiki/Big_O_notation) and its [time complexity](https://en.wikipedia.org/wiki/Time_complexity) companion.
- **Correctness** is argued with loop *invariants* and *induction*. The standard reference is [*Introduction to Algorithms* (CLRS) by Cormen, Leiserson, Rivest, and Stein](https://mitpress.mit.edu/9780262046305/introduction-to-algorithms/).
- For a video alternative, [MIT OpenCourseWare 6.006 (Introduction to Algorithms)](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/) and Princeton's [Algorithms, Part I & II](https://www.coursera.org/learn/algorithms-part1) are excellent and free.

Every problem document in this repo states its target time and space complexity — confirm your solution matches before calling it done.

## 3. Choose the right data structure and pattern

Recognition is most of the battle. Two references cover the "toolbox" especially well:

- [Steven Skiena, *The Algorithm Design Manual*](https://www.algorist.com/) — a catalog of real problems and the techniques that solve them.
- [Robert Sedgewick & Kevin Wayne, *Algorithms* (4th ed.)](https://algs4.cs.princeton.edu/) — rigorous, code-heavy, with a free companion course.

The techniques that recur most in this repo (and in interviews): hash maps, two pointers, sliding window, prefix sums, binary search, stack/queue, DFS/BFS on graphs, dynamic programming, greedy, and backtracking. For fast, well-credited write-ups of specific algorithms, [cp-algorithms.com](https://cp-algorithms.com/) is the best free reference. [LeetCode's "Learn" tracks](https://leetcode.com/explore/learn/) and the widely-cited [Blind 75 list](https://www.teamblind.com/post/New-Year-Gift---Curated-List-of-Top-75-LeetCode-Questions-to-Save-Your-Time-OaM1orEU) (and its popular successor [NeetCode](https://neetcode.io/)) group problems by exactly these patterns.

## 4. Hunt edge cases and test like it ships

Interviews are lost on edge cases, not the happy path. Before writing, list: empty input, single element, all-equal values, negative numbers, integer overflow, and off-by-one boundaries — then encode them as tests.

- *Cracking the Coding Interview* devotes a chapter to testing and edge-case strategy.
- This repo treats tests as first-class: every Rust reference solution (in `solutions/`) carries a `#[cfg(test)]` block, and every TypeScript reference solution carries `console.log` checks.

## 5. When you're stuck: simplify, then recover

- Solve a smaller or simpler version first, then generalize (Pólya's "solve a related problem").
- Write the brute force even if it is O(n²): a correct slow answer beats a clever broken one, and it gives you a reference to test the fast version against.
- Step through a tiny input by hand, the way the trace tables in this repo's docs do. [Jon Bentley's *Programming Pearls*](https://en.wikipedia.org/wiki/Programming_Pearls) is full of worked, hand-traced examples and is the best book for this habit.

## 6. Demonstration: one idea, two languages

The **two-sum** problem solved with a hash map. The point is the parallel, not the syntax:

**TypeScript**

```typescript
function twoSum(nums: number[], target: number): number[] {
  const seen = new Map<number, number>(); // value -> index
  for (const [i, num] of nums.entries()) {
    const complement = target - num;
    const found = seen.get(complement);
    if (found !== undefined) {
      return [found, i];
    }
    seen.set(num, i);
  }
  return [];
}
```

**Rust**

```rust
pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
    use std::collections::HashMap;

    let mut seen: HashMap<i32, usize> = HashMap::new(); // value -> index
    for (i, &num) in nums.iter().enumerate() {
        let complement = target - num;
        if let Some(&j) = seen.get(&complement) {
            return vec![j as i32, i as i32];
        }
        seen.insert(num, i);
    }
    vec![]
}
```

Same idea in both: remember values you've seen and look up the complement in O(1). The differences worth noticing: TypeScript signals "not found" with `undefined`, while Rust uses `Option` (`Some` / `None`); and Rust needs the `as i32` cast to turn a `usize` index into the `Vec<i32>` return type.

For the full step-by-step syntax breakdown of this and every other problem, open [its document](../problems/easy/two_sum.md) — each one explains the TypeScript and Rust line by line.

**Language references:**

- TypeScript — [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) and the [MDN JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript).
- Rust — [The Rust Programming Language ("The Book")](https://doc.rust-lang.org/book/), [Rust by Example](https://doc.rust-lang.org/rust-by-example/), the [standard library docs](https://doc.rust-lang.org/std/), and the [Rustlings exercises](https://github.com/rust-lang/rustlings).
- PHP (lower priority) — [PHP Manual](https://www.php.net/manual/).

## 7. Practice deliberately, not just more

- Prefer a small number of problems done *slowly* — attempt independently, compare against the reference solution, then re-implement from memory — over skimming many.
- Spaced repetition and deliberate practice (see the research on [deliberate practice](https://en.wikipedia.org/wiki/Practice_(learning_method))) beat cramming.
- Use [this repo's problem catalog](../problems/README.md), which orders problems by difficulty and topic, as your queue.

## Reference list

**Books**

- Pólya, G. — *How to Solve It*. [Wikipedia](https://en.wikipedia.org/wiki/How_to_Solve_It)
- Cormen, Leiserson, Rivest, Stein — *Introduction to Algorithms* (CLRS). [MIT Press](https://mitpress.mit.edu/9780262046305/introduction-to-algorithms/)
- Skiena, S. — *The Algorithm Design Manual*. [algorist.com](https://www.algorist.com/)
- McDowell, G. L. — *Cracking the Coding Interview*. [crackingthecodinginterview.com](https://www.crackingthecodinginterview.com/)
- Sedgewick, R. & Wayne, K. — *Algorithms* (4th ed.). [algs4.cs.princeton.edu](https://algs4.cs.princeton.edu/)
- Bentley, J. — *Programming Pearls*. [Wikipedia](https://en.wikipedia.org/wiki/Programming_Pearls)

**Courses & lectures**

- MIT OpenCourseWare 6.006 — *Introduction to Algorithms*. [ocw.mit.edu](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/)
- Princeton — *Algorithms, Part I & II* (Sedgewick/Wayne). [Coursera](https://www.coursera.org/learn/algorithms-part1)

**Web references**

- Big O notation — [Wikipedia](https://en.wikipedia.org/wiki/Big_O_notation); Time complexity — [Wikipedia](https://en.wikipedia.org/wiki/Time_complexity)
- *Algorithms for Competitive Programming* — [cp-algorithms.com](https://cp-algorithms.com/)
- LeetCode Learn — [leetcode.com/explore/learn](https://leetcode.com/explore/learn/)
- Blind 75 — [original curated list](https://www.teamblind.com/post/New-Year-Gift---Curated-List-of-Top-75-LeetCode-Questions-to-Save-Your-Time-OaM1orEU)
- NeetCode — [neetcode.io](https://neetcode.io/)
- USACO Guide — [usaco.guide](https://usaco.guide/)

**Language documentation**

- TypeScript Handbook — [typescriptlang.org](https://www.typescriptlang.org/docs/handbook/intro.html)
- MDN JavaScript — [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- The Rust Book — [doc.rust-lang.org/book](https://doc.rust-lang.org/book/)
- Rust by Example — [doc.rust-lang.org/rust-by-example](https://doc.rust-lang.org/rust-by-example/)
- Rust standard library — [doc.rust-lang.org/std](https://doc.rust-lang.org/std/)
- Rustlings — [github.com/rust-lang/rustlings](https://github.com/rust-lang/rustlings)
