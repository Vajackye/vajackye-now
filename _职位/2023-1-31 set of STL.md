## set 0f STL
* disadvantage : 空间大， 速度慢
* advantage : 去重（每种元素在集合中，只能出现一次） ，自动排序

#### set(有序)；（底层实现：平衡二叉树）
#### multiset(有序可重)；（底层实现：平衡二叉树）
#### unordered_set(无序)；（底层实现：哈希表）

*(无序部分：)
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
