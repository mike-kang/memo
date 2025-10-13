C 표준에 따르면:
> 두 `unsigned` 타입 피연산자의 연산은 **모듈러 연산(mod 2^n)** 으로 수행됩니다.
```c
#include <stdio.h> 
int main() 
{ 
unsigned char a = 245; unsigned char b = 3;
printf("%d\n", (char)(b-a));
return 0; 
}
```
모듈러 연산이므로 0과 256은 같다.
결과는, 3 + 256 - 245 = 14

위 예는 245, 다음에 overflow가 발생해서 3이 되었을 때, 둘 사이에 뺄셈에 대한 내용이다.
결국 unsigned 끼리 뺄셈은 overflow가 발생하더라도 차이가 정확히 계산된다.

