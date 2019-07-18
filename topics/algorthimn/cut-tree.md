# 剪枝叶

## 题目描述

有一条马路，马路上有很多树，树的高度不一。现在要统一剪树，剪到高度为 h。
意思就是，比 h 高的树都剪到 h，比 h 低的树高度不变。所有的树剪掉的总长度为 C。
现在要使 C>某个值的情况下(假设为 MM)，使 h 最大。问怎么确定 h。

## 代码

```js
function cutTree(list, MM, range) {
  if (list.length === 0) return 0;
  let start = 0;
  let end = Math.max(...list);

  while (start <= end) {
    const mid = start + ((end - start) >> 1);
    let res = 0;
    for (let i = 0; i < list.length; i++) {
      if (list[i] > mid) {
        res = res + list[i] - mid;
      }
    }
    if (res > MM) {
      if (res - MM <= range) return mid;
      end = mid - range;
    } else {
      start = mid + range;
    }
  }

  return -1;
}

// test
const a = cutTree([10, 8, 9, 7, 7, 6], 16, 1);
const b = cutTree([10, 8, 9, 7, 7, 6], 20, 1);
const c = cutTree([10, 8, 9, 7, 7, 6], 15, 1);

console.log(a, b, c);
```
