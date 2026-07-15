#pointers

Pointerlər elə bir tip dirki başqa bir tipin yerini saxlayır.
& ile adress-of edirik
(ulduz) ile deference edirik

```cpp
#include<iostream>

int main() {
	std::string name = "Bro";
	std::string FreePizzas[5] = {"pizza1" , "pizza2" , "pizza3" , "pizza4" , "pizza5"}
	std::string *pName = &name;
	std::cout << *pName;
	int age = 21;
	int *pAge = &age;
	std::string *pFreePizzas = FreePizzas;
	cout << FreePizzas;
}
```

