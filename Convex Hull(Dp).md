[Video1AZ](https://www.youtube.com/watch?v=fy0Zghco4qMhttps://www.youtube.com/watch?v=fy0Zghco4qM)
[video2](https://www.youtube.com/watch?v=HnZKQJtGeHs)

[[convex-hull]](cp algo /geomety)

Convex hulli bu zaman isdifade ede bilerikki:
$y = k * x + d$ olsun

[[Convex Hull Dp -problems]] $<--$ baxib anlaya bilersiniz

[[Kalila and Dimna in the Logging Industry]] - DP + convex hull

Snippet:

```cpp
struct CHT {
    struct line {
        int k , b;
        line(int k , int b) : k(k) , b(b) {} 
        int f(int x) {
            return x * k + b;
        }
        db col2(line a) {
            return db(a.b - b) / (a.k - k); 
        }
        int col(line a) {
            return (a.b - b + k - a.k - 1) / (k - a.k);
        }
    };
    
    deque< pair< line , int > > dq;
    
    void insert(int k , int b) {
        line l(k , b);
        while (dq.size() > 1 && dq.back().second >= dq.back().first.col(l)) {
            dq.pop_back();
        }
        if(dq.empty()) {
            dq.emplace_back(l , 0);
            return;
        }
        dq.emplace_back(l , dq.back().first.col(l));
    }

    int query(int x) {
        while (dq.size() > 1) {
            if(dq[1].second <= x)
                dq.pop_front();
            else 
                break;
        }
        return dq[0].first.f(x);
    }
};
```

Snippet2:

```cpp
struct Line { mutable ll k, m, p; bool operator<(const Line& o) const { return k < o.k; } bool operator<(ll x) const { return p < x; } }; struct LineContainer : multiset<Line, less<>> { // (for doubles, use inf = 1/.0, div(a,b) = a/b) static const ll inf = LLONG_MAX; ll div(ll a, ll b) { // floored division return a / b - ((a ^ b) < 0 && a % b); } bool isect(iterator x, iterator y) { if (y == end()) return x->p = inf, 0; if (x->k == y->k) x->p = x->m > y->m ? inf : -inf; else x->p = div(y->m - x->m, x->k - y->k); return x->p >= y->p; } void add(ll k, ll m) { auto z = insert({k, m, 0}), y = z++, x = y; while (isect(y, z)) z = erase(z); if (x != begin() && isect(--x, y)) isect(x, y = erase(y)); while ((y = x) != begin() && (--x)->p >= y->p) isect(x, erase(y)); } ll query(ll x) { assert(!empty()); auto l = *lower_bound(x); return l.k * x + l.m; } };
```