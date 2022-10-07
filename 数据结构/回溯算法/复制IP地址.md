## 复制IP地址

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效的 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效的 IP 地址。

- ```
  示例 1：
  
  - 输入：s = "25525511135"
  - 输出：["255.255.11.135","255.255.111.35"]
  
  示例 2：
  
  - 输入：s = "0000"
  - 输出：["0.0.0.0"]
  ```

  ```c++
  #include<iostream>
  #include<string>
  using namespace std;
  class Solution {
  	private:
  		bool isValid (const string& s, int start, int end) {
  			if (start > end) return false;
  			if (s[start] == '0' && start != end) return false;
  			int num = 0;
  			for (int i = start; i <= end; i++) {
  				if (!isdigit(s[i])) return false;
  				num = num * 10 + (s[i] - '0');
  				if (num > 255) return false;
  			}
  			return true;
  		}
  	public:// startIndex：搜索的起始位置；pointNum：添加逗点的数量 
  		void backstracking(string& s, int startIndex, int pointNum) {
  			if (pointNum == 3) {// '.'的数量为3时，分隔结束 
  				if (isValid(s,startIndex,s.size()-1)) {// 用来判断第三个小数点后面片段
  				// 是否合法 
  					cout<<s<<endl;
  				}
  			}
  			for (int i = startIndex; i < s.size(); i++) {
  				if (isValid(s,startIndex,i)) {//判断[startIndex,i]这个区间的子字符串是否合法 
  					pointNum++;
  					s.insert(s.begin()+i+1,'.');// 在i的后面插入一个逗点 
  					backstracking(s,i+2,pointNum);//插入逗点后下一个字符串的起始位置为i+2 
  					pointNum--;
  					s.erase(s.begin()+i+1);
  				}
  				else break;// 不合法直接结束本层循环 
  			}
  		}
  };
  int main() {
  	Solution Q;
  	string s;
  	cin>>s;
  	Q.backstracking(s,0,0);
  }
  ```

  