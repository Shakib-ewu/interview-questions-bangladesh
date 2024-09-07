# WellDev Ltd

## Introduction

WellDev Ltd is a software company based in Zurich, Switzerland, specializing in software development and IT services. It has offices in Bangladesh (Dhaka), South Africa, Canada etc.

## Interview Stages

1. **Initial Screening:** After dropping CV they take a MCQ Round, almost every candidate gets an email for participation in this round.
2. **Round 1:** The first round is a technical round and generally lasts for an hour.
3. **Round 2:** The second round is divided into two part. The first part is a behavioural part taken by HR of the company. For the second part two software engineer conducts the technical sessions.
4. **COO Round:** The final round is taken by the COO of the company


## MCQ Round
A Broad Range of Topics  

This round consisted of a multiple-choice questionnaire covering these topics. The test required me to share my screen with Quillgo and keep my camera on. It covers wide range of topics like JavaScript fundamentals, OOP, DBMS, SWE principles, Networking, Rest API knowledge, Analytical reasoning, DSA (time complexity, sorting, binary trees, MST, greedy algorithms).

## First Round Questions
Hands-On Problem Solving

<details>
<summary>
Given an array, what will be the base address if we print the array name only (e.g., printf(ara))?
</summary>
<hr>
</details>

<details>
<summary>
Write a code to delete the middle element of a stack without using any additional data structure while preserving the original order. Input: [1, 2, 3, 4, 5]. Output: [1, 2, 4, 5]
</summary>
<hr>
</details>

<details>
<summary>
Given a recursive function that calculates the sum of the first N consecutive numbers, provide an appropriate, readable name for the function.
</summary>
<hr>
</details>

<details>
<summary>
What is the time complexity of the following code?

```C
int fun(int n) {
    if(n <= 1) return n;
    int x = fun(n - 1);
    int y = fun(n - 2);
    return x + y;
}
```
</summary>
<hr>

</details>

<details>
<summary>
Explain the order of SQL query execution (e.g., FROM, WHERE, GROUP BY, HAVING, SELECT).
</summary>
<hr>  
</details>

<details>
<summary>
Given a table with redundant data in multiple columns, how would you optimize it? (Hint: Normalization)
</summary>
<hr>
</details>

<details>
<summary>
Given a Java code, identify issues that violate access modifiers.
</summary>
<hr>
</details>

<details>
<summary>
Explain the basic concepts of Object-Oriented Programming (OOP).
</summary>
<hr>
</details>

<details>
<summary>
What are the ACID properties in DBMS?
</summary>
<hr>
</details>

<details>
<summary>
A basic GRE-like math question.
</summary>
<hr>
</details>

<details>
<summary>
Write a SQL query to show all the duplicate rows in a table.
</summary>
<hr>
</details>

<details>
<summary>
Can we make a stack with a queue?
</summary>
<hr>
</details>

## Second Round Questions

<details>
<summary>
Write an API call to check whether the system is running properly and explain a GET API call.
</summary>
<hr>  
</details>

<details>
<summary>
Write a code to create a directory and a text file inside it with “Hello World” written.
</summary>
<hr>
</details>

<details>
<summary>
What happens if two people try to reserve the same ticket simultaneously in a ticket reservation system? How would you solve this problem in a ticket management system? What will be your idea in this regard?
</summary>
<hr>
</details>

<details>
<summary>
How many APIs are required to solve the above ticket reservation problem?
</summary>
<hr>
</details>

<details>
<summary>
How can passwords be secured so that no one (even the administrator) can view them? How can password hashing be strengthened? What techniques do you know? (Hint: Salting and hashing techniques)
</summary>
<hr>
</details>

<details>
<summary>
What is a trigger in DBMS, and what does cascading mean?
</summary>
<hr>
</details>

<details>
<summary>
If we need to display a large amount of data on a website, what technique should be followed? (Hint: Pagination)
</summary>
<hr>
</details>

<details>
<summary>
What happens when we browse a website? How are the contents rendered?
</summary>
<hr>
</details>

<details>
<summary>
What is the difference between SQL and NoSQL?
</summary>
<hr>
</details>

<details>
<summary>
For storing values from cache memory to RAM, should we use SQL or NoSQL?
</summary>
<hr>
</details>

<details>
<summary>
Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.
</summary>
<hr>

[**💻 Submit Code**](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)

::: code-group

```C++ [Stack]
// src: https://www.geeksforgeeks.org/largest-rectangular-area-in-a-histogram-using-stack/
int largestRectangleArea(vector<int>& hist) {
    int n = hist.size();
    stack<int> s;

    int max_area = 0; 
    int tp; 
    int area_with_top; 
    int i = 0;
    while (i < n) {
        if (s.empty() || hist[s.top()] <= hist[i]){
            s.push(i++);
        } else {
            tp = s.top(); 
            s.pop();

            area_with_top = hist[tp] * (s.empty() ? i : i - s.top() - 1);
            max_area = max(max_area,area_with_top);
        }
    }

    while (s.empty() == false) {
        tp = s.top();
        s.pop();

        area_with_top = hist[tp] * (s.empty() ? i : i - s.top() - 1);
        max_area = max(max_area,area_with_top);
    }

    return max_area;
}
```
```C++ [Segment Tree]
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define pii pair<ll,ll>
#define F first
#define S second
const int MAX = 1e9+5;
const int N = 200005;
pii segtree[4*N];
int ara[N],n;
 
void build(int node,int l,int r ){
    if( l == r ){
        segtree[node] = {ara[l],l};
        return;
    }
    int mid = (l+r)/2;
    build(node*2,l,mid);
    build(node*2+1,mid+1,r);
    segtree[node] = min( segtree[node*2],segtree[node*2+1] );
}
 
pii query(int node,int L,int R,int l,int r){
    if( l>R or r<L ) return {MAX,-1};
    if( l>=L and r<=R ) return segtree[node];
    int mid = (l+r)/2;
    return min( query(node*2,L,R,l,mid), query(node*2+1,L,R,mid+1,r) );
}
 
ll getRect(int l,int r){
    if( l>r ) return 0;
    auto pp = query(1,l,r,0,n-1);
    ll res = (r-l+1)*pp.F;
    return max({ res, getRect(l,pp.S-1),getRect(pp.S+1,r) });
}
int main(){
    cin>>n;
    for(int i=0;i<n;i++) cin>>ara[i];
    build(1,0,n-1);
 
    cout<<getRect(0,n-1);
}
```
:::
</details>

<details>
<summary>
You have a 100-story building, and two marbles. A marble will break if dropped from a certain height (from any floor). Find the highest floor you can lift by dropping or utilizing exactly two marbles.
</summary>
<hr>
</details>

<details>
<summary>
Given a table with product_id, price, and product_name, write a query to find products with the same price.
</summary>
<hr>
</details>

<details>
<summary>
What is the difference between DELETE, TRUNCATE, and DROP in SQL?
</summary>
<hr>
</details>

<details>
<summary>
Explain threading in OOP.
</summary>
<hr>
</details>

<details>
<summary>
How do you check for changes in a database?
</summary>
<hr>
</details>

<details>
<summary>
Many questions from my CV (all practical, not just asking what you have done).
</summary>
<hr>
</details>

<details>
<summary>
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
</summary>
<hr>

[**💻 Submit Code**](https://leetcode.com/problems/move-zeroes/description/)
```C++
void moveZeroes(vector<int>& nums) {
    int i = 0;
    for(int j=0;j<nums.size();j++){
        swap(nums[i], nums[j]);
        if( nums[i] != 0 ) i++;
    }
}
```
</details>


## Contributors
1. [Salman Farsi](https://www.linkedin.com/in/salmanfarsi0/)