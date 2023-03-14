### 竞赛细节

* 输入输出：测试数据一般都是多组，如果惟有告诉数据数量，就要while(scanf("%d", &a) != EOF)  输入的数据实际上就是文件。EOP->end of file； 或者：while(cin>>a>>b)//==0停止
(其实：多组测试数据封在一个文件夹里测试)
![34701287dc6d9a6eb1195e7dbb6800a](https://user-images.githubusercontent.com/121871885/221875566-00712b78-cf48-4d60-b0b0-4a473e390499.jpg)

* cin.getline(变量名，读取最长长度);//读取一行，避免scanf的'%s'和cin不读取空格
* getline(cin, string name);//格式，其中getline在string头文件中
* getline参考网址：http://c.biancheng.net/view/1345.html
* 对于字符数组char c[];容量一般要加1（题目所给字符长度+1），因为要'\0'终止字符串，'\0'占一个字符。
* 输入多组文件时，每次测试完一组，要重新初始化某些**含有计算过的值**的变量（所以，关键变量都要放在测试数据内）

### 编译报错：
* ![01344c63506bc223cbff271bcf1ef43](https://user-images.githubusercontent.com/121871885/221873206-5eb80396-3474-4b0a-8a91-223b39ad7656.jpg)
* expected member name or ';' after declaration specifiers:情况1：定义多维数组同时初始化，里面的值之间用","隔开，不是";"，只有初始化完成，才有;


### 文件测试数据：
* 用记事本记录测试数据， 文件名类型：*_*（非txt）。

### 思想：
* 条件if判断如果多了，时间复杂度也会提升
* 极端化思考，如果代码太长（重复的），那就想一个好的策略
* 归纳,写出通项公式，具体分析，举小例子
* 逆序思想，比如最后一个结果不输出空行：第一行不输出空行，接下来：先空行在输出值
