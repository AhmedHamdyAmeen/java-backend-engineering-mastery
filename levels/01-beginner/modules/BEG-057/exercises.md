# BEG-057 · Verifying AI-generated code — Exercises and lab

## Lab
### BEG-057-LAB1 · Trust but verify
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Ask an assistant for three methods from earlier labs: a search, a hash map operation, and a Library borrowing rule.
2. For each, write the tests first from the requirement (normal, boundary, invalid input); do not paste the generated code yet.
3. Paste the code, run the tests, and fix every failure. Document at least one defect found (what, how the test caught it, the fix).
4. Explain the final code in your own words in comments or the README, and add a disclosure line stating the AI use.
**Acceptance:** tests written before the code is pasted; at least one defect found and documented; final code explained in your own words in comments or the README.

## Exercises (assessment: given generated code with hidden defects, find them with tests; score = defects caught and explained)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-057-EX01 | 1 | Trace this generated code with `[3, 4]` and write what it returns and what it should: `int sum(int[] a){int s=0; for(int i=0;i<a.length-1;i++) s+=a[i]; return s;}` |
| BEG-057-EX02 | 2 | Write four tests, from the requirement only, for `int indexOf(int[] sorted, int target)` returning -1 when absent. |
| BEG-057-EX03 | 3 | Name the problem: a generated method calls `String.isNullOrEmpty(s)`. |
| BEG-057-EX04 | 3 | A generated "find duplicates" method uses `List.contains` inside a loop. State its complexity and a better approach. |
| BEG-057-EX05 | 2 | A teammate writes expected values by running the generated code and copying its output. Explain the risk. |
| BEG-057-EX06 | 4 | Write a two-sentence disclosure for code you drafted with an assistant, and list two things you must never paste into a public assistant. |

## Solutions
- **EX01** Returns 3 (loop stops one early, skips the last item); it should return 7. The bound should be `i < a.length`.
- **EX02** For example: `[]` with 5 gives -1; `[5]` with 5 gives 0; `[1,3,5,7]` with 7 gives 3; `[1,3,5,7]` with 4 gives -1.
- **EX03** An invented method: `String` has no static `isNullOrEmpty`. Use `s == null || s.isEmpty()` (or `isBlank` if blank counts).
- **EX04** O(n²) because `contains` is O(n). Use a `HashSet`: O(n) time, O(n) space.
- **EX05** The test then copies any bug into the expectations and cannot fail; expected values must come from the requirement.
- **EX06** For example: "Binary search was first drafted with an AI assistant. I wrote the tests from the requirement, found and fixed a boundary bug, and can explain every line." Never paste secrets or credentials, customer or personal data, or private code (check your policy).
