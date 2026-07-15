# DFS-də Euler Tour

## Giriş

Euler Tour ağacı DFS vasitəsilə xətti massivə çevirmək üsuludur. Bu üsul subtree sorğuları, LCA və digər ağac alqoritmlərində geniş istifadə olunur.

---

## Base

DFS zamanı hər düyün üçün iki məlumat saxlanıla bilər:

- `tin[v]` — düyünə ilk dəfə daxil olma anı.
- `tout[v]` — düyündən çıxma anı.

Nümunə:

```text
        1
      / | \
     2  3  4
       / \
      5   6
```

DFS sırası:

```text
1 → 2 → 3 → 5 → 6 → 4
```

---

## 1. In Time (`tin`)

```cpp
int timer = 0;
vector<int> tin(n + 1);

void dfs(int v, int p){
    tin[v] = timer++;

    for(int u : adj[v]){
        if(u == p) continue;
        dfs(u, v);
    }
}
```

Nəticə:

| Düyün | tin |
|------:|----:|
|1|0|
|2|1|
|3|2|
|5|3|
|6|4|
|4|5|

---

## 2. Out Time (`tout`)

```cpp
int timer = 0;

void dfs(int v, int p){
    tin[v] = timer++;

    for(int u : adj[v]){
        if(u == p) continue;
        dfs(u, v);
    }

    tout[v] = timer++;
}
```

---

## 3. Ancestor yoxlaması

`a` nodu `b`-nin ancestor-udur, əgər

```text
tin[a] <= tin[b] && tout[b] <= tout[a]
```

Cod:

```cpp
bool isAncestor(int a, int b){
    return tin[a] <= tin[b] && tout[b] <= tout[a];
}
```

Vaxt mürəkkəbliyi: **O(1)**.

---

## 4. Euler Tour (yalnız giriş)

Subtree sorğuları üçün ən vacib variantdır.

```cpp
vector<int> euler;

void dfs(int v, int p){
    tin[v] = euler.size();
    euler.push_back(v);

    for(int u : adj[v]){
        if(u == p) continue;
        dfs(u, v);
    }

    tout[v] = euler.size() - 1;
}
```

Euler massivi:

```text
1 2 3 5 6 4
```

Ən vacib xüsusiyyət:

Subtree həmişə massivdə bir intervaldır.

Məsələn:

```text
Subtree(3) = 3 5 6
```

Massivdə:

```text
[tin[3], tout[3]]
```

---

## 5. Subtree Sum

```cpp
vector<int> flat;

void dfs(int v, int p){
    tin[v] = flat.size();
    flat.push_back(value[v]);

    for(int u : adj[v]){
        if(u == p) continue;
        dfs(u, v);
    }

    tout[v] = flat.size() - 1;
}
```

Artıq:

```text
Subtree(v) = sum(tin[v], tout[v])
```

Bu sorğunu Segment Tree və ya Fenwick Tree ilə `O(log N)` vaxtda cavablandırmaq olar.

---

## 6. Subtree Update

Bütün subtree-yə `+x` əlavə etmək:

```text
update(tin[v], tout[v], x)
```

---

## 7. Euler Tour (giriş + çıxış)

```cpp
vector<int> euler;

void dfs(int v, int p){
    euler.push_back(v);

    for(int u : adj[v]){
        if(u == p) continue;
        dfs(u, v);
    }

    euler.push_back(v);
}
```

Nəticə:

```text
1 2 2 3 5 5 6 6 3 4 4 1
```

Bu variant əsasən LCA və Mo on Trees üçün istifadə olunur.

---

## 8. LCA üçün Euler Tour

```cpp
vector<int> euler;
vector<int> depth;
int first[N];

void dfs(int v, int p, int d){
    first[v] = euler.size();

    euler.push_back(v);
    depth.push_back(d);

    for(int u : adj[v]){
        if(u == p) continue;
        dfs(u, v, d + 1);

        euler.push_back(v);
        depth.push_back(d);
    }
}
```

Sonra RMQ ilə LCA hesablamaq mümkündür.

---

## Vaxt mürəkkəbliyi

- DFS: **O(N)**
- Subtree sorğusu (Fenwick/Segment Tree): **O(log N)**
- Ancestor yoxlaması: **O(1)**

---

## Xülasə

| Variant | İstifadə |
|---------|----------|
| tin/tout | Ancestor yoxlama |
| Euler Tour (N element) | Subtree Query və Update |
| Euler Tour (2N element) | LCA, RMQ, Mo on Trees |

**Yadda saxla:** Euler Tour-un əsas məqsədi ağacı massivə çevirməkdir ki, ağac üzərindəki bir çox problemi massiv alqoritmləri ilə həll etmək mümkün olsun.
