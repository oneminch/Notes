---
title: Defanging an IP Address
problemUrl: https://leetcode.com/problems/defanging-an-ip-address/
tags:
  - javascript
  - strings
---

**My Solution**:

```javascript
/**
 * @param {string} address
 * @return {string}
 */
var defangIPaddr = function(address) {
    return address.split('.').join('[.]');   
};
```
