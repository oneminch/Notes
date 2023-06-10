---
title: Excel Sheet Column Number
problemUrl: https://leetcode.com/problems/excel-sheet-column-number/
tags:
  - python
  - math
  - strings
---

**My Solution**:

```py
import string

def titleToNumber(columnTitle: str) -> int:
    str_list = string.ascii_uppercase[:26]
    
    column_num = 0
    letters = list(reversed(columnTitle))
    for index, letter in enumerate(letters):
        column_num += (str_list.index(letter)+1)*(26**index)

    return column_num
```
