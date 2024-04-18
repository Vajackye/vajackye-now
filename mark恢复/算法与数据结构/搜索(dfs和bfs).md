* 深搜与广搜 区别①广搜定义结构体，求step，深搜回溯求
* 广度搜索优先：
* 经典走迷宫：(起点到终点，求最短路，若有条件限制，还需要优化，可设置一个数组？存储步数，当再次走过该点，比较，选择最优路)
```c++
#include<bits/stdc++.h>
using namespace std;
char maze[100][100];
int book[100][100];
int dir[4][2] = {{0,1},{1,0},{0,-1},{-1,0}};//上下左右四个坐标 走向
int n, m; 

//坐标存储进入队列，步数也存入 
bool stayin(int tx, int ty) {
	return x>=0&&x<n&&y>=0&&y<m;
}
struct position
{
	int x, y, step;
	position(int px, int py, int pstep): x(px), y(py), step(pstep){ }
}

int bfs(int sx, int sy) {
	queue<position> que;//存储 
	q.push(position(sx, sy, 0));//起点入队
	book[sx][sy] = 1;
	//开始每个出入队，遍历所有结点 
	while(!que.empty()) {
		int x = que.front().x;//获取当前坐标与步数 
		int y = que.front().y;
		int step = que.front().step;
		que.pop();
		//开始四个方向走一波 
		for(int i = 0; i < 4; i++) {
			int tx = x + dir[i][0];
			int ty = y + dir[i][1];
			//越界，非障碍，未走过 
			if(stayin(tx,ty)&&maze[tx][ty]!='#'&&!book[tx][ty]) {
				if(maze[tx][ty] == 'T') {
					return step+1;
				}
				//如果上面外if都满足，且不是终点
				q.push(position(tx, ty, step+1));
				book[tx][ty] =1;
			}
		} 
	}
	return -1;//遍历所有，都到不了终点 
	
}
int main() {
	int sx sy;
	cin>>n>>m;
	for(int i = 0; i < n; i++) {
		//cin>>maze[i];//也可，行的列，当作string输入 
		for(int j = 0; j < m; j++) {
			cin>>maze[i][j];
			if(maze[i][j] == 'S') {
				sx = i;
				sy = j;
			}
			
		}
	}
	cout<<bfs(sx,sy);//输出步数 
} 
```
* 深度优先搜索
* 经典走迷宫：（起点走迷宫，搜索全路径，找到通路，修改一下，可求最短路，需要比较min，优化）
```c++
#include<iostream> 
#include<math.h>
#include<memory.h>
#include<stack>
using namespace std;
//这是设定的状态转移变量，分为上下左右4组，每一组的值分别代表X,Y的偏移
int dst[4][2]={//上下左右 
                -1,0,
                1,0,
                0,-1,
                0,1
              }; 
//迷宫，终点设置为数字3，已经走过的节点设置为4，测试样例
int  maze[5][5] = {

        0,1, 0, 0, 0,

        0,1, 0, 1, 0,

        0,0, 0, 0, 0,

        0,1, 1, 1, 0,

        0,0, 0, 1, 3,

};

void dfs(int x,int y)
{

    if(maze[x][y]==3)//判断是否走到了终点，走到了就是输出找到的解
    {//if里面是对可行解的一个判断表达式，里面的话就执行我们得到一个解后要进行的操作。
        for(int i=0;i<5;i++)
        {
            for(int j=0;j<5;j++)
            {
                cout<<maze[i][j]<<" ";
            }
            cout<<endl;
        }
        cout<<endl;
        return ;
    }

    for(int i=0;i<4;i++)//枚举转移状态
    {

        int nextx = x+dst[i][0];//计算转移状态
        int nexty = y+dst[i][1];
        //下面这里就是DFS的核心部分了，判断转移是否合法，合法的递归进去，不合法的，不进行搜索，if需要包含全部判断条件，不可缺一，否则搜索回出问题
        if(nextx>=0 && nextx<=4 && nexty>=0 && nexty<=4&&(maze[nextx][nexty]!=1)&&(maze[nextx][nexty]!=4))//判断下一个要走的点是否合法，在迷宫的题目里面主要是判断转移的点能不能走 
        {
            maze[x][y] = 4;//设置当前点为走过   
            dfs(nextx,nexty);//进一步搜索            
            maze[x][y] = 0;//退出来设置为没有走过，这样在回溯进行后续搜索时，不会影响对路径的搜索     
        }
    }

    return ;
} 
int main()
{

  dfs(0,0);//初始调用

 return 0;

}
```
dfs求step：
```c++
#include<iostream>
using namespace std;
char _map[10][10];//地图
int n, m, ans = 0x3f3f3f3f;
int dir[4][2] = { 0,1,1,0,0,-1,-1,0 };
int book[10][10];

void dfs(int sx, int sy, int step) {
	//递归终止条件，待会stack替代 
	
    //剪枝
    if(ans < step) return ;
	if (_map[sx][sy] == 'T') {
		ans = min(ans, step);
		return;
	}
	for (int i = 0; i < 4; i++) {
		int px = sx + dir[i][0], py = sy + dir[i][1];
		if (px >= 0 && px < n && py >= 0 && py < m && _map[px][py] != '#' && book[sx][sy] != 1)
		{
			//当前点标记 
			book[sx][sy] = 1;
			//走到底 
			dfs(px, py, step + 1);
			//回溯
			book[sx][sy] = 0;
		}
	}
	return;
}

int main() {
	int sx, sy;
	int step = 0;
	cin >> n >> m;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			cin >> _map[i][j];
			if (_map[i][j] == 'S') {
				sx = i;
				sy = j;
			}
		}
	}
	dfs(sx, sy, step);
	cout << ans;
	return 0;
}
```
