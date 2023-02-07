### 一维:
```c++
	vector<int> que;
	que.insert(position, value)；
```
---

### 二维：
遍历方式：
```c++
//要先定义一个一维vector，来不定长赋值给二维vector：等价：res.push_back(vector<int>()); res[depth].push_back(xxx);//先开辟一维列[]，方可使用下标插入第几维
vector<vector<int>> res;
	 for (int i = 0; i < N; ++i) {
	    vector<int> temp;
	     for (int j = 0; j < M; ++j) {
	         tmp.push_back(xxx);
	     }
	     res.push_back(tmp);
	 }
```
---
### 链表：
```c++
	//插入效率比vector高，因为vector插入时，效率大于等于n^2，先开辟新扩容数组，在插入copy到新数组。
	list<int> que;
	que.insert(position, value);
```
