A

Problem description
求ax+b=cy+d的非负整数解,a,b,c,d<=100

Solution
数据太水。直接令a=1,2,3......1000000；b=1,2.3，......1000000，看有没有交集即可、
如果数据规模后面加几个0可以用扩展欧几里得
Code
```cpp
#include<bits/stdc++.h>
using namespace std;
int a,b,c,d,j=1,ans=2000000000,x[1000001],y[1000001];
int main() 
{
	cin>>a>>b>>c>>d;
	x[1]=b; y[1]=d; 
	for (int i=2;i<=100000;i++) x[i]=x[i-1]+a;
	for (int i=1;i<=100000&&y[i-1]+c<x[100000];i++)
	 {
	 	if (i!=1) y[i]=y[i-1]+c; 
		while (y[i]>x[j]) j++;
	 	if (y[i]==x[j]) ans=min(ans,x[j]);
	 }
	 if (ans<2000000000) cout<<ans;
	  else cout<<-1;
	return 0;
}
```
B

Problem description
数学建模后就是判断一个序列中有无相反数（难点在于题目鸟语看不懂）
Data Limit：n <= 7000*7000  Time Limit: 1s

Solution
对于每一段序列使用计数排序即可
Code
```cpp
#include<bits/stdc++.h>
using namespace std;
int a[10001],b[10001],yes,ans=0;
int main()
 {
 	int n,m,k,x; cin>>n>>m;
 	for (int i=1;i<=m;i++)
 	 {
 	 	yes=1;
		scanf("%d",&k);
 	 	memset(a,0,sizeof(a));
 	 	memset(b,0,sizeof(b));
 	 	for (int j=1;j<=k;j++) 
 	 	 {
			 scanf("%d",&x);
			 if (x>0) a[x]++;
			 if (x<0) b[-x]++;
			 if (x>0&&a[x]&&b[x]) yes=0;
			  else if (x<0&&a[-x]&&b[-x]) yes=0;
		   }
		if (yes) ans=1;
	  }
	if (ans) cout<<"YES";
	 else cout<<"NO";
	return 0; 
 }
```
赛后补题

C

Problem description
比赛的时候：鸟语啊看不懂啊。比赛一半：啊啊啊我真的看不懂啊。比赛快结束：我居然看懂了！！！但我不会做啊啊啊啊。题目是有一个编号1--n的棋盘，1的位置有一个黑洞，其它某一位置有怪物。A，B有各一个整数序列，他们轮流从序列中选择一个数x，将怪物推到前方x格。将怪物推入黑洞的人获胜。对于每一个怪物可能的位置，分别输出A或B先手时，A或B可以取得的最佳结果。

Data Limit：n <= 7000  Time Limit: 4s

Solution
博弈论+记忆化搜索。用f[i]表示A选手位于i的结果（1表示Win，0表示Loop，-1表示Lose）g[i]表示B选手位于i的结果。如果f[i]可以到达B的必败点（如g[1]），则f[i]为A的必胜点。如果F[i]只能到达B的必胜点，则f[i]为A的必败点。否则，存在策略使得Loop成立。搜索一次不能保证搜索出正确答案，可以往复搜索两次。同时，每次搜索要用vis数组记录下当前状态是否已经被搜索过，避免死循环。
Code
```cpp
#include<bits/stdc++.h>
using namespace std;
int f[7001],g[7001],a[7001],b[7001];  //f:先发选手位于i的结果 
int vis[2][7001];                     //v:记录是否被访问过 
int k1,k2,n,m;                        //g:后发选手位于i的结果 
int search(int k,int x)               //k=0，先发选手移动；k=1，后发选手移动 
{ 
	if (k==0&&f[x]!=0) return f[x];
    if (k==1&&g[x]!=0) return g[x];
	if (vis[k][x]) return 0;
	int u=0,v=0;
	vis[k][x]=1;
	if (k==0)
     for (int i=0;i<k1;i++)
      {
       	if (search(1,(x+a[i])%n)==-1) f[x]=1;    	
      	if (search(1,(x+a[i])%n)==1) u++;    	
	 }
	if (k==1)
	 for (int i=0;i<k2;i++)
	  {
	  	if (search(0,(x+b[i])%n)==-1) g[x]=1;
	  	if (search(0,(x+b[i])%n)==1) v++;
	 }
	 if (u==k1) f[x]=-1;
	 if (v==k2) g[x]=-1;
	 if (k==0) return f[x];
	 if (k==1) return g[x];
}
int main()
 {
 	cin>>n>>k1;
 	for (int i=0;i<k1;i++) scanf("%d",&a[i]);
 	cin>>k2;
 	for (int i=0;i<k2;i++) scanf("%d",&b[i]);
 	g[1]=-1;f[1]=-1;
 	for  (int j=0;j<=1;j++)
 	 {
 	 	memset(vis,0,sizeof(vis));
		for (int i=0;i<=n-1;i++) { search(0,i); search(1,i); }
		memset(vis,0,sizeof(vis));
	 	for (int i=n-1;i>=0;i--) { search(0,i); search(1,i); }
	  }
 	for (int i=2;i<=n-1;i++) 
 	 if (f[i]==1) printf("Win ");
 	  else if (f[i]==-1) printf("Lose ");
 	   else printf("Loop ");
 	if (f[0]==1) printf("Win ");
 	  else if (f[0]==-1) printf("Lose ");
 	   else printf("Loop ");
 	cout<<endl;
 	for (int j=2;j<=n-1;j++)
 	 if (g[j]==1) printf("Win ");
 	  else if (g[j]==-1) printf("Lose ");
 	   else printf("Loop ");
 	 if (g[0]==1) printf("Win ");
 	  else if (g[0]==-1) printf("Lose ");
 	   else printf("Loop ");
    return 0;
 }
```
D

Problem description

Data Limit：n <= 1e5  Time Limit: 1s

Solution

Code

E

Problem description

Data Limit：n <= 1e5  Time Limit: 1s

Solution

Code

