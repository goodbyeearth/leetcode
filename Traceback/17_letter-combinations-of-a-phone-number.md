# [17. 电话号码的字母组合] (https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

# 方法1
先得到前面的 k-1 个数字的字母的组合 C

```
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        phone = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z']}
        
        def add_digit(combinations, digit):
            new_combinations = []
            for comb in combinations:
                for letter in phone[digit]:
                    new_combinations.append(comb+letter)
            return new_combinations
        
        if len(digits)==0:
            return []
        cur_combinations = phone[digits[0]]
        for i in range(1, len(digits)):
            cur_combinations = add_digit(cur_combinations, digits[i])
        return cur_combinations
```