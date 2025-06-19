# Binary Search
Binary Search is an algorithim that has an input of a sorted list and begins by comparing the middle element of the list with the target element. If the target value matches the middle element, its position in the list is returned. If it does not match, the list is divided into two halves. The first half consists of the first element to the middle element whereas the second half consists of the element next to the middle element to the last element i.e. the search interval is repeatedly divided into halves.

Binary search is the most efficient searching algorithm having a run-time complexity of O(log2 N) in a sorted array.

Binary search can be done iteratively or recursively

## Binary Seearch in Ruby
```ruby
def binary_search_iterative(arr, target)
  low = 0
  high = arr.length - 1

  while low <= high
    mid = (low + high) / 2
    if arr[mid] == target
      return mid
    elsif arr[mid] < target
      low = mid + 1
    else
      high = mid - 1
    end
  end

  nil
end

def binary_search_recursive(arr, target, low = 0, high = arr.length - 1)
  return nil if low > high

  mid = (low + high) / 2
  if arr[mid] == target
    return mid
  elsif arr[mid] < target
    binary_search_recursive(arr, target, mid + 1, high)
  else
    binary_search_recursive(arr, target, low, mid - 1)
  end
end
```
