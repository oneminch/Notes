---
title: Longest Common Prefix
problemUrl: https://leetcode.com/problems/longest-common-prefix/
tags:
  - python
  - strings
---

**My Solution**:

```py
def longestCommonPrefix(strs: List[str]) -> str:
		prefixes = []
		shorterStr = 0
		commonCount = 0
		shouldContinue = True
		i = 0

		if len(strs) < 2:
				return strs[0]

		while shouldContinue:
				if len(strs[i]) == 0 or len(strs[i+1]) == 0:
						return "";

				shorterStr = len(strs[i+1]) if len(strs[i]) > len(strs[i+1]) else len(strs[i])

				for j in range(0, shorterStr):
						if strs[i][j] == strs[i+1][j]:
								commonCount+=1
						else:
								break

				prefixes.append(commonCount)
				commonCount = 0
				i+=1

				if i == len(strs) - 1:
						shouldContinue = False;


		prefixes.sort()
		return strs[0][0:prefixes[0]]
```
