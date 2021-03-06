# 排序问题 — 冒泡排序

## 冒泡排序简介

> the bubble sort seems to have nothing to recommend it, except a catchy name and the fact that it leads to some interesting theoretical problems. - Donald Knuth

### 算法

冒泡排序是一个*迭代*的过程。每次比较两个相邻元素，若二者逆序，则将其置换，以成为顺序。每轮迭代重复前述过程，可以将目前最小的元素放置适合的位置。

### 示例

初始时：

- 序列 `A`: [5, 1, 4, 2, 8],

1. 第一轮迭代：
    - 比较 5, 1, 由于 5 > 1, 所以交换二者，序列 `A` 为 [1,5,4,2,8].
    - 比较 5, 4, 由于 5 > 4, 所以交换二者，序列 `A` 为 [1,4,5,2,8].
    - 比较 5, 2, 由于 5 > 2, 所以交换二者，序列 `A` 为 [1,4,2,5,8].
    - 比较 5, 8, 由于 5 < 8, 所以不变，序列 `A` 为 [1,4,2,5,8].
2. 第二轮迭代：
    - 比较 1, 4, 由于 1 < 4, 所以不变，序列 `A` 为 [1,4,2,5,8].
    - 比较 4, 2, 由于 4 > 2, 所以交换二者，序列 `A` 为 [1,2,4,5,8].
    - 比较 4, 5, 由于 4 < 5, 所以不变，序列 `A` 为 [1,2,4,5,8].  
3. 第三轮迭代，虽然此时数组已经有序，但由于冒泡排序的特性，此时依旧会进行比较。
    - 比较 1, 2, 由于 1 < 2, 所以不变，序列 `A` 为 [1,2,4,5,8].
    - 比较 2, 4, 由于 2 < 4, 所以不变，序列 `A` 为 [1,2,4,5,8].
4. 第四轮迭代：
    - 比较 1, 2, 由于 1 < 2, 所以不变，序列 `A` 为 [1,2,4,5,8].

### 实现

```Rust
pub fn bubble_sort(arr: Vec<i32>) -> Vec<i32> {
  let mut arr = arr;
  for i in (0..arr.len()).rev() {
      for j in 1..(i + 1) {
          if arr[j-1] > arr[j] {
              arr.swap(j-1, j);
          }
      }
  }
  return arr;
}
```

### 性能

- 运行时间: $O(n^2)$.
- 空间复杂度: $O(1)$.

### 特性

冒泡排序满足:

- 稳定性。对于相同的元素，排序后相对次序保持不变。

### 练习

- [排序数组](https://leetcode-cn.com/problems/sort-an-array/)

## 参考

- [bubble sort](https://en.wikipedia.org/wiki/Bubble_sort)
