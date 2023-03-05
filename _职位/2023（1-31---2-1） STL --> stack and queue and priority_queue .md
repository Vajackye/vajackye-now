stack (先进后出，不提供迭代器iterator，栈是以底层容器完成其所有的工作，对外提供统一的接口，底层容器是可插拔的（也就是说我们可以控制使用哪种容器来实现栈的功能),
       栈的底层实现可以是vector，deque，list 都是可以的， 主要就是数组和链表的底层实现)
* deque容器，详解：http://c.biancheng.net/view/6860.html
* but ,you also can use the vector to as the container, the way is "std::stack<int, std::vector<int>> ???(variable name)" 
* stack相关操作：
       
       top();//返回一个栈顶元素的引用，但是不删除栈顶元素
       push();//插入栈顶一个元素
       pop();//移除栈顶一个元素
       size();//返回栈中元素个数
       empty();//如果栈中无元素，返回true
       swap(stack<T> & other_stack);//将当前栈中元素与参数元素对调，但是数据类型要一致
       emplace();//用传入的参数调用构造函数，在栈顶生成对象
       交换栈，直接等号。
       清空栈：①pop一直循环。②定义一个临时栈such as：stack<int>().swap(s);//s为你要清空的栈，通过swap与空栈交换位置.
       
***string类也可自身作为一个栈，有相关操作，如，push.back();//键入末尾一个单字符  pop_back();//删掉最后一个字符，empty();back();......***
       
       经典问题： ① 括号匹配：leetcode：（https://leetcode.cn/problems/valid-parentheses/）
                  ②逆波兰表达式：leetcode：（https://leetcode.cn/problems/evaluate-reverse-polish-notation/）,其中有些细节，比如stoll()把字符串转换成long long int 型；string s; s[i]==""(双引号)和''(单引号区别)。细节为：
             * 单引号用来表示字符字面量，单引号括起来的单个字符代表整数。
             * 双引号用来表示字符串字面量，双引号括起来的若干个字符代表字符指针
             **字符串客串详解： http://c.biancheng.net/view/2236.html **
       
                  ③删除字符串相邻重复字符：leetcode：（https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/）(解法如下：)
```c++
       //one kind
       class Solution {
public:
    string removeDuplicates(string s) {
        string res;
        for(char ch : s) {
            if(res.empty() || res.back() != ch) {
                res.push_back(ch);
            }
            else {
                res.pop_back();
            }
        }
        return res;
    }
};
       //second kind
       /*
stack<char> res;
for(char s : S) {
    if(res.empty() || s != res.top()) {
        res.push(s);
    }
    else {
        res.pop();
    }
}
string ret = "";//赋值为空字符，方便字符串加减法
while(!res.empty()) {
    ret += res.top();//&
    res.pop();//cut
}
reverse(ret.begin(), ret.end());//栈出来的字符是反过来的，反转一下
return ret;
*/
```
       
---
* Leetcode：https://leetcode.cn/problems/implement-queue-using-stacks/submissions/
* answer code:
```c++
       class MyQueue {
public:
    stack<int>stin;
    stack<int>stout;
    MyQueue() {
        //用于对自己的数据进行初始化，自己命名，结构体，相当于，把下面的几个函数封包进去，隐藏实现，初始化。MyQueue que = new MyQueue();//such as： A *obj = new A();  //使用 new 创建对象
    }
    //将x推到队列末尾
    void push(int x) {
        stin.push(x);//压栈
    }
    //从队列开头移除并返回元素
    int pop() {
        //当stout为空时，才能stin导入元素，否则会压栈，出不来元素
        if(stout.empty()) {
            //stin put in until the stin elements empty.
            while(!stin.empty()) {
                stout.push(stin.top());//top，栈顶返回引用值
                stin.pop();//，引用完之后，删除栈顶值
            }
        }
        int ret = stout.top();//入栈的栈底等于出栈的栈尾
        stout.pop();
        return ret;
    }
    //返回队列开头的元素
    int peek() {
        int res = this->pop();//用this指针引用自己编的pop函数
        stout.push(res);//把pop弹出的栈顶元素放回去(毕竟每个操作不一样，这里只是返回，不要删除，但是要经过pop函数，所以，删在补)
        return res;
    }
    //队列空，true，or false
    bool empty() {
        return stin.empty() && stout.empty();//非0，true ，0 false
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```
---
 
 
queue（先进先出，不提供迭代器iterator,与栈大同小异）
       
      q.empty();//如果队列为空返回true，否则返回false
      q.size();//返回队列中元素的个数
      q.pop();//删除队列首元素但不返回其值
      q.front();//返回队首元素的值，但不删除该元素
      q.push();//在队尾压入新元素
      q.back();//返回队列尾元素的值，但不删除该元素
      清空队列：①pop一直循环。②定义一个临时队列such as：queue<int>().swap(s);//s为你要清空的队列，通过swap与空队列交换位置


---
* leetcode：https://leetcode.cn/problems/implement-stack-using-queues/submissions/
* answer code：
```c++
       class MyStack {
public:
    //only use one queue can finish all thing, but you also can use two queue, the second queue will be used to copy the queue1 except the final element.
    queue<int> que;
    MyStack() {
        //look the 232 use the stack as the queue.
    }
    //压入栈顶
    void push(int x) {
        que.push(x);
    }
    //移除并返回栈顶元素
    int pop() {
        int size = que.size();
        size--;//最后一个元素不删，当作栈底，其他元素删除，然后反向移入队尾（入栈）
        while(size--) {
            que.push(que.front());//front,引用首元素，back引用尾元素
            que.pop();//front 后 ，删掉元素
        }
        int res = que.front();//the final element
        que.pop();//移除栈顶
        return res;
    }
    //返回栈顶元素
    int top() {
        return que.back();//三个操作互不干扰，与stack模拟queue不同
    }
    //空true
    bool empty() {
        return que.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
``` 
---

### 优先队列(`priority_queue`):
* https://blog.csdn.net/xingzi201/article/details/119884227
* https://blog.csdn.net/c20182030/article/details/70757660?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162977367316780274196594%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=162977367316780274196594&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-8-70757660.first_rank_v2_pc_rank_v29&utm_term=%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97&spm=1018.2226.3001.4187

* 底层实现是堆，大顶堆小顶堆，一开始默认是大顶堆，如果没有自己设置比较方式;
* 自定义数据类型，需要自己编写排序函数cmp；
       
```c++
#include<iostream>
#include<queue>
#include<functional>//用于比较操作符       
using namespace std;

int main()  {
    srand(time(NULL));//随机数生成
    priority_queue<int> pq1;
    priority_queue<int, vector<int>, greater<>() > pq2;//大顶堆，后面两个可省略，默认为大顶堆，实现容器为vector   
    priority_queue<int, vector<int>, less<>() > pq3;//小顶堆，后面两个加上。
    //less是从大到小，greater是从小到大。从根开始算（数组头）
    //默认会排序，基本用法：
    for(int i = 0; i < 10; i++) {
        int i = rand()%100; //随机数
        pq1.push(i);
        cout<<pq1.top();  //与普通队列不同，front(),back() ，优先队列的top为顶部（前为出口）                               
    }
    for(int i = 0; i < pq1.size(); i++) {
       int out = pq1.top();
       cout<<out;
       pq1.pop();
       }
    return 0;
       //pq1.emplace();原地构造一个元素并插入队列
       //pq1.empty();
       //swap();交换队列元素
}       
```
* 附录：关于rand：https://support.microsoft.com/zh-cn/office/rand-%E5%87%BD%E6%95%B0-4cbfa695-8869-4788-8d90-021ea9f5be73       
