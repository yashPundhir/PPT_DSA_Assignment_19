# Assignment 19 - DSA Searching and Sorting

---

Q2. **Count of Smaller Numbers After Self**

Given an integer array `nums`, return *an integer array* `counts` *where* `counts[i]` *is the number of smaller elements to the right of* `nums[i]`.

**Example 1:**

```
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are2 smaller elements (2 and 1).
To the right of 2 there is only1 smaller element (1).
To the right of 6 there is1 smaller element (1).
To the right of 1 there is0 smaller element.

```

**Example 2:**

```
Input: nums = [-1]
Output: [0]

```

**Example 3:**

```
Input: nums = [-1,-1]
Output: [0,0]

```

**Constraints:**

- `1 <= nums.length <= 100000`
- `-10000 <= nums[i] <= 10000`

**Solution 2:**

```javascript
function countSmaller(nums) {
	const n = nums.length;
	const counts = new Array(n).fill(0);

	for (let i = 0; i < n; i++) {
		let count = 0;
		for (let j = i + 1; j < n; j++) {
			if (nums[j] < nums[i]) {
				count++;
			}
		}
		counts[i] = count;
	}

	return counts;
}

const nums1 = [5, 2, 6, 1];
console.log(countSmaller(nums1)); // Output: [2, 1, 1, 0]

const nums2 = [-1];
console.log(countSmaller(nums2)); // Output: [0]

const nums3 = [-1, -1];
console.log(countSmaller(nums3)); // Output: [0, 0]
```

---

Q3. **Sort an Array**

Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in** functions in `O(nlog(n))` time complexity and with the smallest space complexity possible.

**Example 1:**

```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).

```

**Example 2:**

```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
Explanation: Note that the values of nums are not necessairly unique.

```

**Constraints:**

- `1 <= nums.length <= 5 * 10000`
- `-5 * 104 <= nums[i] <= 5 * 10000`

**Solution 3:**

```javascript
function sortArray(nums) {
	function merge(left, right) {
		const merged = [];
		let i = 0,
			j = 0;

		while (i < left.length && j < right.length) {
			if (left[i] <= right[j]) {
				merged.push(left[i]);
				i++;
			} else {
				merged.push(right[j]);
				j++;
			}
		}

		return merged.concat(left.slice(i)).concat(right.slice(j));
	}

	function mergeSort(nums) {
		if (nums.length <= 1) {
			return nums;
		}

		const mid = Math.floor(nums.length / 2);
		const left = mergeSort(nums.slice(0, mid));
		const right = mergeSort(nums.slice(mid));

		return merge(left, right);
	}

	return mergeSort(nums);
}

const nums1 = [5, 2, 3, 1];
console.log(sortArray(nums1)); // Output: [1, 2, 3, 5]

const nums2 = [5, 1, 1, 2, 0, 0];
console.log(sortArray(nums2)); // Output: [0, 0, 1, 1, 2, 5]
```

---

Q4. **Move all zeroes to end of array**

Given an array of random numbers, Push all the zero’s of a given array to the end of the array. For example, if the given arrays is {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0}, it should be changed to {1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0}. The order of all other elements should be same. Expected time complexity is O(n) and extra space is O(1).

**Example:**

**Solution 4:**

```javascript
function moveZeroes(nums) {
	let j = 0;

	for (let i = 0; i < nums.length; i++) {
		if (nums[i] !== 0) {
			[nums[i], nums[j]] = [nums[j], nums[i]];
			j++;
		}
	}

	for (let i = j; i < nums.length; i++) {
		nums[i] = 0;
	}
}

const nums = [1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0];
moveZeroes(nums);
console.log(nums); // Output: [1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0]
```

---

Q8. **Intersection of Two Arrays II**

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must appear as many times as it shows in both arrays and you may return the result in **any order**.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]

```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.

```

**Constraints:**

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

**Solution 8:**

```javascript
function intersect(nums1, nums2) {
	const frequency = new Map();

	// Update frequency in hashmap for nums1
	for (let num of nums1) {
		if (frequency.has(num)) {
			frequency.set(num, frequency.get(num) + 1);
		} else {
			frequency.set(num, 1);
		}
	}

	const intersection = [];

	// Find intersection with nums2
	for (let num of nums2) {
		if (frequency.has(num) && frequency.get(num) > 0) {
			intersection.push(num);
			frequency.set(num, frequency.get(num) - 1);
		}
	}

	return intersection;
}

const nums1 = [1, 2, 2, 1];
const nums2 = [2, 2];
console.log(intersect(nums1, nums2)); // Output: [2, 2]

const nums3 = [4, 9, 5];
const nums4 = [9, 4, 9, 8, 4];
console.log(intersect(nums3, nums4)); // Output: [4, 9]
```

---
