## 实现strStr()

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回 -1。

```ini
示例 1: 输入: haystack = "hello", needle = "ll" 输出: 2

示例 2: 输入: haystack = "aaaaa", needle = "bba" 输出: -1
```

说明: 当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。 对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

```c++
#include<iostream>
#include<string>
using namespace std;
class Solution {
	public:
		void getNext(int* next, string& s) {
			int j = -1;
			next[0] = j;
			for (int i = 1; i < s.size(); i++) { // 注意 i 从 1 开始
				while (j >= 0 && s[i] != s[j]) {// 前后缀不相同
					j = next[j];// 向前回退
				}
				if (s[i] == s[j]) j++;// 前后缀相同
				next[i] = j;// 将 j (前缀的长度) 赋值给next[i]
			}
		}
    // haystack:文本串  needle:模式串
		int strStr (string& haystack, string& needle) {
			if (needle.size() == 0) return 0;
			int next[needle.size()];
			getNext(next,needle);
			int j = -1;
			for (int i = 0; i < haystack.size(); i++) {
				while (j >= 0 && haystack[i] != needle[j]) j = needle[j];
				if (haystack[i] == needle[j]) j++;
				if (j == needle.size() - 1) return i - needle.size() + 1;
			}	
			return -1;	
			}
};
```

