Depth First Search

#graphs/dfs 

Her hansısa bir nodedən başlayıb bütün used olmayan qonşularına gedib oradaki subtree ni bitirəndən sonra geri qayıdır , ve tebiki bir [[node]]-nin [[subtree]]-sini bitirmemis basqa bir [[node]]-ye kecmir

Time: O(n log(m)) -ə işləyir.

dfs snippetim:
```cpp
void dfs(int v) {
    used[v] = true;
    for(int &to : g[v]) {
        if(!used[to])
            dfs(to);
    }
}
```

ilk olaraq bir [[node]] ye girende ona birde girmemek ucun `used = true` edir.
sonra butun qonsularina baxib evvelceden `used` olmayan nodelere gedir.

parantle olan dfs snippetim:

```cpp
void dfs(int v , int pa = -1) {
	for(auto &to : g[v]) {        // NOTE: auto->hansi type olacaqini deyir
		if(to == pa)
			continue;
		dfs(to , v);
	}
}
```

DFS qrafda bir cox ferqli funksiya yerine yetire ve komek ede biler.
[(en) video tutorial](https://www.youtube.com/watch?v=7fujbpJ0LB4)