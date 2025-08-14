# 구성
시계
timepoint : 시점. 
duration



# 시간 측정
```c++
	auto start = std::chrono::high_resolution_clock::now();
	...
	auto end = std::chrono::high_resolution_clock::now();
	int c = std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count();

```

시계의 종류
![[Pasted image 20250814143816.png]]