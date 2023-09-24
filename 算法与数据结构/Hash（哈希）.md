## 哈希算法
* 哈希函数应该尽量避免冲突，即函数h(X)尽量**单射**。
* 由于得到的哈希值一般都很大，所以通常对字符串的哈希值进行取余操作。
* 隐性取余：取空间大小为M = 2^64, 64是unsigned long long的长度，一个哈希值H, H>M时会自动溢出，等价于**自动对M取余**
  
### BKDRHash算法
* 是一种**进制哈希**
* 即，制定一个进制P，（通常为31，131，1313，13131，131313.....用这些数字能有效避免碰撞。），对字符串转换为基于P进制的数字，最后对M取余，就得到了相应的哈希值
* 举个例子：S = "abc", P = 131, 则H(S) = 'a' * P^2 + 'b' * P^1 + 'c' * p^0 = 'a' * 131^2 + 'b' * 131^1 + 'c' * 131^0;
* 就是每一位按进制P的权值相加。
* 例题：洛谷P3370
* 代码如:
*  ```c++
   #include<bits/stdc++.h>
   using namespace std;
   typedef unsigned long long ull;

   ull a[10010];
   string s;
   bool cmp(ull a, ull b)
   {
       return a>b;
   }

   ull BKDRHash(string s)
   {
       ull P = 131, H = 0;
       int n = s.size();
       for(int i = 0; i < n; i++)
       {
           H = H * P + s[i]-'a' + 1;//开始计算权值，也可以：H = H*P + s[i];字符转换为数字。
       }
       return H;//一个哈希函数值
   }

   int main()
   {  
       int n; 
       cin>>n;
       for(int i = 0; i < n; i++)
       {
           cin>>s;
           a[i] = BKDRHash(s);  //存储每一个字符串的哈希值
       }
    
       int ans = 0;
       sort(a, a+n, cmp);
       for(int i = 0; i < n; i++)
       {
           if(a[i] != a[i+1])
           {
               ans++;
           } 
       }
       cout<<ans;
   }
   ```

* 进制哈希的应用：
  * 两个字符串S1+S2 的哈希值为：H(S1+S2) = H(S1) * P^len(S2) + H(S2) //即向左移动len(S2)位.
  * 可以快速计算字符串S的所有前缀，eg:S="abcde", 则前缀有{a,ab,abc,abcd,abcde}
  * 快速计算：
    * 计算a的哈希值：得H(a), 时间复杂度O(1)
    * 计算ab的哈希值：得H(ab) = H(a)^P + H(b), 时间复杂度为O(1)
    * .......只需要一个for循环即可在O(n)内求解所有前缀，然后便可求解任意区间字符的哈希值：
    * H(de) = H(abcde) - H(abc)*P^2  （求区间[L, R]的哈希值的代码可以写成：`ull get_hash(ull L, ull R) {return H[R] - H[L-1] * P[R-L+1]  //P[i]表示P的i次方}`


* 进制哈希与最长回文串
* 进制哈希与循环节
------------

 
   
