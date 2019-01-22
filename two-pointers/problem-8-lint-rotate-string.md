# Problem 8\(Lint\): Rotate String

## Description:

Given a string and an offset, rotate string by offset. \(rotate from left to right\)

## Example:

#### Example

```text
Example 1:
	Input: str="abcdefg", offset = 3
	Output:"efgabcd"
	
	Explanation: 
	Given a string and an offset, rotate string by offset. (rotate from left to right)

Example 2:
	Input: str="abcdefg", offset = 0
	Output: "abcdefg"
	
	Explanation: 
	Given a string and an offset, rotate string by offset. (rotate from left to right)

Example 3:
	Input: str="abcdefg", offset = 1
	Output: "gabcdef"
	
	Explanation: 
	Given a string and an offset, rotate string by offset. (rotate from left to right)

Example 4
	Input: str="abcdefg", offset =2
	Output:"fgabcde"
	
	Explanation: 
  Given a string and an offset, rotate string by offset. (rotate from left to right)
```

## Key points & Thoughts:

三次翻转法

## Solution:

```python
class Solution:
    """
    @param str: An array of char
    @param offset: An integer
    @return: nothing
    """
    def rotateString(self, str, offset):
        # write your code here
        if not str:
            return str
        if offset > len(str):
            offset = offset % len(str)
        n = len(str) - offset
        
        str[:n] = str[:n][::-1]
        str[n:] = str[n:][::-1]
        str[:] = str[::-1]
```



