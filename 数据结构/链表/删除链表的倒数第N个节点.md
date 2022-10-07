## 删除链表的倒数第N个节点

 给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。 

```ini
输入：head = [1,2,3,4,5], n = 2 输出：[1,2,3,5] 示例 2：

输入：head = [1], n = 1 输出：[] 示例 3：

输入：head = [1,2], n = 1 输出：[1]
```

```c++
#include<iostream>
using namespace std;
struct Node{
	int data;
	Node* next;
	Node(int data):data(data),next(nullptr){};
}; // 构造结构体
class Solution{
	public:
		Node* removeNthFromEnd(Node* head, int n) {
			Node* dummyNode = new Node(0); // 设置虚拟头节点
			dummyNode->next = head;
			Node* fast = dummyNode;
			Node* slow = dummyNode;
			while(n-- && fast){
				fast = fast->next;
			}// fast首先走n + 1步 ，为什么是n+1呢，因为只有这样同时移动的时候slow才能指向删除节点的上一个节点（方便做删除操作）
			fast = fast->next;
			while(fast){
				fast = fast->next;
				slow = slow->next;
			} // fast和slow同时移动，直到fast指向末尾
			Node *p;
			p = slow->next;
			slow->next = p->next;
			delete p;
			return dummyNode->next;
		}
};
int main() {
	int n;
	cin>>n;
	Node*p=NULL,*q=NULL,*head=NULL;
	for (int i = 1; i <= n; i++) {
		int data;
		cin>>data;
		p = new Node(data);
		p->next = NULL;
		if (!head) head = p, q = p;
		q->next = p;
		q = p;
	} // 构造链表
	Solution Q;
	int k;
	cin>>k;
	head = Q.removeNthFromEnd(head,k);
	Node* t = head;
	while(t){
		p = t;
		cout<<t->data<<" ";
		t = t->next;
		delete p;
	}
	cout << endl;
	
}
```

