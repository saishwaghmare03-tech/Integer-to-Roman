# 12. Integer to Roman (Medium)

[![Java](https://img.shields.io/badge/Language-Java-orange.svg)](https://www.java.com)
[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow.svg)](https://leetcode.com/problems/integer-to-roman/)
[![Status](https://img.shields.io/badge/Status-Accepted-brightgreen.svg)]()

## 📌 Problem Description
Seven different symbols represent Roman numerals with the following values:

| Symbol | Value |
| :---: | :---: | 
| I | 1 |
| V | 5 |
| X | 10 |
| L | 50 |
| C | 100 |
| D | 500 |
| M | 1000 |

Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. For example, to convert an integer, we select the maximal value that can be subtracted, handle subtractive forms (like `IV` for 4, `IX` for 9, `XL` for 40, etc.), and concatenate the symbols.

* **Constraints:** `1 <= num <= 3999`

---

## 💡 Approach (Greedy Algorithm)
1. **Pre-computed Mappings:** Create two parallel arrays (`values` and `symbols`) containing all standard Roman values and their subtractive pairs in descending order (`1000, 900, 500, 400, ...`).
2. **Greedy Subtraction:** Iterate through the arrays, and for each value, use a `while` loop to subtract it from `num` as many times as possible while appending its corresponding Roman symbol to a `StringBuilder`.
3. **Early Exit:** Once `num` reaches `0`, the conversion is complete.

---

## ⏱️ Complexity Analysis
* **Time Complexity:** $O(1)$ — Since the maximum input is `3999`, the number of iterations is strictly bounded by a small constant.
* **Space Complexity:** $O(1)$ — Uses a constant amount of extra space for the `StringBuilder` and arrays.

---

## 💻 Java Solution

```java
public class Solution {
    public String intToRoman(int num) {
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        
        StringBuilder result = new StringBuilder();
        
        for (int i = 0; i < values.length && num > 0; i++) {
            while (num >= values[i]) {
                num -= values[i];
                result.append(symbols[i]);
            }
        }
        
        return result.toString();
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        
        // Test cases
        System.out.println(solution.intToRoman(3749)); // Output: MMMDCCXLIX
        System.out.println(solution.intToRoman(58));   // Output: LVIII
        System.out.println(solution.intToRoman(1994)); // Output: MCMXCIV
    }
}
