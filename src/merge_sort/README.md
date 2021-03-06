# 排序问题 — 归并排序

## 归并排序简介

### 算法

归并排序是一个*分治*的过程：

1. 将一个具有 $n$ 个元素的未排序序列 $A$ 划分为两个具有 $n/2$ 个元素的子序列。
2. 对于每一个子序列，重复步骤 1, 直到子序列只包含一个元素。
3. 将步骤 2 中划分的子序列两两合并成一个有序的序列。

### 示例

初始时：

- 序列 `A`: [3,4,2,1,7,5,8,9,0,6],

分：

```text
                [3,4,2,1,7,5,8,9,0,6]
                  /             \
          [3,4,2,1,7]          [5,8,9,0,6]
            /      \             /      \
        [3,4,2]    [1,7]     [5,8,9]    [0,6]
         /   \     / \       /    \     / \
     [3,4]   [2] [1]  [7]  [5,8]   [9] [0] [6]
      / \     |   |   |    / \      |   |   |
    [3] [4]  [2] [1] [7] [5] [8]   [9] [0] [6]
      \ /      \ /      \ /     \ /      \ /
    [3,4]     [1,2]   [5,7]    [8,9]    [0,6]
       \       /         \     /         |
      [1,2,3,4]         [5,7,8,9]       [0,6]
          \              /               |
          [1,2,3,4,5,7,8,9]             [0,6]
                  \                   /
                [0,1,2,3,4,5,6,7,8,9]
```

### 实现

```Rust
pub fn merge_sort(arr: Vec<i32>) -> Vec<i32> {
    fn merge_sort_recursive(arr: &mut Vec<i32>, left: usize, right: usize) {
        if left + 1 < right {
            let mid = left + (right - left) / 2;
            merge_sort_recursive(arr, left, mid);
            merge_sort_recursive(arr, mid, right);
            merge(arr, left, mid, right);
        }
    }

    fn merge(arr: &mut Vec<i32>, left: usize, mid: usize, right: usize) {
        let mut t: Vec<i32> = Vec::new();
        let mut i = left;
        let mut j = mid;
        while i < mid && j < right {
            if arr[i] < arr[j] {
                t.push(arr[i]);
                i = i + 1;
            } else {
                t.push(arr[j]);
                j = j + 1;
            }
        }
        while i < mid {
            t.push(arr[i]);
            i = i + 1;
        }
        while j < right {
            t.push(arr[j]);
            j = j + 1;
        }
        for k in 0..t.len() {
            arr[k + left] = t[k];
        }
    }

    let mut arr: Vec<i32> = arr.clone();
    let left = 0;
    let right = arr.len();
    merge_sort_recursive(&mut arr, left, right);
    return arr;
}
```

### 性能

- 运行时间: $O(nlogn)$.
- 空间复杂度: $O(n)$.

### 特性

归并排序满足:

- 对于**较小**的数组，其表现更加优秀。
- 稳定性。对于相同的元素，排序后相对次序保持不变。

### 扩展

[WIP]

- 按照从大到小的顺序排序；
- 迭代版递归排序；
- 自顶向下和自下而上的递归排序的比较；
- 递归排序的优化；
- 并行递归排序；
- 大规模排序；
- 带有哨兵的写法；

### 练习

- [排序数组](https://leetcode-cn.com/problems/sort-an-array/)

## 参考

- [merge sort](https://en.wikipedia.org/wiki/Merge_sort)
