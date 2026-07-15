bizde bir [[array]] var , ve bu arrayda hansisa bir operationu.
[ Tərs Çevirmə](https://eolymp.com/az/problems/2098):
meselen bizde bir array var ve bunu tersine cixisa vermeliyik.
burada 1 pointer besdir.O pointeri sagdan basladib, sola qeder azaldiriq , ve indi olduqu indeksi cixisa veririk. Belelikle arrayimiz tersine cevrilir.

l -> n - 1;
```cpp
int a[n];
while(l >= 0) {
	cout << a[l];
	l--;
}
```


 [ Kart Oyunları](https://eolymp.com/en/problems/11387) :
Huseyn and Yaroslav are playing a card game. There are n cards laid out in a row on the table, each with a different number written on it. The players take turns. Huseyn starts the game. On each turn, a player can take either the leftmost or the rightmost card. The player will always choose the card with the highest number. The game ends when there are no cards left on the table. Find the sum of the numbers on the cards collected by Huseyn and Yaroslav at the end of the game.

Input. The first line contains the number of cards n (1≤n≤10000) on the table. The second line contains n positive integers, each indicating the number on a card. All numbers are not greater than 109.

Output. Print the sum of the numbers on the cards collected by Huseyn and Yaroslav at the end of the game.

Sample input:

```text
7
4 7 5 1 12 8 2
```


Sample output:
```cpp
18 21
```
l->0
r-> n - 1
```cpp
l = 0;
r = n - 1;
tour = 0;
int ans[2];
ans[0] = ans[1] = 0;
while(l <= r) {
	if(tour == 0) {
		if(a[l] > a[r]) {
			ans[0] += a[l];
			l++;
		} else {
			ans[0] += a[r];
			r--;
		}
	} else {
		if(a[l] > a[r]) {
			ans[1] += a[l];
			l++;
		} else {
			ans[1] += a[r];
			r--;
		}
	}
}
```