# Sliding Window Problems

## How to Identify a Sliding Window Problem

If you're given an **Array** or a **String** and asked to find a **Subarray** or **Substring**, especially if it's related to finding the largest size, largest sum, or the size of a window, it usually points to a **Sliding Window** problem.

### Types of Sliding Window Problems

There are two main types of sliding window problems:

### 1. Fixed-Size Window Problems

In these problems, the window size is fixed, and the goal is to perform operations (e.g., sum, count) on each subarray or substring of the given size.

Example: 
- Given a sum and a fixed window size, you are asked to find the maximum sum of any subarray of that size.

### 2. Variable-Size Window Problems

In these problems, the window size can vary. You're often asked to find the largest subarray or substring that satisfies a given condition, such as a sum greater than or equal to a specific value.

Example: 
- Given a sum, you might be asked to find the largest window size whose sum satisfies the condition.

---

### Fixed-Size Sliding Window Problem Examples

#### [1. Max Sum Subarray of size K](https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)
```cpp
long maximumSumSubarray(int k, vector<int> &arr, int n) {
    long maxSum = INT_MIN;
    long sum = 0;
    int i = 0, j = 0;
    
    while (j < n) {
        sum += arr[j];
        
        // Check if window size is smaller than k
        if (j - i + 1 < k) {
            j++;
        } 
        // When window size reaches k
        else if (j - i + 1 == k) {
            maxSum = max(maxSum, sum);
            sum -= arr[i];  // Slide the window forward
            i++;
            j++;
        }
    }
    return maxSum;
}
```
#### 2. First negative in every window of size k

```cpp
vector<long long> printFirstNegativeInteger(long long int A[],
                                            long long int N, long long int K) {
    queue<long long int> q;  // Create a queue to store negative numbers
    vector<long long> ans;   // To store the result
    int i = 0, j = 0;        // i for window start, j for window end

    while (j < N) {
        // Check if the current element is negative
        if (A[j] < 0) {
            q.push(A[j]);
        }

        // If window size is less than K, expand the window
        if (j - i + 1 < K) {
            j++;
        }
        // When window size equals K
        else if (j - i + 1 == K) {
            // If there's no negative number in the current window
            if (q.empty()) {
                ans.push_back(0);
            } 
            // If there is a negative number, add it to the answer
            else {
                ans.push_back(q.front());
                // If the front of the queue is leaving the window, remove it
                if (A[i] == q.front()) {
                    q.pop();
                }
            }
            // Slide the window
            i++;
            j++;
        }
    }

    return ans;
}

```

#### 3. Count Occurences of Anagrams

```cpp
int search(string pat, string txt) {
    int n = txt.size();
    int k = pat.size();
    
    int ans = 0;
    
    // Store the frequency of the characters in the pattern
    vector<int> storeFreqOfPat(26, 0);
    for (int i = 0; i < k; i++) {  // Iterate over the pattern size
        storeFreqOfPat[pat[i] - 'a']++;
    }
    
    vector<int> storeFreqOfTxt(26, 0);
    int i = 0, j = 0;
    
    // Sliding window over the text
    while (j < n) {
        storeFreqOfTxt[txt[j] - 'a']++;  // Add the current character frequency
        
        // When window size equals k
        if (j - i + 1 == k) {
            // Compare the frequency of the current window with the pattern
            if (storeFreqOfPat == storeFreqOfTxt) {
                ans++;
            }
            // Shrink the window from the left
            storeFreqOfTxt[txt[i] - 'a']--;  // Remove the frequency of the leftmost character
            i++;  // Move the window
        }
        j++;  // Expand the window
    }
    
    return ans;
}
```
