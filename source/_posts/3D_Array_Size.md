title: 3D Array Size
date: 2016-01-17 14:20:43
categories: 
- Interview
tags:
- Technical Interview
comments: true
---
Given a number, return true if this number is the total number of elements in a 3D array or false if it's not. For each dimension, the number of elements should be at least 2, i.e., the smallest number that is the size of a 3D array is 8.

```python
def is_3d_array_size(a_size):
	if (a_size < 8):
		return False
	factor = 2
	dim = 3
	while (dim > 0):
		if (a_size % factor == 0):
			a_size /= factor
			dim -= 1
			if (a_size == 1 and dim > 0):
				return False
		else:
			factor += 1
			if (factor > a_size):
				return False
	return True

def main():
	i = 1
	# a test case, it's known that 12 should return true since 12 = 2 * 2 * 3 
	print is_3d_array_size(12)

if __name__ == "__main__":
	main()
```