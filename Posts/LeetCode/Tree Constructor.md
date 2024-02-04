---
title: Tree Constructor
problemUrl: https://www.coderbyte.com/information/Tree%20Constructor
tags:
  - javascript
  - binary tree
---

## My Solution

### JavaScript

```javascript
function Node(v) {
  this.value = v;
  this.childCount = 0;
}

function TreeConstructor(strArr) {
  const nodeList = [];

  // convert string pairs to array pairs
  const numArr = strArr.map((item) => {
    let strPairs = item.substring(1, item.length - 1).split(",");
    return strPairs.map((item) => {
      return parseInt(item);
    });
  });

  for (pair of numArr) {
    let firstNode = nodeList.find((node) => node.value === pair[0]);
    let secondNode = nodeList.find((node) => node.value === pair[1]);

    let node1 = null,
      node2 = null;

    // create a node if it doesn't exist
    if (!firstNode) {
      node1 = new Node(pair[0]);
      nodeList.push(node1);
    }

    // create a node if it doesn't exist
    // else update childcount of existing value
    if (!secondNode) {
      node2 = new Node(pair[1]);
      node2.childCount++;
      nodeList.push(node2);
    } else {
      if (secondNode.childCount < 2) {
        secondNode.childCount++;
      } else {
        return false;
      }
    }
  }

  return true;
}
```
