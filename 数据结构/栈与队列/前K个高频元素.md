## 前K个高频元素

给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

示例 1:

- ```ini
  - 输入: nums = [1,1,1,2,2,3], k = 2
  - 输出: [1,2]
  ```

  

示例 2:

- ```ini
  - 输入: nums = [1], k = 1
  - 输出: [1]
  ```

  ## 代码：

  ```c++
  #include<bits/stdc++.h>
  using namespace std;
  // 时间复杂度：O(nlogk)
  // 空间复杂度：O(n)
  class Solution {
  public:
      // 小顶堆
      class mycomparison {
      public:
          bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
              return lhs.second > rhs.second;
          }
      };
      vector<int> topKFrequent(vector<int>& nums, int k) {
          // 要统计元素出现频率
          unordered_map<int, int> map; // map<nums[i],对应出现的次数>
          for (int i = 0; i < nums.size(); i++) {
              map[nums[i]]++;
          }
  
          // 对频率排序
          // 定义一个小顶堆，大小为k
          priority_queue<pair<int, int>, vector<pair<int, int>>, mycomparison> pri_que;
  
          // 用固定大小为k的小顶堆，扫面所有频率的数值
          for (unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++) {
              pri_que.push(*it);
              if (pri_que.size() > k) { // 如果堆的大小大于了K，则队列弹出，保证堆的大小一直为k
                  pri_que.pop();
              }
          }
  
          // 找出前K个高频元素，因为小顶堆先弹出的是最小的，所以倒序来输出到数组
          vector<int> result(k);
          for (int i = k - 1; i >= 0; i--) {
              result[i] = pri_que.top().first;
              pri_que.pop();
          }
          return result;
  
      }
  };
  int main() {
  	int n, k;
  	Solution Q;
  	cin>>n>>k;
  	vector<int> nums(n);
  	for (int i = 0; i < n; i++) {
  		cin>>nums[i];
  	}
  	vector<int> result = Q.topKFrequent(nums,k);
  	for (int i = 0; i < k; i++) {
  		cout<<result[i]<<" ";
  	}
  	cout<<endl;
  }
  ```

  