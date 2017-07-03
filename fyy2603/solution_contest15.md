A

Problem description
求ax+b=cy+d的正整数解,a,b,c,d<=100

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

Data Limit：n <= 1e5  Time Limit: 1s

Solution

Code

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

