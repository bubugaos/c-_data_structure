## 实现strstr功能

在文本串中查找是否出现过模式串t,如果出现过则返回匹配的第一的位置，如果没有出现返回-1 

```
文本串：aabaabaafa

模式串：aabaaf
```



#### 前缀表统一减一的代码实现

```c++
#include<iostream>
#include<string>
using namespace std;
void Getnext(int *next, const string &s) {
	int j = -1;//j指向前缀的起始位置 
	int i;//i只想后缀地的起始位置 
	next[0] = j;//next数组为前缀表 
	for (i = 1; i < s.size(); i++) {    //注意i从1开始 
		while(j >= 0 && s[j+1] != s[i]) {   //前后缀不同 
			j = next[j];//j寻找之前匹配的位置 
		}
		if (s[j+1] == s[i]) j++;//前后缀相同 ，i,j 同时向后移动 
		next[i] = j;//将j(前缀的长度)赋值为next[i] 
	}
}
int Strstr(string haystack, string needle) {  //haystack为文本串,needle为模式串 
	if (haystack.size() == 0) return 0;
	int next[needle];
	Getnext(next,needle);
	int i, j = -1;//因为next数组中记录的起始位置为-1 
	for (i = 0; i < haystack.size(); i++) {
		while(j >= 0 && haystack[i] != needle[j+1]) {
			j = next[j];//j寻找之前匹配的位置 
		}
		if (haystack[i] == needle[j+1]) j++;
		if (j == needle.size()-1) return i - needle.size() + 1;//文本串出现的模式串 
	}
	return -1;
}
int main() {
	string haystack, needle;
	cin>>haystack>>needle;
	cout<<Strstr(haystack,needle)<<endl;
}
```


