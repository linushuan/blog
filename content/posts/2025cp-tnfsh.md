---
title: "2025資訊校內能競" # 標題
date: 2025-10-02T19:25:26+08:00 # 發布時間
draft: false # 草稿
description: "2025TNFSH校內資訊能競" # ani 摘要
summary: "2025TNFSH校內資訊能競" # sim 摘要
author: "Wonderhoi" # 作者

# can put many in
tags: ["daily", "cp"] # 標籤
categories: ["CP", "Coding", "Daily"] # 分類

math: true            # Latex 支援
toc: true             # 是否顯示目錄 (Anatole 支援)

# picture put in static/
# thumbnail: "arima.png" # Anatole
cover: "arima.png"     # Reimu
---

> 2026 發現自己這個寫了好多於是就從 hackmd 搬過來了

> 最好趁記得的時候打一打 不然會像我的選訓心得一樣

賽前跟 tobiichi 說這次目標是前5
<small>居然達成了不可思議</small>

今天早上考地科的能競 然後燒機
所以早上心態其實沒有很好
~~雖然也有可能是這樣所以打code發洩情緒~~

第四節吃完飯就跟 asdfg 和 brinton 去萊爾富買飲料
~~原翠 真理果綠果然厲害~~
然後就過去社部了

## 測機
第一題和第二題就很水
第三題是互動題 題目看錯 燒雞了一陣子
發現是題目看錯 結果還是98.2分
但至少有熟悉了互動題 不然很久沒打了

bonus1: 帳號偷懶沒有把前綴的24改成25 ~~譴責~~
bonus2: 剛開始tobiichi忘記把正式賽題目關掉 所以記分板有題目名稱ww

## 正式賽
一開始先開了wsl創檔案 cpeditor打模板
我真的不會用windows

## pA
一開始沒管那麼多就直接寫pA 果然是水題 位元枚舉一下就好
但也花了10幾分鐘
賽後被 blame 打爆 忘了可以用 next_permutation()

bonus1: 一開始錯了一次 原因是忘記重置變數戳出去
但本地沒跟我說 不嘻嘻
bonus2: 我用int128砸ww 怕溢位

```cpp=
#include<bits/stdc++.h>
using namespace std;
#define squre(x) ((x)*(x))

void solve() {
	long long xy[10][2], toge2[5], toge1[5];
	__int128 len1[5],len2[5];
	bool yess=0;
	for(int i = 0; i<6; i++) {
		cin>>xy[i][0]>>xy[i][1];
	}
	int t;
	for(int i = 15; i < (1<<6); i++) {
		t = 0;
		for(int j = 0; j < 6 ;j++) t+=(i>>j)&1;
		if(t!=3) continue;
		t = 0;
		for(int j = 0; j < 6 ;j++){
			if((i>>j)&1) toge1[t] = j;
			else toge2[j-t] = j;
			t+=(i>>j)&1;
		}
		for(int i = 0; i<3;i++) {
			len1[i] = squre((__int128)xy[toge1[i]][0]-(__int128)xy[toge1[(i+1)%3]][0]) + squre((__int128)xy[toge1[i]][1]-(__int128)xy[toge1[(i+1)%3]][1]);
			len2[i] = squre((__int128)xy[toge2[i]][0]-(__int128)xy[toge2[(i+1)%3]][0]) + squre((__int128)xy[toge2[i]][1]-(__int128)xy[toge2[(i+1)%3]][1]);
		}
		sort(len1,len1+3);
		sort(len2,len2+3);
		for(int i = 0; i<3;i++) {
			if(len1[i]!=len2[i]) goto haha;
		}
		yess = 1;
		break;
		haha:;
	}
	cout<<(yess?"Yes":"No")<<'\n';
}

int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	int t = 1;
	// cin>>t;
	while(t--) {
		solve();
	}
	return 0;
}
```


## pB 
其實在寫的時候看到有人寫pC 90幾分 就知道是互動題了
~~所以先繼續寫pB~~
發現是數學題所以覺得自己很有機會寫很快
發現是要檢測質數 就無腦刻了miller-rabin質數測試
結果寫錯 :( 燒雞
而且一開始在算要開到幾次方根時 我把 $10^{18}$ 寫成 $10^8$ 所以次方數算錯然後燒雞ww
大概花了30分鐘才發現
中間看到很多人拿了pB 100分 就覺得自己想法有問題了ww
換了檢驗質數演算法之後才發現自己是智障 但還是只拿了60分
因為一直debug不出來 所以就跑去寫pC了

因為60分是TLE
所以在想說怎樣可以加快
有注意到t次方從1枚舉需要的數字太慢了
所以在想怎麼加速
這時候突然有一個靈感告訴我
***今天都還沒用到二分搜***
然後就想到t次方根數字可以用二分搜找了
就在很後面拿了一個AC 爽
這個時候就拿了400分 還有一個小時
發現 paul 還沒寫出 pF 所以目標就是寫出 pE
追平 asdfg 但他那個時候好像已經寫出 pE 只是 pB還是60分

bonus1: 寫完之後回家才發現自己的質數檢驗法一直都是寫錯的 :wa:
bonus2: 中間發現 brinton 藏扣 後來回來寫這題又發現他破台了 太強 :place_of_worship: 

```cpp=
#include<bits/stdc++.h>
using namespace std;

long long fsp(__int128 a, int b, long long c) {
	__int128 tmp = 1;
	for(;b>0;b>>=1) {
		if(b&1) tmp = tmp*a;
		a = a*a;
		if(tmp>=c || (a>=c && ((b>>1)!=0))) return LLONG_MAX;
	}
	return tmp;
}
set<int> prime1;
bitset<3000005> isprime;
bool check_prime(int a) {
	if(prime1.count(a)) return 1;
	else if(*prime1.rbegin() < a){
		for(auto& i:prime1){
			if(a%i==0) return 0;
		}
	}else return 0;
	return 1;
}

void prime(int n) {
	for(int i = 2;i<=n;i++) {
		if(!isprime[i]){
			prime1.insert(i);
		}
		if((long long)i*(long long)i>(long long)n) continue;
		for(int j = i * i; j<=n;j+=i) {
			isprime[j] =1;
		}
	}
	return;
}

bool check(int i,long long n,long long k) {
	if(fsp(k,i,LLONG_MAX)>=n) return 1;
	else return 0;
}

int sqrtt(int i,long long n){
	int l = 0, r = (int)sqrtl(n), mid = (l+r)>>1;
	while(l+1<r){
		mid = (l+r)>>1;
		if(check(i,n,mid)){
			r = mid;
		}else{
			l = mid;
		}
	}
	return l+1;
}

void solve() {
	long long n;
	cin>>n;
	prime(3000000);
	if((long long)sqrtl(n)*(long long)sqrtl(n) == n){
		if(check_prime((int)sqrt(n))){
			cout<<"Yes\n";
			return;
		}
	}
	for(int i = 3; i < 45; i++) {
		for(long long j = sqrtt(i,n); fsp(j,i,LLONG_MAX) <= n;j++) {
			if(fsp(j,i,LLONG_MAX) == n) {
				if(check_prime(j)){
					cout<<"Yes\n";
					return;
				}
			}
		}
	}
	cout<<"No\n";
	return;
}

int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	int t = 1;
	// cin>>t;
	while(t--) {
		solve();
	}
	return 0;
}
```

## pC
看到題序差不多 快速看完題目發現是數學水題 筆寫了兩條式子就推出來了
~~但其實根本就不用寫就是了~~
恩 就爽快的AC了
原本以為互動題會更難的說

bonus: 有吃WA是因為我把 $b-a$寫成 $a-b$ 可惡

:::spoiler ACcode

```cpp=
#include<bits/stdc++.h>
using namespace std;

vector<int> wow(1005,0);
int compare_numbers(int a, int b);
void bob_init(int n){
	int all = n*(n+1)/2, sum=0;
	for(int i = 2; i<=n;i++) {
		wow[i] = compare_numbers(i, 1);
		sum+=wow[i];
	}
	wow[1] = (all-sum)/n;
	for(int i = 2; i<=n;i++) {
		wow[i]+=wow[1];
	}
	return;
}

int query_from_alice(int a) {
	return wow[a];
}
```


## pD
看完題目
覺得非常熟悉 就一臉DP樣
看了數字範圍 嗯嗯 $O(N^2)$ 我絕對會寫的
雖說如此 轉移式有推對 但是實做小燒雞
但其實是我在紙上寫太爛 賽後看題解才想到自己開二維陣列根本是腦霧

bonus1: 這題我大概註解掉的code:實際演算的code大概是 1:1 超好笑
bonus2: 又吃一次WA的原因是我不小心把輸出的code註解掉了(因為那裡也有拿來debug的輸出ww)

```cpp=
#include<bits/stdc++.h>
using namespace std;

void solve() {
	int n;
	cin>>n;
	long long ans=0;
	vector<long long> vl(n+1),sum(n+1,0);
	for(int i =1;i<=n;i++) cin>>vl[i];
	for(int i = 1;i<=n;i++){
		sum[i] = sum[i-1]+vl[i];
	}
	vector<vector<long long>> dp(n+2,vector<long long>(n+2,0));
	vector<long long> dp2(n+1,0);
		for(int j = 1;j <= n;j++){
			for(int i = 1;i <= j;i++){
			// cout<<(dp[0][i-1])<<" "<<((sum[j]-sum[i-1])*(j-i+1))<<" "<<dp[0][i-1]<<'\n';
			dp[i][j] = max((sum[j]-sum[i-1])*(j-i+1),dp[i][j]);
			// dp[1][j] = max(dp[1][j],dp[1][i]+dp[i+1][j]);
		}
		// for(int i = 1; i<=j;i++){
			// dp[0][j] = max(dp[0][j],dp[0][i]+dp[i+1][j]);
		// }
		
	}
	for(int i = 1;i <=n;i++){
		for(int j=0;j<=i-1;j++){
			dp2[i] = max(dp2[i],dp2[j]+dp[j+1][i]);
		}
		// cout<<dp2[i]<<'\n';
	}
	cout<<dp2[n]<<'\n';
}

int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	int t = 1;
	// cin>>t;
	while(t--) {
		solve();
	}
	return 0;
}
```

## pE
好又是地震
好地質小組
~~這不AC說不過去吧~~
看完題目其實稍微想了一兩分鐘
但因為有寫出 pA到pD所以信心大增
而且看到很多人包括 JKdelta都寫出pE了
就覺得自己一定可以

有初步想法後發現是BIT覺得有點怪
因為初選好像不太容易出資結?
但是因為只是BIT所以好像又還好
就先刻了一下
在實做更改的部份時 發現單純陣列操作很難處理
但又想不太到 ~~也因為三個多小時沒上廁所有點憋不住了~~
所以就跑去上~~炸~~廁所了

廁所上一上就剛好想到之前地震那題是差分兩次
所以就想到了差分 超棒 今天通靈得很成功
回來打code結果實做繼續燒雞
1. 更改的時候忘了把原本 h[l-1]<h[l] 改成 h[l] > 0 大概debug 5分鐘
2. bit.modify(int value, int pos) 我在呼叫的時候一直寫反 想說怎麼都對不上
3. 看錯題目 $H_i<H_{i+1}$ 看成 $H_{i-1}<H_i$ 想說怎麼對不到範圍 是不是題目出錯了

最後debug完之後丟上去就AC了
500分 get 好爽 就稍做休息了www

bonus: 這題依然錯了一次 原因是因為第三點ww 後來馬上就發現自己看錯題目了

```cpp=
#include<bits/stdc++.h>
using namespace std;

struct BIT{
	int n;
	vector<int> bit;
	vector<int> ori;
	int lowbit(int x){
		return x&-x;
	}
	void setup(int k){
		bit.resize(k+1,0);
		n = k;
		ori.resize(n+1,0);
	}
	void modify(int k,int p) {
		for(int i = p; i<=n;i+=lowbit(i)){
			bit[i]+=k-ori[p];
		}
		ori[p]+=k-ori[p];
		return;
	}
	int query(int p){
		int ans=0;
		for(int i=p;i>0;i-=lowbit(i)){
			ans+=bit[i];
		}
		return ans;
	}
};

void solve() {
	int n,q,o,l,r,c,a,b;
	cin>>n>>q;
	BIT bit;
	vector<long long> h(n+5,0),hh(n+5,0);
	for(int i=1;i<=n;i++){
		cin>>h[i];
		hh[i] = h[i]-h[i-1];
	}
	// for(int i=1;i<=n;i++) cout<<hh[i]<<'\n';
	bit.setup(n);
	hh[1]=LLONG_MIN;
	for(int i=1;i<=n;i++)
		if(hh[i]>0){
			bit.modify(1,i);
		}
		// cout<<bit.query(5)<<'\n';
	while(q--){
		cin>>o;
		if(o==1){
			cin>>l>>r>>c;
			hh[l]+=c;
			hh[r+1]-=c;
			if(hh[l]>0) bit.modify(1,l);
			if(hh[r+1]<=0) if(r+1<=n) bit.modify(0,r+1);
		}else{
			cin>>a>>b;
			cout<<bit.query(b)-bit.query(a)<<'\n';
		}
	}
}

int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	int t = 1;
	// cin>>t;
	while(t--) {
		solve();
	}
	return 0;
}
```

## pF
因為已經500分了 而且感覺大家 pF 都燒雞(當然 除了brinton) 所以我就慢慢看題目
看完題目第一個想法是DP 但覺得怪怪的
腦海中有一瞬間閃出之前我也想成DP的最短路(CF2300的某題) 要建虛點之類的 但因為我不會那東西所以就放棄了

原本排名都還在第二 發現自己變第三 原因是因為 blame拿了四分
當時我想說 乾不是 blame連這個也要刮 那我也來拿一下4分好了
然後就開始亂寫 感覺對了就傳上去看看
結果一直WA 最後才把bug de掉 成功拿下最後4分
但後來 paul 拿了48分就又從2掉到3了
我也才發現題目配分有出入 跑去提交了第一個提問ww

bonus1: blame其實沒有刮分 抱歉
bonus2: 我靠這個贏了 asdfg 4分
bonus3: 我有一筆CE是因為max(long long, 0)可惡


## bonus
- CPeditor燒雞1 比賽一開始編譯的時候都會卡住 大概要5-10秒才會好 根本201吧
- CPeditor燒雞2 在TLE的時候再次編譯會出現權限不足 我只好一直開檔案www
- pB submit大師
![圖片](https://hackmd.io/_uploads/HkCIxDgslx.png)
- 最後一刻發現 pF 配分有問題 但 tw87 不回我 :qaq:
- 沒一題是一發AC的 我好菜
- 贏了 asdfg 好爽

- 記分板:
![圖片](https://hackmd.io/_uploads/SyP--Dlilg.png)


<small>cover from: 我推的孩子</small>
