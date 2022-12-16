---
layout: post
title:  "[演算法] Dynamic Programming"
date:  2022-05-05 22:00:00 +0800
categories: 演算法
tags: 筆記 DP Recursion
pin: false
---
## 動態規劃 (Dynamic Programming)，簡稱DP

屬於 Divide-and-conquer 的延伸，和 Divide-and-conquer 同樣是藉由 combining the solutions to subproblems。

Dynamic Programming 主要可以將原問題分解為相較簡單的子問題，再通過子問題的解求出複雜問題的方法。

其核心可以說是 **記憶化儲存**，每當子問題的答案被算出來時，同時將答案儲存在記憶體中，以便下次需要時可以直接透過查表的方式得出解，並從而減少計算量。

以著名的 Fibonacci 為例

---

## Fibonacci Number

![](https://i.imgur.com/gy3sYKG.png)

簡單的說就是 從第一次等於0，第二次等於1開始，下一個數字等於前兩個數字的相加，以此類推...

| -------- |
| f(0)=0 | 
| f(1)=1 | 
| f(2)=0+1=1| 
| f(3)=1+1=2 | 
| f(4)=1+2=3 | 
| f(5)=2+3=5 | 
| f(6)=3+5=8 | 
| ... |

所以得出函式 F(n) = F(n-1) + F(n-2)

---

### Recursion

如果用遞迴來寫的話，Function 會像這樣：

```c++
int Fib(int n){
    if(n < 2) return n;
    return Fib(n-1) + Fib(n-2); 
}
int main(){
    cout << Fib(n) << endl;
    return 0;
}
```
雖然在演算法設計上十分直覺，但執行效率不佳，以 n = 5 為例的話 Recursion Tree 畫出來會長這樣：

![](https://i.imgur.com/LI2xydn.png)

其時間複雜度 $T(n)$ = $O(2^n)$，可以發現用遞迴解容易產生多個 overlapping subproblem，光 $F(2)$ 就被呼叫了3次，如果 n 更大的話呢？有沒有可能讓記憶體超出負荷？

---

### Dynamic Programming

如果換用 Dynamic Programming 的話，有兩種作法：

- Top-down：Recursion，執行由上到下，較慢，可能有深層遞迴
- Bottom-up：for loop，執行由下到上，較快，有漏掉 subproblems 沒解決的可能

但通常到最後多數情況都會使用 Bottom-up 作法比較多

Bottom-up：

```c++
long long Fib(long long n){
    long long D[n+1];
    D[0] = 0;
    D[1] = 1;
    for(int i=2; i < n+1; i++){
        D[i] = D[i-1] + D[i-2];
    }
    return D[n];
}
int main(){
    cout << Fib(n) << endl;
    return 0;
}
```
透過 D[n] 將所有的 subproblems 儲存，當再次碰到重複的 subproblems 就可以透過先前儲存的答案查表得出。 

![](https://i.imgur.com/WuqUDxF.png)

所以其實有點像是用空間換取時間的概念，時間複雜度為 $T(n)$ = $O(n)$。

跟遞迴的 $O(2^n)$ 效率是差很多的，但在讀寫上遞迴就是比較直覺，但換來的就是效率差，還有除錯的時候會很頭痛，要一直追遞迴...

---

## 總結

前面講到 Dynamic Programming 算是 Divide-and-conquer 的延伸，也具有相同的概念。

至於使用時機：

- Divide-and-conquer：independent or disjoint subproblems
- Dynamic Programming：overlapping subproblems

當一個問題具有 optimal substructure 性質時，或許以遞迴的方式可以得出結果，但易產生許多 overlapping subproblems。

以 bottom-up 方式解開所有 subproblems 並儲存，以便建構出原問題之解，就是 Dynamic Programming。

##### 參考來源

[費波那契數 - 維基百科](https://zh.m.wikipedia.org/zh-tw/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0)

##### 以上皆為自己整理的筆記，僅供參考與複習使用。