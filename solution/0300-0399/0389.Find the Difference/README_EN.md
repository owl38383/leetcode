# [389. Find the Difference](https://leetcode.com/problems/find-the-difference)

[中文文档](/solution/0300-0399/0389.Find%20the%20Difference/README.md)

## Description

<p>You are given two strings <code>s</code> and <code>t</code>.</p>

<p>String <code>t</code> is generated by random shuffling string <code>s</code> and then add one more letter at a random position.</p>

<p>Return the letter that was added to <code>t</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abcd&quot;, t = &quot;abcde&quot;
<strong>Output:</strong> &quot;e&quot;
<strong>Explanation:</strong> &#39;e&#39; is the letter that was added.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;&quot;, t = &quot;y&quot;
<strong>Output:</strong> &quot;y&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 1000</code></li>
	<li><code>t.length == s.length + 1</code></li>
	<li><code>s</code> and <code>t</code> consist of lowercase English letters.</li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        counter = Counter(s)
        for c in t:
            if counter[c] <= 0:
                return c
            counter[c] -= 1
        return None
```

### **Java**

```java
class Solution {
    public char findTheDifference(String s, String t) {
        int[] counter = new int[26];
        for (int i = 0; i < s.length(); ++i) {
            int index = s.charAt(i) - 'a';
            ++counter[index];
        }
        for (int i = 0; i < t.length(); ++i) {
            int index = t.charAt(i) - 'a';
            if (counter[index] <= 0) {
                return t.charAt(i);
            }
            --counter[index];
        }
        return ' ';
    }
}
```

### **TypeScript**

```ts
function findTheDifference(s: string, t: string): string {
    const n = s.length;
    const count = new Array(26).fill(0);
    for (let i = 0; i < n; i++) {
        count[s.charCodeAt(i) - 'a'.charCodeAt(0)]++;
        count[t.charCodeAt(i) - 'a'.charCodeAt(0)]--;
    }
    count[t.charCodeAt(n) - 'a'.charCodeAt(0)]--;
    return String.fromCharCode(
        'a'.charCodeAt(0) + count.findIndex(v => v !== 0),
    );
}
```

```ts
function findTheDifference(s: string, t: string): string {
    return String.fromCharCode(
        [...t].reduce((r, v) => r + v.charCodeAt(0), 0) -
            [...s].reduce((r, v) => r + v.charCodeAt(0), 0),
    );
}
```

### **Rust**

```rust
impl Solution {
    pub fn find_the_difference(s: String, t: String) -> char {
        let s = s.as_bytes();
        let t = t.as_bytes();
        let n = s.len();
        let mut count = [0; 26];
        for i in 0..n {
            count[(s[i] - b'a') as usize] += 1;
            count[(t[i] - b'a') as usize] -= 1;
        }
        count[(t[n] - b'a') as usize] -= 1;
        char::from(b'a' + count.iter().position(|&v| v != 0).unwrap() as u8)
    }
}
```

```rust
impl Solution {
    pub fn find_the_difference(s: String, t: String) -> char {
        let mut ans = 0;
        for c in s.as_bytes() {
            ans ^= c;
        }
        for c in t.as_bytes() {
            ans ^= c;
        }
        char::from(ans)
    }
}
```

### **C**

```c
char findTheDifference(char *s, char *t) {
    int n = strlen(s);
    int count[26] = {0};
    for (int i = 0; i < n; i++) {
        count[s[i] - 'a']++;
        count[t[i] - 'a']--;
    }
    count[t[n] - 'a']--;
    int i;
    for (i = 0; i < 26; i++) {
        if (count[i]) {
            break;
        }
    }
    return 'a' + i;
}
```

```c
char findTheDifference(char *s, char *t) {
    int n = strlen(s);
    char ans = 0;
    for (int i = 0; i < n; i++) {
        ans ^= s[i];
        ans ^= t[i];
    }
    ans ^= t[n];
    return ans;
}
```

### **...**

```

```

<!-- tabs:end -->
