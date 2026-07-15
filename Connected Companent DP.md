---
id: Connected Companent DP
aliases: []
tags: []
---
#dp 
Biz bunu xususi permutasiyalarin sayi kimi hesablaya bilerik yani hansisa sertlere emel eden permutasiyalari saymaq.

Men burada asand olsun deye o(n!) i nece bununla hesablamaq olacaqini gorsedecem.

ilk oncelikle
```cpp
T dp[i][j];
```
qururuq , i nece elementi secdiyimiz , j nece dene [[companent]] olduqudur.

indi burada ele bir bizim bir qrafimiz var ve biz 1 den n e ededleri insert edirik.

ededleri insert edende 3 sey ola biler:
1. yeni bir [[companent]] yarada.
```cpp
	dp[i][j] += dp[i - 1][j - 1] * (j);
	```
2. [[companent]]lere birlese.
```cpp
	dp[i][j] += dp[i - 1][j] * (2 * j); 
```
1. 2 [[companent]]i birlesdire.  
```cpp
	dp[i][j] += dp[i - 1][j + 1] * (j);
	```
bu [[dp]] ni yazdiqdan sonra n! i hesablaya bilersiniz.

Biraz cetin mesele - [[Kangaroo]].

```cpp
for(int i = 1; i <= n; i++) {
	for(int j = 1; j <= i; j++) {
		// edge case leri duzeltmek lazimdir mes. i = 1
		dp[i][j] += dp[i - 1][j - 1] * (j);
		dp[i][j] += dp[i - 1][j] * (2 * j); 
		dp[i][j] += dp[i - 1][j + 1] * (j);
	}
}
```
