

c++链表<list>函数总结

```c++
#include<iostream>
#include<list>
using namespace std;
int main() {
	int arr[10] = {1,2,3,4,5,6,7,8,9,10};
	list<int> intlist(arr,arr+10);
	

	//assign用法 
​	for (auto it = intlist.begin();it != intlist.end();it++) {
​		cout<<*it<<" ";
​	}
​	cout<<endl; 
​	for (auto it = intlist.rbegin();it != intlist.rend();it++) {
​	    cout<<*it<<" ";//反向输出--rbegin(),rend()反向迭代器 
​	}  
​	cout<<endl;
​	int brr[5]={5,2,3,1,4};
​	intlist.assign(brr,brr+5);//assign:替换原链表的数据 
​	for (auto it = intlist.begin();it != intlist.end(); it++) {
​		cout<<*it<<" ";
​	}
​	cout<<endl;
​	intlist.assign(5,1);//assing(num,val)将原链表的数据替换成 num个val 
​	for (auto it = intlist.begin(); it != intlist.end(); it++) {
​		cout<<*it<<" ";
​	}
​	
​	//front back 用法 
​	cout<<endl;
​	cout<<intlist.front()<<" "<<intlist.back();//front和back访问链表首结点和尾节点，并可以修改 
​	//clear()清空链表，empty()判断链表是否为空 
​	//erase 删除链表中的元素 ，只能通过迭代器遍历删除 

}


```

