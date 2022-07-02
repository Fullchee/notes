## Edge cases

-   Empty
-   Length
    -   Extremely Long
    -   Odd/even length string
-   Encoded string
    -   HTTPResponse binary, need to `.decode()`
    -   UTF-8
-   Null (as argument)
-   C: non null terminated string

## String Search

### KMP Substring

-   https://leetcode.com/problems/implement-strstr/
-   https://youtu.be/BXCEFAzhxGY
-   look for repeating prefix/suffix
    -   so that you can take advantage of the work you already did
-   Time complexity
    -   Calculating prefixes takes one traversal through the pattern
    -   comparing the pattern to the string takes one traversal through the string
