# Two Pointers (İki Göstərici)

## Two Pointers nədir?

**Two Pointers (İki Göstərici)** massivlər (array), sətirlər (string) və digər ardıcıl verilənlər strukturlarında istifadə olunan sadə və çox faydalı bir alqoritmik texnikadır.

Bu üsulda bir indeks əvəzinə **iki indeks (pointer)** istifadə olunur.

Adətən:

- `l` (**left**) — massivin əvvəlindən başlayır.
    
- `r` (**right**) — massivin sonundan başlayır.
    

```text
Massiv:

İndeks:  0   1   2   3   4
Dəyər:  [3] [7] [1] [9] [5]
         ^               ^
         l               r
```

Problemə görə bu göstəricilər:

- Bir-birinə doğru hərəkət edə bilər.
    
- Eyni istiqamətdə hərəkət edə bilər.
    
- Bəzən biri sabit qalarkən digəri hərəkət edə bilər.
    

Məqsəd massivi mümkün qədər sürətli emal etməkdir. Əksər hallarda bu üsulun mürəkkəbliyi **O(n)** olur.

---

# Nümunə 1 — [Massivi tərsinə çap etmək](https://eolymp.com/az/problems/2098)

**Məsələ:**

Bizə bir massiv verilir. Massivin elementlərini **tərs ardıcıllıqla** ekrana çıxarmaq lazımdır.

Məsələn:

```text
Giriş:
1 2 3 4 5

Çıxış:
5 4 3 2 1
```

Bu məsələ üçün **iki pointer lazım deyil**, yalnız **bir pointer** kifayətdir.

Pointer-i massivin sonundan başlayırıq (`n - 1`) və sola doğru hərəkət etdiririk.

```cpp
int l = n - 1;

while (l >= 0) {
    cout << a[l] << " ";
    l--;
}
```

### Necə işləyir?

```text
1 2 3 4 5
        ^
        l

5 çap olunur.

1 2 3 4 5
      ^
      l

4 çap olunur.

1 2 3 4 5
    ^
    l

3 çap olunur.

...
```

Bu nümunədə yalnız bir pointer istifadə olunsa da, pointer-lərin massiv daxilində necə hərəkət etdiyini başa düşmək üçün yaxşı başlanğıcdır.

---

# Nümunə 2 — [Kart Oyunu](https://eolymp.com/en/problems/11387)

**Məsələ:**

Hüseyn və Yaroslav kart oyunu oynayırlar.

- Kartlar bir sırada düzülüb.
    
- Hər gedişdə oyunçu **ya ən soldakı**, ya da **ən sağdakı** kartı götürə bilər.
    
- Oyunçu həmişə bu iki kartdan **böyük olanı** seçir.
    
- Oyuna Hüseyn başlayır.
    

Sonda hər iki oyunçunun topladığı xalları tapın.

Nümunə:

```text
Giriş

7
4 7 5 1 12 8 2
```

Başlanğıc vəziyyəti:

```text
4 7 5 1 12 8 2
^             ^
l             r
```

Hüseyn müqayisə edir:

- Sol kart = 4
    
- Sağ kart = 2
    

Böyük olan **4**-dür. Ona görə 4-ü götürür.

```text
7 5 1 12 8 2
^          ^
l          r
```

Sonra növbə Yaroslava keçir.

Yaroslav müqayisə edir:

- Sol kart = 7
    
- Sağ kart = 2
    

Böyük olan **7**-dir. O da 7-ni götürür.

Bu proses bütün kartlar bitənə qədər davam edir.

---

## Alqoritm

1. `l = 0`
    
2. `r = n - 1`
    
3. `l <= r` olduğu müddətdə:
    
    - `a[l]` və `a[r]` müqayisə edilir.
        
    - Böyük olan kart götürülür.
        
    - Hansı kart götürülübsə, həmin pointer bir addım hərəkət edir.
        
    - Növbə digər oyunçuya keçir.
        

---

## Kod

```cpp
int l = 0;
int r = n - 1;

int turn = 0;          // 0 = Hüseyn, 1 = Yaroslav
long long ans[2] = {0, 0};

while (l <= r) {

    if (a[l] > a[r]) {
        ans[turn] += a[l];
        l++;
    } else {
        ans[turn] += a[r];
        r--;
    }

    turn ^= 1; // Növbəni dəyiş
}

cout << ans[0] << " " << ans[1];
```

---

## Vizual izah

```text
4 7 5 1 12 8 2
^             ^

4 və 2 müqayisə edilir.

4 böyükdür.

4 götürülür.

↓

7 5 1 12 8 2
^          ^
```

Sonra:

```text
12 8 2
^    ^

12 və 2 müqayisə edilir.

12 götürülür.

↓

8 2
^ ^
```

Pointer-lər hər dəfə bir-birinə yaxınlaşır və sonda `l > r` olduqda alqoritm bitir.

---

# Two Pointers nə vaxt istifadə olunur?

Bu texnikadan əsasən aşağıdakı hallarda istifadə edilir:

- Massivin əvvəlini və sonunu eyni anda yoxlamaq lazım olduqda.
    
- İki elementi müqayisə etmək lazım olduqda.
    
- Massivi bir dəfə gəzərək (`O(n)`) məsələni həll etmək mümkün olduqda.
    

Ən çox rast gəlinən məsələlər:

- Massivi tərsinə çap etmək
    
- Palindrom yoxlamaq
    
- Sorted massivdə iki ədədin cəmini tapmaq (Two Sum)
    
- Sorted massivdə təkrarlanan elementləri silmək
    
- Container With Most Water
    
- Kart seçmə tipli məsələlər
    

---

# Yadda saxla

- Dövr şərtini düzgün yaz (`l <= r` və ya `l < r`).
    
- Hansı pointer-in hərəkət etməli olduğuna diqqət et.
    
- Əgər məsələ çətin görünürsə, massivi kağız üzərində çək və pointer-ləri addım-addım hərəkət etdir.
    
- Hər addımda özünə bu sualları ver:
    
    - **`l` irəli getməlidir?**
        
    - **Yoxsa `r` geri gəlməlidir?**
        

Bu texnikanı yaxşı öyrəndikdən sonra massivlə bağlı bir çox məsələləri daha rahat və daha sürətli həll edə biləcəksən.