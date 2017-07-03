# 比赛记录

[比赛链接](https://www.codeforces.com)

## A
### Problem description
> 输入一堆单词。如果两个单词输入的间隔大于C单词就会没掉
### Solution
每读入一个和上一个比对暴力即可
```cpp
for (int i=1;i<=n;i++)
	 {
	 	scanf("%d",&a[i]);
	 	if (a[i]-a[i-1]>c) ans=1;
	 	 else ans++;
	 }
```

***** 
# 赛后补题

## B
### Problem description
> 给你一个由大写字母和问号组成的字符串。将问号改成大写字母，使得这个字符串存在一个子串，它长度为26且正好包含所有字母。输出一个方案即可。
### Solution
长度小于26.直接输出-1.否则维护一段长为26的区间，记录区间中每个字母出现的次数，出现字母的种树cnt，出现问号的个数p。当且仅当cnt+p==26时，这个子串可以满足要求把子串变成满足要求的串，剩下的随便输出就可以了。
还有！
注意字符串的读入输出233333333333333333333
蒟蒻因为多输出了一个空格调了两个多小时（其中一个多小时的时间在比赛里）
```cpp
while ('A'<=s[r+1]&&s[r+1]<='Z'||s[r+1]=='?'||cnt+p==26)
	 {
	 	if (cnt+p==26)
	 	 {
	 	 	for (int i=l;i<=r;i++)
	 	 	 if (s[i]=='?')
	 	 	  for (int j=0;j<=25;j++)
	 	 	   if (num[j]==0&&s[i]=='?') {s[i]=j+'A'; num[j]++;} 
	 	 	ok=1; return ;
		}
		else 
		 {
		 	if ('A'<=s[l]&&s[l]<='Z')
		 	 { 	num[s[l]-'A']--; if (num[s[l]-'A']==0) cnt--; l++;	}
			else if (s[l]=='?')
			 { 	p--; l++; }
			if ('A'<=s[r+1]&&s[r+1]<='Z')
			 { 	r++; 
			    num[s[r]-'A']++;if (num[s[r]-'A']==1) cnt++; }
			else if(s[r+1]=='?')
			  {	r++;p++; }	  
		 }
	 }
```
##c
### Problem description
> 给出num=2，level=1； 你可以给num加上level，当你的num满足：1、是完全平方数；2、开平方根后是level+1的倍数时，你可以让num=sqrt（num），并且level+1；输出每一次level+1需要加level的次数。输出一种方案即可
### Solution
沉迷B题没有做C题的蒟蒻。。。。。。（估计看了C题题面也看不懂的）
易知num是level的倍数。要使num能开方，则（level*level）是num的因数。
要使num开方后是（level+1）的倍数，则（level+1）*（level+1）是num的因数
多种方案么就取那个最小的(level*(level+1)*(level+1)-num/level)好了
```cpp
 	for (long long i=1;i<=n;i++)
 	 {
 	 	cout<<(i*(i+1)*(i+1)-num/i)<<endl;
 	 	num=i*(i+1);
	  }
```
