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
       
***string类也可自身作为一个栈，有相关操作，如，push.back();//键入末尾一个单字符  pop_back();//删掉最后一个字符，empty();back();......***
       
       经典问题： ① 括号匹配：leetcode：（https://leetcode.cn/problems/valid-parentheses/）
                  ② 删除字符串相邻重复字符：leetcode：（https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/）
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
