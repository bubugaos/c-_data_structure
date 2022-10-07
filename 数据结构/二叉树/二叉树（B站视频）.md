## 二叉树（B站视频）

```
二叉搜索数，左边的数永远小于右边的数；
（查找最大最小数）
```

```c
#include<stdio.h>
#include<stdlib.h>
struct Bstnode{
	int data;
	struct Bstnode *left;
	struct Bstnode *right;
};
struct Bstnode *Getnewnode(int data) {
	struct Bstnode *newnode;
	newnode = (struct Bstnode*)malloc(sizeof(struct Bstnode));
	newnode->data = data;
	newnode->left = NULL;
	newnode->right = NULL;
	return newnode;
}
struct Bstnode *Insert(struct Bstnode *root, int data) {
	if (root == NULL) root = Getnewnode(data);
	else if (data <= root->data) root->left = Insert(root->left, data);
	else  root->right = Insert(root->right, data);
	return root;
}
int Search(struct Bstnode *root, int data) {
	if (root == NULL) return false;
	if (data == root->data) return true;
	else if (data < root->data) return Search(root->left, data);
	else return Search(root->right, data);
}
int findmin(struct Bstnode *root) {
	if (root == NULL) return -1;
	if (root->left == NULL) return root->data;
	return findmin(root->left);
}
int findmax(struct Bstnode *root) {
	if (root == NULL) return -1;
	else if (root->right == NULL) return root->data;
	return findmax(root->right);
}
int main() {
	struct Bstnode *root = NULL;
	int i, x, n;
	scanf("%d", &n);
	for (i = 1; i <= n; i++) {
		scanf("%d", &x);
	    root = Insert(root, x);
	}
	scanf("%d", &x);
	if (Search(root, x) == true) printf("Found");
	else printf("Not found"); 
	x = findmin(root);
	int y = findmax(root);
	printf("\n%d %d",x, y);
}
```

```
二叉搜索树中序遍历（从小到大排序）
```

```c
#include<stdio.h>
#include<stdlib.h>
struct Bstnode{
	int data;
	struct Bstnode *left;
	struct Bstnode *right;
};
struct Bstnode *Getnewnode(int data) {
     struct Bstnode *newnode;
	 newnode = (struct Bstnode *)malloc(sizeof(struct Bstnode));
	 newnode->data = data;
	 newnode->left = NULL;
	 newnode->right = NULL;
	 return newnode;	
}
struct Bstnode *Insert(struct Bstnode *root, int data) {
	if (root == NULL) root = Getnewnode(data);
	else if (data <= root->data) root->left = Insert(root->left,data);
	else root->right = Insert(root->right, data);
	return root;
}
void Midorder(struct Bstnode *root) {
	if (root == NULL) return;
	Midorder(root->left);
	printf("%d ",root->data);
	Midorder(root->right);
}
int main() {
	struct Bstnode *root = NULL;
	int n, i, x;
	scanf("%d", &n);
	for (i = 1; i <= n; i++) {
		scanf("%d", &x);
		root = Insert(root,x);
	}
	Midorder(root);
	return 0;
}
```

```
C++层序遍历
```

```c++
#include<iostream>
#include<queue>
using namespace std;
struct node{
	int data;
    node *left;
    node *right;
};
//层序遍历核心代码 
void levelorder(node *root) {
	if (root == NULL) return;
	queue<node*> Q;
	Q.push(root);
	while (!Q.empty()) {
		node *current = Q.front();
		cout<<current->data<<" ";
		if (current->left != NULL) Q.push(current->left);
		if (current->right != NULL) Q.push(current->right);
		Q.pop();
	}
}//利用队列先进先出的性质存储节点
node *Getnewnode(int data) {
	node *newnode;
	newnode = new node;
	newnode->data = data;
	newnode->left = NULL;
	newnode->right = NULL;
	return newnode;
}
node *Insert(node *root, int data) {
	if (root == NULL) root = Getnewnode(data);
	else if (data <= root->data) root->left = Insert(root->left, data);
	else root->right = Insert(root->right, data);
	return root;
}
int main() {
	node *root = NULL;
	int i, n, x;
	cin>>n;
	for (i = 1; i <= n; i++) {
		cin>>x;
		root = Insert(root, x);
	}
	levelorder(root);
}
```

```
给出二叉树后序遍历写出层序遍历
```

```c
#include<stdio.h>
int  n, j = 1;
int a[100],b[100];
void dfs(int i) {
	 if (i > n) return;
		dfs(i * 2);
		dfs(i * 2 + 1);
		b[i] = a[j++];	
}
int main() {
	scanf("%d", &n);
	for (int i = 1; i <= n; i++) {
		scanf("%d", &a[i]);
	}
	dfs(1);
	for (int i = 1; i <= n; i++) {
		if (i != n)
		printf("%d ",b[i]);
		else printf("%d",b[i]);
	}
	return 0;
}
```

