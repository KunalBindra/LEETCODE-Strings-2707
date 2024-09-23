# LEETCODE-Strings-2707
Let’s do a dry run of the code to understand how it works.

### Problem Understanding
This function aims to compute the minimum number of extra characters required to partition the string `s` such that each partition is either present in the `dictionary` or consists of extra characters.

- `s`: Input string.
- `dictionary`: Array of valid words.
- `dp[i]`: The minimum extra characters if breaking up `s[0..i)` optimally.

### Dry Run Example
Let's take an example input:
```plaintext
s = "applepie"
dictionary = ["apple", "pie"]
```

We’ll break down the string to minimize extra characters by using the valid words in the dictionary.

### Step-by-Step Execution

1. Initialize `dictionarySet` with the words from the `dictionary`:
   ```plaintext
   dictionarySet = {"apple", "pie"}
   ```

2. Initialize the `dp` array where `dp[i]` will store the minimum number of extra characters needed for the substring `s[0..i)`. Initially, we set `dp[0] = 0` (no extra chars for an empty string) and `dp[i] = n` for all other `i`, since we assume the worst case (all characters are extra):
   ```plaintext
   dp = [0, 8, 8, 8, 8, 8, 8, 8, 8]  // 8 because s.length() = 8
   ```

3. Start iterating through each index `i` of the string `s`:

   - **i = 1**:
     - For `j = 0`, substring `s[0..1) = "a"` is not in `dictionarySet`. Hence, update `dp[1]`:
       ```plaintext
       dp[1] = min(dp[1], dp[0] + 1) = min(8, 0 + 1) = 1
       ```
     - `dp` now: `[0, 1, 8, 8, 8, 8, 8, 8, 8]`.

   - **i = 2**:
     - For `j = 0`, substring `s[0..2) = "ap"` is not in `dictionarySet`. Update `dp[2]`:
       ```plaintext
       dp[2] = min(dp[2], dp[0] + 2) = min(8, 0 + 2) = 2
       ```
     - For `j = 1`, substring `s[1..2) = "p"` is not in `dictionarySet`. Update `dp[2]`:
       ```plaintext
       dp[2] = min(dp[2], dp[1] + 1) = min(2, 1 + 1) = 2
       ```
     - `dp` now: `[0, 1, 2, 8, 8, 8, 8, 8, 8]`.

   - **i = 3**:
     - For `j = 0`, substring `s[0..3) = "app"` is not in `dictionarySet`. Update `dp[3]`:
       ```plaintext
       dp[3] = min(dp[3], dp[0] + 3) = min(8, 0 + 3) = 3
       ```
     - For `j = 1`, substring `s[1..3) = "pp"` is not in `dictionarySet`. Update `dp[3]`:
       ```plaintext
       dp[3] = min(dp[3], dp[1] + 2) = min(3, 1 + 2) = 3
       ```
     - For `j = 2`, substring `s[2..3) = "p"` is not in `dictionarySet`. Update `dp[3]`:
       ```plaintext
       dp[3] = min(dp[3], dp[2] + 1) = min(3, 2 + 1) = 3
       ```
     - `dp` now: `[0, 1, 2, 3, 8, 8, 8, 8, 8]`.

   - **i = 4**:
     - For `j = 0`, substring `s[0..4) = "appl"` is not in `dictionarySet`. Update `dp[4]`:
       ```plaintext
       dp[4] = min(dp[4], dp[0] + 4) = min(8, 0 + 4) = 4
       ```
     - For `j = 1`, substring `s[1..4) = "ppl"` is not in `dictionarySet`. Update `dp[4]`:
       ```plaintext
       dp[4] = min(dp[4], dp[1] + 3) = min(4, 1 + 3) = 4
       ```
     - For `j = 2`, substring `s[2..4) = "pl"` is not in `dictionarySet`. Update `dp[4]`:
       ```plaintext
       dp[4] = min(dp[4], dp[2] + 2) = min(4, 2 + 2) = 4
       ```
     - For `j = 3`, substring `s[3..4) = "l"` is not in `dictionarySet`. Update `dp[4]`:
       ```plaintext
       dp[4] = min(dp[4], dp[3] + 1) = min(4, 3 + 1) = 4
       ```
     - `dp` now: `[0, 1, 2, 3, 4, 8, 8, 8, 8]`.

   - **i = 5**:
     - For `j = 0`, substring `s[0..5) = "apple"` is in `dictionarySet`. Update `dp[5]`:
       ```plaintext
       dp[5] = min(dp[5], dp[0]) = min(8, 0) = 0
       ```
     - For `j = 1`, substring `s[1..5) = "pple"` is not in `dictionarySet`. No change.
     - For `j = 2`, substring `s[2..5) = "ple"` is not in `dictionarySet`. No change.
     - For `j = 3`, substring `s[3..5) = "le"` is not in `dictionarySet`. No change.
     - For `j = 4`, substring `s[4..5) = "e"` is not in `dictionarySet`. No change.
     - `dp` now: `[0, 1, 2, 3, 4, 0, 8, 8, 8]`.

   - **i = 6**:
     - For `j = 0`, substring `s[0..6) = "applep"` is not in `dictionarySet`. Update `dp[6]`:
       ```plaintext
       dp[6] = min(dp[6], dp[0] + 6) = min(8, 0 + 6) = 6
       ```
     - For `j = 1`, substring `s[1..6) = "pplep"` is not in `dictionarySet`. Update `dp[6]`:
       ```plaintext
       dp[6] = min(dp[6], dp[1] + 5) = min(6, 1 + 5) = 6
       ```
     - For `j = 2`, substring `s[2..6) = "plep"` is not in `dictionarySet`. No change.
     - For `j = 3`, substring `s[3..6) = "lep"` is not in `dictionarySet`. No change.
     - For `j = 4`, substring `s[4..6) = "ep"` is not in `dictionarySet`. No change.
     - For `j = 5`, substring `s[5..6) = "p"` is not in `dictionarySet`. No change.
     - `dp` now: `[0, 1, 2, 3, 4, 0, 6, 8, 8]`.

   - **i = 7**:
     - For `j = 0`, substring `s[0..7) = "applepi"` is not in `dictionarySet`. Update `dp[7]`:
       ```plaintext
       dp[7] = min(dp[7], dp[0] + 7) = min(8, 0 + 7) = 7
       ```
     - For `j = 1`, substring `s[1..7) = "pplepi"` is not in `dictionarySet`. Update `dp[7]`:
       ```plaintext
       dp[7] = min(dp[7], dp[1] + 6) = min(7, 1 + 6) = 7
       ```
     - For `j = 2`, substring `s[2..7) = "plepi"` is not in `dictionarySet`. No change.
     - For `j = 3`, substring `s[3..7) = "
