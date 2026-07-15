
IFFT = interpration.


Burada iki dene tenlikin hasilini fft ile tapmaq gosterilib.



```cpp
#include <complex>
typedef complex<duoble> cmpl;

const double PI = atan2(0 , -1);

vector<cmpl> fft(vector<cmpl> P) {
	int n = P.size();
	if(n == 1) {
		return P;
	}
	vector<cmpl> P_even(n / 2) , P_odd(n / 2);
	for(int j = 0;j < n / 2;j++) {
		P_even[j] = P[j * 2];
		P_odd[j]  = P[j * 2 + 1];
	}
	vector<cmpl> val_even = fft(P_even);
	vector<cmpl> val_odd  = fft(P_odd);
	vector<cmpl> val(n);
	for(int j = 0;j < n / 2;j++) {
		cmpl wj(cos(2 * PI * j / n) , sin(2 * PI * j / n));
		val[j] = val_even[j] + wj * val_odd[j];
		val[j + n / 2] = val_even[j] - wj * val_odd[j];
	}
	return val;
}

```



conj e vurmaq bolmek demekdir , inverse kimi;
Inverse FFT:
```cpp

vector<cmpl> inverse_fft(vector<cmpl> val_P) {
	int n = val_P.size();
	if(n == 1) {
		return val_P:
	}
	vector<cmpl> val_even(n / 2) , val_odd(n / 2);
	for(int j = 0;j < n / 2;j++) {
		cmpl wj(cos(2 * PI * j / n) , sin(2 * PI * j / n));
		val_even[j] = (val_P[j] + val_P[j + n / 2]) / 2;
		val_odd[j]  = (val_P[j] - val_P[j + n / 2]) / 2 * conj(wj);
	}

	vector<cmpl> P_even = inverse_fft(val_evem);
	vector<cmpl> P_odd = inverse_fft(val_odd);
	vector<cmpl> P(n);
	for(int j = 0;j < n;j++) {
		P[2 * j] = P_even[j];
		P[2 * j + 1] = P_odd[j];
	}
	return P;
}

```


ve hasili:
```cpp
vector<ll> multiply(vector<int> P , vector<int> Q) {
	int n = 1;
	while(n < P.size() + Q.size() - 1) {
		n *= 2;
	}
	vector<cmpl> P_cmpl(n) , Q_cmpl(n);
	copy(P.begin() , P.end() , P_cmpl.begin());
	copy(Q.begin() , Q.end() , Q_cmpl.begin());
	vector<cmpl> Q_val = fft(Q_cmpl);
	vector<cmpl> P_val = fft(P_cmpl);
	vector<cmpl> R_val(n);
	for(int i = 0; i < n; i++) {
		R_val[j] = P_val[j] * Q_val[j];
	}
	
}
```


fft ni 1 arraya iki defe edende demek olarki inverse fft olur.
meselen:
	fft(fft([1 , 2 , 3 , 4])) = [4 , 16 , 12 , 8]
gorduyunuz kimi ilkinnen basqa qalanlari reverse olur ve n e vurulur hamisi.