## set 0f STL
* disadvantage : 空间大， 速度慢
* advantage : 去重（每种元素在集合中，只能出现一次） ，自动排序

#### set(有序)；（底层实现：平衡二叉树）
#### multiset(有序可重)；（底层实现：平衡二叉树）
#### unordered_set(无序)；（底层实现：哈希表）

```c++
    set<int> ss;
    ss.begin()//是一个指针，返回值的话，要*ss.begin();
    ss.erase()//擦除第一个元素。
    ss.rbegin()//返回最后一个元素（可以认为：reversebegin？？）
```
* (无序部分：)
* leetcode ：  https://leetcode.cn/problems/intersection-of-two-arrays/submissions/
* answer :

**考虑其中的find和insert 的用法**

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int>result_set;//set自带去重效果，只能存放每种元素一个
        unordered_set<int>nums_set(nums1.begin(), nums1.end());//去重存入
        for(int num : nums2) {
            //!=end 代表存在元素在nums1
            if(nums_set.find(num) != nums_set.end()) {
                result_set.insert(num);//insert随机插入，最后unordered_set不会自动排序， 
            }
        }
        return vector<int>(result_set.begin(), result_set.end());//返回vector类型
    }
};
```
---

```c++
* leetcode :https://leetcode.cn/problems/happy-number/submissions/
* answer:
class Solution {
public:
//get sum for the num which in
    int getsum(int n) {
        int sum = 0;
        while(n) {
            sum += (n % 10) * (n % 10);//every number power 2
            n /= 10;
        }return sum;
    }
    bool isHappy(int n) {
        unordered_set<int> book;//标记用无序，其中find迅速查找是否循环
        while(true) {
            int sum = getsum(n);
            if(sum == 1) {
                return true;
            }
            //if circle,循环
            if(book.find(sum) != book.end()) {
                return false;
            }else {
                book.insert(sum);
            }
            n = sum;
        }
    }
};
```
---
* set的erase函数和clear函数使用：
```c++
    #include <iostream>
#include <set>
#include <string>
using namespace std;
int main()
{   /*//删除 set 容器中值为 val 的元素
    size_type erase (const value_type& val);
    
    //删除 position 迭代器指向的元素
    iterator  erase (const_iterator position);
    
    //删除 [first,last) 区间内的所有元素
    iterator  erase (const_iterator first, const_iterator last);
    
    */
    
    //创建并初始化 set 容器
    std::set<int>myset{1,2,3,4,5};
    cout << "myset size = " << myset.size() << endl;
   
    //1) 调用第一种格式的 erase() 方法
    int num = myset.erase(2); //删除元素 2，myset={1,3,4,5}
    cout << "1、myset size = " << myset.size() << endl;
    cout << "num = " << num << endl;
    
    //2) 调用第二种格式的 erase() 方法
    set<int>::iterator iter = myset.erase(myset.begin()); //删除元素 1，myset={3,4,5}
    cout << "2、myset size = " << myset.size() << endl;
    cout << "iter->" << *iter << endl;
    
    //3) 调用第三种格式的 erase() 方法
    set<int>::iterator iter2 = myset.erase(myset.begin(), --myset.end());//删除元素 3,4，myset={5},注意"--myset.end()"，有--,且为前闭后开擦除
    cout << "3、myset size = " << myset.size() << endl;
    cout << "iter2->" << *iter2 << endl;
    return 0;
}
```
* clear()函数是擦除set里面的所有元素
