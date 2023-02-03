**map:  map是一种key value的存储结构，可以用key保存数值，用value在保存数值所在的下标。**
* map也有find等东西
* 定义方式： map<数据类型1(key)，数据类型2(value)> 对象name;
* 第二种写法：auto i = map[key];//此时传给i的是value，所以，map可以通过key找value，此时key相当于下标了属于是。  <u>未初始化的map[key]++;默认value从0开始？好像还可以自定义，</u>，**在devc++运行了，可行。是0.**

* map可以用来查找，且存储两种类型，有时和结构体差不多作用.
* ！！！类似于几数相加，几数之和问题，若是在一个数组内操作，数字大了一般不建议哈希，用双指针，不然会time limited。
### std::unordered_map();（底层实现：哈希表）
* 具体用法：leetcode(两数之和)：https://leetcode.cn/problems/two-sum/submissions/
*           leetcode(四数相加)：https://leetcode.cn/problems/4sum-ii/
* answer code： 

```c++
  class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map<int, int> myMap;
        for(int i = 0; i < nums.size(); i++) {
            //遍历当前元素，在map中匹配是否有相应的key
            auto iter = myMap.find(target - nums[i]);//auto， 省下很多功夫，因为数据类型很长，auto自动转换,iter也是map型
            if(iter != myMap.end()) {
                return {iter->second, i};//返回存储i的vector对象，其中iter->second代表该数下标，i是当前数下标。题目说只有一对有效答案，所以，返回的vector里面只有两个元素，是ok滴
            }
            myMap.insert(pair<int, int>(nums[i], i));//**插入key and value.**
        }
        return {};//C++ 11 新特性，返回类型和函数类型一致，这里代表返回一个空的vector<int> 对象
    }
};
```
其中auto的用法，和iter->second的用法，pair用法，和return 用法：
* 针对数据类型很复杂的，自动转换。
* iter由初始化时知道，iter此时指向map中某个元素的全部值，也就是此元素位置的key和value值，iter->second指向，value值，iter->first指向，key值。iter++,则指向map下一个元素全部值。
* return{}，返回函数的类型空对象，return{iter->second, i}; 返回i；返回指针类型时： return nullptr;
* pair：pair是将2个数据组合成一组数据;pair类型定义在#include <utility>头文件中.具体用法：
---
    pair<T1, T2> p1;            //创建一个空的pair对象（使用默认构造），它的两个元素分别是T1和T2类型，采用值初始化。
    pair<T1, T2> p1(v1, v2);    //创建一个pair对象，它的两个元素分别是T1和T2类型，其中first成员初始化为v1，second成员初始化为v2。
    make_pair(v1, v2);          // 以v1和v2的值创建一个新的pair对象，其元素类型分别是v1和v2的类型。
    p1 < p2;                    // 两个pair对象间的小于运算，其定义遵循字典次序：如 p1.first < p2.first 或者 !(p2.first < p1.first) && (p1.second < p2.second) 则返回true。
    p1 == p2；                  // 如果两个对象的first和second依次相等，则这两个对象相等；该运算使用元素的==操作符。
    p1.first;                   // 返回对象p1中名为first的公有数据成员
    p1.second;                 // 返回对象p1中名为second的公有数据成员


* pair创建和初始化等pair<date type1, ...2> name;
* 详细链接：https://blog.csdn.net/sevenjoin/article/details/81937695
---
```c++
  //四数相加
  class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
            unordered_map<int, int> book;//key = nums1 + nums2,value = (nums1 + nums2)times
            for(int a : nums1) {
                for(int b : nums2) {
                    book[a + b]++;//未初始化的map[key]++;默认value从0开始?
                }
            }
            int cnt = 0;//有0-n3-n4出现，直接加出现次数，因为没说不可以重复，相当于，m*n型。
            for(int c : nums3) {
                for(int d : nums4) {
                    if(book.find(0 - c - d) != book.end()) {
                        cnt += book[0 - c - d];
                    }
                }
            }
            return cnt;
    }
};
```
### map();(底层实现：平衡二叉树)
### multimap();(底层实现：平衡二叉树)
