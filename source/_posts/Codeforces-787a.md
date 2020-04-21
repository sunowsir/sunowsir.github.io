---
title: Codeforces-787a
tags:
- 题解
- codeforces
cover: title.jpg
mathjax: 'true'
date: 2019-09-02 16:48:33
---

> [题目传送](https://vjudge.net/problem/709847/origin)
* 题目思路：
  拓展欧几里德：
  $$
  a*x+b=c*y+d; <=> a*x+c*y=d-b;
  $$


代码：
```c++
#include<bits/stdc++.h>
using namespace std;

#define ll long long

ll exgcd(ll a,ll b,ll &x,ll &y){
    if(b==0){
        x=1;
        y=0;
        return a;
    }
    ll d=exgcd(b,a%b,x,y);
    ll tmp=x;
    x=y;
    y=tmp-a/b*y;
    return d;
}

int main(){
    ll a,b,C,D,x,y;
    while(cin>>a>>b>>C>>D){
        if(b<D){//若b<D,那么y<0，
            //原方程式等价于y=(a*x+b-d)/c,
            //下面的处理可保证x不小于0,但是不能保证y，
            //所以需要保证(a*x+b-d)%c==0,即：保证：b>D；若不成立需交换；
            swap(a,C);
            swap(b,D);
        }
        ll d = exgcd(a,C,x,y);
        ll c = D-b;
        if(c%d)  cout<<"-1"<<endl;
        else{
            x=x*(c/d);
            x=(x%(C/d)+(C/d))%(C/d);
            cout<<b+a*x<<endl;
        }
    }
    return 0;
}
```
