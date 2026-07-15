[Youtube Tut](https://www.youtube.com/watch?v=-StmrE2gY44) 

Problem:
1) Add line $a \cdot x + b$
2) Evaluate $\max(a\cdot x + b)$
with time complexity: $O(\log m)$, $m$ = $\max X$ or at offline with compress you can make it $\log n$ or with dynamic *Li chao tree* you can amortized $\log n$ 

Benefits:
1) Can e made persistent
2) Faster than dynamic [[Convex Hull(Dp)]] in practice


Li Chao tree = Dynamic [[SegmentTree]] with a line in each node
![[Pasted image 20260507204028.png]]

We want to: Candidates for answer to query are the nodes on the path from the root to leaf for the interval$(x, x)$

for query:
1) $ans = \max(ans, L.col(x))$
2) if (mid >= x) go left
3) else go right

![[Pasted image 20260507204346.png]]

for addition:

Case 1:
Main idea here, imagine we have in_tree(which is line in current node)
if at **mid** the line that we are adding is greater than in_tree then we must **swap** them(add will be previus intree line and intree  will be previeus add line) and continue with cases below
We doing it to be sure at mid add is greater so at L or R we can not go there
![[Pasted image 20260507204444.png]]

Case 3:
At here we don't need to go left because at left our in_tree is always greater than add, so we only go to right(recurcivly) 
![[Pasted image 20260507204824.png]]

Case 4:
We can say add is always smaller at right than in_tree so we don't need to go right
![[Pasted image 20260507205058.png]]

other cases: if we add this our time complexity will decrease 
if one line is always greater we don't need to continue recursion at all(add is greater at mid so we will swap them then we will stop recursion)
![[Pasted image 20260507205201.png]]

Basicly we are adding left or right so we will only have $\log n$  recursions 

Code:
![[Pasted image 20260507205525.png]]

snippet:
```cpp
struct LiChaoTree {
    struct Line {
        ll k, c;
        Line(ll k = 0, ll c = INFll) : k(k), c(c) {}
        ll get(ll x) {
            i128 prod = k * x + c;
            if(prod > INFll)
                return INFll;
            if(prod < -INFll)
                return -INFll;
            return k * x + c;
        }
    };

    struct Node {
        Line L;
        pair<int, int> interval;
        Node *l, *r;
        Node(Line V, ll l, ll r) : L(V), interval(make_pair(l, r)), l(nullptr), r(nullptr) {}
    };

    ll _L , _R;

    Node* root;

    LiChaoTree (ll l = -INFi , ll r = INFi) {
        _L = l;
        _R = r;
        root = new Node(Line() , l , r);
    }

    ll ask(Node* v, ll x) {
        if (v == nullptr)
            return INFll;  // WARNING: Null vali deyismek lazim ola biler...
        auto [l, r] = (v)->interval;
        if (l == r)
            return v->L.get(x);
        ll mid = (l + r) >> 1LL;
        if (x <= mid) {
            return min(ask(v->l, x), v->L.get(x));
        } else {
            return min(ask(v->r, x), v->L.get(x));
        }
    }

    Node* add(Node* v, Line L, ll _l, ll _r) {
        if (v == nullptr)
            return new Node(L, _l, _r);
        auto [l, r] = v->interval;
        ll mid = (l + r) >> 1LL;
        if (L.get(mid) < v->L.get(mid))
            swap(v->L, L);
        if(L.get(l) > v->L.get(l) && L.get(r) > v->L.get(r))
            return v;
        if (L.get(l) < v->L.get(l)) {  // WARNING: Min ucun duzdur...
            v->l = add(v->l, L, _l, mid);
        } else {
            v->r = add(v->r, L, mid + 1, _r);
        }
        return v;
    }

    ll query(ll x) {
        return ask(root , x);
    }

    void ins(ll k , ll c) {
        root = add(root, Line(k , c), _L, _R);
    }
};



```

[[Li Chao Tree -problems]]