#datastructs/fenwicktree 

Binary tree de deyilir.

[[Range queries]] ucun isdifade edeciyik ve [[SegmentTree]] kimi $4 * N$ qeder memory isdifade elemirik, $N + 10$ memory isdifade edirik.

[Cp Algo](https://cp-algorithms.com/data_structures/fenwick.html)

Mentiq olaraq ededlerin binary yazilisindaki her biri ferqli bir range ni gorsedir.

consttanti cox yaxsi olduqu ucun texminen $O(1)$ sayilir, amma 
$$upd: log_n$$$$get:log_n$$ amma ancaq *prefix range*leri saxlaya bilir deye , max , min kimi operasiyalar isdifade oluna *bilmir*.

```cpp
struct BIT {
	int N;
	vector < int > t;
	
	BIT(_n) {
		N = _n;
		t.resize(N + 10);
	}
	
	void update(int pos , int val) {
		while(pos < N) {
			t[pos] += val;
			pos += (pos & (-pos)); 
		}
	}
	
	int query(int l , int r) {
		if(l != 1) {
			return query(1 , r) - query(1 , l - 1);
		}
		
		int res = 0;
		while(r > 0) {
			res += t[r];
			r -= (r & (-r));
		}
		
		return res;
	}
};
```

  