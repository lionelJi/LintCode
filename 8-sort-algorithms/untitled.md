# 快速排序 Quick Sort

![](../.gitbook/assets/image%20%282%29.png)



![../\_images/partitionB.png](http://interactivepython.org/courselib/static/pythonds/_images/partitionB.png)

## Solution:

```python
class QuickSort:
    def __init__(self, target):
        self.target = target

    def quick_sort(self):
        self.quick_sort_helper(0, len(self.target) - 1)
        return self.target

    def quick_sort_helper(self, first, last):
        if first < last:
            split_point = self.partition(first, last)

            self.quick_sort_helper(first, split_point - 1)
            self.quick_sort_helper(split_point + 1, last)

    def partition(self, first, last):
        pivot, left, right = self.target[first], first + 1, last

        while left < right:
            # find first element > pivot from left
            while left <= right and self.target[left] < pivot:
                left += 1
            # find first element < pivot from left
            while right >= left and self.target[right] > pivot:
                right -= 1

            if left <= right:
                self.target[left], self.target[right] = self.target[right], self.target[left]

        self.target[first], self.target[right] = self.target[right], self.target[first]

        return right


s = QuickSort([54, 26, 93, 17, 77, 31, 44, 55, 20])
print(s.quick_sort())
```



