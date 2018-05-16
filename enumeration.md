## 题目要求
请写一个程序, 确定:
• 在各条青蛙行走路径中, 踩踏水稻最多的那一条上, 有多
少颗水稻被踩踏

• 例如, 图4中答案是7, 因为第6行上全部水稻恰好构成一
条青蛙行走路径


程序输入
• 从标准输入设备上读入数据

• 第一行上两个整数R, C, 分别表示稻田中水稻的行数和
列数, 1≤R, C≤5000

• 第二行是一个整数N, 表示被踩踏的水稻数量,
3≤N≤5000

• 在剩下的N行中, 每行有两个整数, 分别是一颗被踩踏水
稻的行号(1~R)和列号(1~C), 两个整数用一个空格隔开
• 且每棵被踩踏水稻只被列出一次


程序输出

• 从标准输出设备上输出一个整数

• 如果在稻田中存在青蛙行走路径, 则输出包含最多水稻
的青蛙行走路径中的水稻数量, 否则输出0

### solution

	//枚举
	
	#include <iostream>
	#include<algorithm>
	
	using namespace std;
	
	int r,c,n;
	struct PLANT{
	    int x, y;
	};
	PLANT plants[5001];
	PLANT plant;
	
	int searchPath(PLANT secPlant, int dx, int dy);
	int main()
	{
	    int i, j, dx, dy, px, py, steps, maxi = 2;
	    cin>>r>>c;//x 沿着行增加， y沿着列增加
	    cin>>n;
	    for(i=0; i<n; i++)
	        cin>>plants[i].x>>plants[i].y;
	    sort(plants, plants+n);
	
	    for(i=0; i<n-2; i++)//i is the first point, there should be at least 3 points ,so it is n-2
	    {
	        for(j=i+1; j<n-1; j++)
	        {
	            dx = plants[j].x - plants[i].x;
	            dy = plants[j].y - plants[i].y;
	            px = plants[i].x - dx;
	            py = plants[i].y - dy;
	            if(px <= r && px >=1 && py <= c && py >= 1)//如果第一点的前一点还在田里， 则说明选择的dx不好，也就是第二点不好
	                continue;//j+1 新选第二个点， 进行下一次运算
	            if(plants[i].x + (maxi -1)*dx > r)//x在小于步数就出边界了，说明第二点不对
	                break;// 因为点是排序了的，因此若当前第二个点在小于确定的步数就出边界了，那么其他可选的j都比这个点更远，更不可能对，所以break，选择一个新的第一点
	
	            py = plants[i].y +(maxi-1)*dy;
	            if(py > c || py < 1)
	                continue;//y 提前出界了，换第二个点
	            steps = searchPath(plants[j], dx,dy);//看从这两点出发能走多少步
	            if(steps > maxi)
	                maxi = steps;
	
	        }
	
	    }
	    if(maxi == 2)
	        maxi = 0;
	    cout<<maxi<<endl;
	    return 0;
	}
	
	bool operator<(const PLANT &p1, const PLANT &p2)
	{
	    if(p1.x == p2.x)
	        return p1.y <p2.y;
	    return p1.x < p2.x;
	}
	
	int searchPath(PLANT secPlant, int dx, int dy)
	{
	    PLANT plant;
	    int steps;
	    plant.x = secPlant.x + dx;
	    plant.y = secPlant.y + dy;
	    steps = 2;
	    while(plant.x <= r && plant.x >= 1 && plant.y <= c && plant.y >=1)
	    {
	        if(!binary_search(plants, plants+n, plant))//搜索每一步是否都踩在水稻上
	        {
	            steps = 0;
	            break;
	        }
	        plant.x += dx;
	        plant.y += dy;
	        steps++;
	    }
	    return(steps);
	
	}
