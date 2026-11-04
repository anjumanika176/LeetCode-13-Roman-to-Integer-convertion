# LeetCode 13: Roman to Integer

## Problem
Roman numerals use seven symbols:

| Symbol | Value |
|--------|-------|
| I | 1 |
| V | 5 |
| X | 10 |
| L | 50 |
| C | 100 |
| D | 500 |
| M | 1000 |

Numerals are usually written from largest to smallest, left to right, and the values are added.
In six cases a smaller symbol is placed before a larger one, and it is subtracted:

- `IV` = 4, `IX` = 9
- `XL` = 40, `XC` = 90
- `CD` = 400, `CM` = 900

Given a valid Roman numeral, convert it to an integer.

## Examples

| Input | Output | Explanation |
|-------|--------|-------------|
| `"III"` | `3` | 1 + 1 + 1 |
| `"LVIII"` | `58` | 50 + 5 + 1 + 1 + 1 |
| `"MCMXCIV"` | `1994` | 1000 + 900 + 90 + 4 |

## Constraints
- `1 <= s.length <= 15`
- `s` contains only `I, V, X, L, C, D, M`
- `s` is a valid Roman numeral in the range `[1, 3999]`

## Approach
Scan the string from left to right. For each symbol, look at the symbol on its right:

- If the current value is **smaller** than the next value, **subtract** it.
- Otherwise, **add** it.

This one rule covers all six special cases, so they do not need to be handled separately.

Example: `MCMXCIV`

| Symbol | Next | Action | Total |
|--------|------|--------|-------|
| M | C | add 1000 | 1000 |
| C | M | subtract 100 | 900 |
| M | X | add 1000 | 1900 |
| X | C | subtract 10 | 1890 |
| C | I | add 100 | 1990 |
| I | V | subtract 1 | 1989 |
| V | none | add 5 | 1994 |

## Solution (Python 3)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        values = {"I": 1, "V": 5, "X": 10, "L": 50, "C": 100, "D": 500, "M": 1000}
        total = 0

        for i in range(len(s)):
            if i + 1 < len(s) and values[s[i]] < values[s[i + 1]]:
                total = total - values[s[i]]
            else:
                total = total + values[s[i]]

        return total
```

## Solution (C)

```c
int value(char c) {
    switch (c) {
        case 'I': return 1;
        case 'V': return 5;
        case 'X': return 10;
        case 'L': return 50;
        case 'C': return 100;
        case 'D': return 500;
        case 'M': return 1000;
        default:  return 0;
    }
}

int romanToInt(char* s) {
    int total = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        int current = value(s[i]);
        int next = value(s[i + 1]);

        if (current < next) {
            total = total - current;
        } else {
            total = total + current;
        }
    }

    return total;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Concepts Used
- Dictionary / switch statement
- Left-to-right scan
- Add or subtract based on the next symbol

## Language
Python 3 and C

## Link
[https://leetcode.com/problems/roman-to-integer/]
