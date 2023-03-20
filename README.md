# Binary_search_rust
## The binary search algorithm has a time complexity of O(log n), which is optimal for searching sorted data.
```rust
use std::cmp::Ordering;

/// Performs a binary search on a slice and returns the index of the element if it is found.
pub fn binary_search<T: Ord>(search_item: &T, sorted_slice: &[T]) -> Option<usize> {
    let mut left_idx = 0;
    let mut right_idx = sorted_slice.len();

    // Continue until the left and right indices overlap
    while left_idx < right_idx {
        // Calculate the midpoint
        let mid_idx = left_idx + (right_idx - left_idx) / 2;

        match search_item.cmp(&sorted_slice[mid_idx]) {
            Ordering::Less => right_idx = mid_idx,
            Ordering::Equal => return Some(mid_idx),
            Ordering::Greater => left_idx = mid_idx + 1,
        }
    }

    // The item was not found
    None
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn empty_slice() {
        // Test an empty slice
        let index = binary_search(&"a", &vec![]);
        assert_eq!(index, None);
    }

    #[test]
    fn one_item_slice() {
        // Test a slice with only one item
        let index = binary_search(&"a", &vec!["a"]);
        assert_eq!(index, Some(0));
    }

    #[test]
    fn search_strings() {
        // Test a slice of strings
        let index = binary_search(&"a", &vec!["a", "b", "c", "d", "google", "zoo"]);
        assert_eq!(index, Some(0));
    }

    #[test]
    fn search_ints() {
        // Test a slice of integers
        let index = binary_search(&4, &vec![1, 2, 3, 4]);
        assert_eq!(index, Some(3));

        let index = binary_search(&3, &vec![1, 2, 3, 4]);
        assert_eq!(index, Some(2));

        let index = binary_search(&2, &vec![1, 2, 3, 4]);
        assert_eq!(index, Some(1));

        let index = binary_search(&1, &vec![1, 2, 3, 4]);
        assert_eq!(index, Some(0));
    }

    #[test]
    fn item_not_found() {
        // Test when the item is not found
        let index = binary_search(&5, &vec![1, 2, 3, 4]);
        assert_eq!(index, None);
    }
}
```
