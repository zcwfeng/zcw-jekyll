---
layout: post
title: "深入浅谈之递归全排列问题"
description: ""
comments : false
category: lessons
tags: []
---
{% include JB/setup %}

### 全排列算法描述
首先我们来全排列ABCD这一序列。

写一个perm方法：perm(int a[],int n,int k)

a[]:代表要排列的内容用数组存放。

n：表示要排列几个数。

k：表示当前排列的状态排列到第几个数。

逻辑方法不变：每一层都是排列

规模不断变小：排完第一个位置后排后面（n-1） 个位置，依次递推。

终止条件：排到最后一个的时候（本次采用的是交换方法所以只需排到n-1就行了）

>算法demo1
设数组a[] =｛"A","B","C","D"｝
    
    #include<iostream>
  
    using namespace std;
  
    void perm(char a[],int n , int k)
  {

       if(k==n-1)
       {//这是终止条件因为是交换所以到n-1步的时候就等于排好了全部了。

           for(int i=0;i<n;i++)

               cout<<a[i]<<" "; cout<<endl;

       }

       else{

           for(int i=k;i<n;++i)

           {

               int temp = a[i];//交换步骤

               a[i] = a[k];

               a[k] = temp;

               perm(a,n,k+1);//确定排完第一个之后排接下去的（n-1）个。

               temp = a[i];//排完后要复原状态

               a[i] = a[k];  a[k] = temp;

           }
       }   
  }
       
    int main(){
        char a[] = {'A','','c','d'};
        perm(a,4,0);
        return 0;
    }
    
>demo2 C语言 【1234】

    #include <stdio.h>
    int a[] = {1,2,3,4};
    void perm(int m[],int k,int n)
    {

	if(k == n-1)
	{
		int i;
		for(i=0;i<n;i++)
		{
			printf("%d ",a[i] );
		}
		printf("%s\n","");
	}
	else
	{
		int i;
		for(i=k;i<n;i++) {
			int temp = m[i] ;
			m[i]  = m[k] ;
			m[k]  = temp;
			perm(a,k+1,n);
			temp = m[i] ;
			m[i]  = m[k] ;
			m[k]  = temp;

		}

	}

    }

    int main(void)
    {
        perm(a,0,4);
        return 0;
    }
