---
layout: post
title:  "[資料結構] Performance Analysis & Complexity"
date:   2022-02-14 22:00:00 +0800
categories: 資料結構
tags: complexity Recursion 筆記
pin: false
---
## 前言
演算法的目的在於改善一個東西或問題，並在從問題中找出現有最好的辦法

一個好的演算法可以節省許多時間與記憶體空間，而一個程式在執行時所佔用的記憶體空間也會反映出執行所需要的時間

因此才需要效能分析 ( Performance Analysis ) ，但其實也不用要求的非常精準，只需要一個最後結果可符合需求且大家都能夠接受的就行了

## 效能分析 ( Performance Analysis )

因為每一隻程式在不同硬體設備上執行所花的時間都不同，但演算法不是只適用於一台特定的硬體設備

因此分析方法必須是不受電腦設備、程式語言、程式設計者，以及實作上的細節影響

但我們可以從這個分析結論得知這個演算法效率如何

其中分析方法就是 Complexity Theory，也是目前比較普遍的方法

## 複雜度理論 ( Complexity Theory ) 

在 Complexity Theory 中，分成 **時間複雜度(Time Complexity)** 與 **空間複雜度(Space Complexity)**

一般 Complexity 表示使用漸近式符號 ( Asymptotic Notation ) 

目的是為了表現時間或空間函數的成長趨勢，種類有：

* Big-oh：O
* Omega：Ω
* Theta：Θ
* little-oh：o
* little-omega：ω

以及常見的複雜度 groth rate 等級 ( 由小到大 )：

| 小| 常數 (constant) 時間 | Ｏ(1) | 
| ↓| 雙重對數 (doubly log) 時間 | Ｏ(log log n) | 
| ↓| 對數 (log) 時間 | Ｏ(log n) | 
| ↓| 線性 (linear) 時間 | Ｏ(n) | 
| ↓| n log n 時間 | Ｏ(n log n) | 
| ↓| 多項式 (polynomial) 時間 | Ｏ($n^a$), a ∈ $R^+$ | 
| ↓| 指數 (exponential) 時間 | Ｏ($2^n$) | 
| 大| 階層 (Factorial) 時間 | Ｏ(n!) | 

![](https://i.imgur.com/CUpCW1x.png)

[圖片來源](https://www.google.com/search?q=big+o+complexity&rlz=1C1CHBF_zh-TWTW921TW921&sxsrf=APq-WBtLjXbFCwD2UFKEu4HIn2H9w0_bmQ:1645104671750&source=lnms&tbm=isch&sa=X&ved=2ahUKEwiguM-87Ib2AhUcrlYBHQ8iCasQ_AUoAXoECAEQAw&biw=1920&bih=937&dpr=1#imgrc=eDClsXUtsfsYVM)

---

## 漸近式符號定義 ( Asymptotic Notation Definition)

### ☆ Big-oh：O

#### Def：f(n) = O(g(n)) 存在兩個正整數 C，$n_0$，滿足 f(n) ≤ C·g(n)，Ɐ n ≥ $n_0$

> Big-oh 描述函式的上界 ( upper-bound )
{: .prompt-tip }

例：f(n) = 5$n^2$+8n-9，則f(n) = O($n^2$)

>   因為可以找到兩個正常數，C = 6，$n_0$ = 7
>
>   使5$n^2$+8n-9 ≤ C·$n^2$，Ɐ n ≥ $n_0$
>
>   f(n) = O($n^2$)，取 C = 6
>
>   5$n^2$+8n-9 ≤ 6$n^2$
>
>   n^2-8n+9 ≥ 0
>   n ≥ 7，所以$n_0$ = 7

### ☆ Omega：Ω

#### Def：f(n) = Ω(g(n)) 存在兩個正整數 C，$n_0$，滿足 f(n) ≥ C·g(n)，Ɐ n ≥ $n_0$

> Omega 描述函式的下界 ( lower-bound )
{: .prompt-tip }

例：f(n) = 4$n^2$-8n-9，則f(n) = Ω($n^2$)

>   因為可以找到兩個正常數，C = 4，$n_0$ = 9/8
>
>   使4$n^2$-8n-9 ≥ 4$n^2$
>
>   8n ≥ 9，所以$n_0$ = 9/8

### ☆ Theta：Θ

#### Def：f(n) = Θ(g(n)) 存在兩個正整數 $C_1$，$C_2$，滿足 $C_1$·g(n) ≤ f(n) ≤ $C_2$·g(n)，Ɐ n ≥ $n_0$

> Theta 描述函式的邊界 ( bound )
{: .prompt-tip }

例：f(n) = 4$n^2$+8n-9，f(n) = Θ($n^2$)

>   因為可以找到3個正常數，$C_1$ = 4，$C_2$ = 5，$n_0$ = 9
>
>   使$C_1$·$n^2$ ≤ f(n) ≤ $C_2$·$n^2$，Ɐ n ≥ $n_0$
>
>   取$C_1$=4，4$n^2$+8n-9 ≤ 4$n^2$，n ≥ 9/8
>
>   取$C_2$=5，4$n^2$+8n-9 ≤ 5$n^2$，$n^2$-8n+9 ≤ 0，(n-9)(n+1) ≥ 0，n ≥ 9

### little-oh：o

#### Def：f(n) = o(g(n)) 對於所有正整數 C 存在一個 $n_0$，使得 f(n) < C·g(n)，Ɐ n ≥ $n_0$

例1：f(n) = 5n = o(n)

> 5n < C·n，Ɐ C 皆要成立
>
> 但 C = 5，5n ≮  5n ⇒ False

例2：f(n) = 5n = o($n^2$)

> True

### little-omega：ω

#### Def：f(n) = ω(g(n)) 對於所有正整數 C 存在一個 $n_0$，使得 f(n) > C·g(n)，Ɐ n ≥ $n_0$

例1：f(n) = 5n = ω(n)

> 因為 5n > C·n，Ɐ C
>
> 取 C = 5 ⇒ 5n ≯  5n ⇒ False

例2：f(n) = 5n = ω(1)

> True

## 遞迴時間函式 (Recursion Time Function)

一般求解 Recursion Time Function 常見做法有幾種：

(1) 迭代法

(2) Master Theorem / Extended Master Theorem

> 求解 Recursion Time Function 還可以用 Recursion Tree 的作法來猜測近似解
{: .prompt-tip }

### 迭代法

例1：T(n) = 2T(n-1)+1，T(1)=1，求T(n)=？ O(?)

> T(n) = 2T(n-1)+1
>
>   = 2T(n-1)+1
>
>   = 4T(n-1)+1+2
>
>   = 4[2T(n-3)+1]+1+2
>
>   = 8T(n-3)+1+2+4
>
>   = ...
>
>   = $2^{n-1}$T(n-(n-1))+$2^{n-1}$-1
>
>   = $2^n-1$
>
>   T(n) = $2^n$-1，O($2^n$)

例2：T(n) = T(n-1)+n，T(0)=0，求T(n)=？ O(?)

> T(n) = T(n-1)+n
>
>   = T(n-2)+(n-1)+n
>
>   = T(n-3)+(n-2)+(n-1)+n
>
>   = ...
>
>   = T(n-n)+n+n-1+...+1
>
>   = T(0)+((n+1)n)/2
>
>   = ($n^2$+n)/2
>
>   T(n)=($n^2$+n)/2，O($n^2$)

### Master Theorem

在演算法中稱 **主定理**，若 T(n) = aT(n/b)+f(n)，其中 a ≥ 1，b ≥ 1，f(n) 是正成長函式，則可以使用 Master Theorem 來計算決定 T(n) = Θ(?)

使用方法：

Step 1. 先求出 $n^{log_ba}$

Step 2. $n^{log_ba}$ 與 f(n) 比較 groth rate，分成 3 個 case：

- case 1：若f(n) = $O(n^{log_ba-ξ})$，ξ 為 > 0 之正常數，則 T(n) = $Θ(n^{log_ba})$
- case 2：若f(n) = $Θ(n^{log_ba})$，則 T(n) = $Θ(n^{log_ba}·logn)$
- case 3：若f(n) = Ω$(n^{log_ba+ξ})$，ξ 為 > 0 之正常數，且 $a$f(n/$b$) ≤ C·f(n)，C 為 < 1 之正常數，則 T(n) = Θ(f(n))

> 通常大多問題帶這個 Master Theorem 公式就可以直接求解，神一般好用，但切記別用得太爽www，有些情況下會誤用，如下
{: .prompt-danger }

例：T(n)=2T(n/2)+nlogn

> 【誤用示範】
>
> a=2，b=2，f(n)=nlogn
>
> 而 $n^{log_ba}$ = $n^1$ = n
>
> Case 3 ⇒ T(n) = Θ(f(n)) = Θ(nlogn) = O(nlogn)

原因：

> f(n) = $Ω(n^{log_ba+ξ})$，ξ 為正常數
>
> ⇒ f(n) = nlogn = $Ω(n^{1+ξ})$，ξ 為正常數，但 ξ 找不到
>
> nlogn ≥ C·$(n^{1+ξ})$
>
> nlogn ≥ C·n·$n^3$，ξ > 0 常數
>
> 所以無法使用

**正解：$Θ(n{log^2}n)$ = $Θ(n．{(logn)^2})$**

### Extended Master Theorem

Master Theorem 還有一個強化版本，稱 Extended Master Theorem，使用條件如下：

若 T(n) = $a$T($a$/$b$) + f(n) 且 $f(n)/n^{log_ba}$ = $log^kn$，k ≥ 0 之常數 ( 或 f(n) = $n^{log_ba}$·$log^kn$  )

則 T(n) = Θ( $n^{log_ba}$ · $log^{k+1}n$)

##### 以上皆為自己整理的筆記，僅供參考與複習使用。