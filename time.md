# 현재 시간을 얻을 때, 무엇을 사용할까?
time_t time(time_t *t)와 int gettimeofday(struct timeval *tv, struct timezone *tz);
둘다 UTC기준 신기원 이후 경과된 시간을 알려준다.
초단위만 알고 싶다면, time()을
더 세밀한 시간을 알고 싶다면, 마이크로 초 단위를 알려주는 gettimeofday()를 사용하자.

# localtime() 특징
struct tm* localtime(const time_t*)
UTC 기준 초단위 시간을 알려주면, /etc/localtime timezone 링크를 참조하여 외부변수 tzname을 설정하고, timezone이 적용된 시간을 알려준다.
**localtime_r** 은 이 timezone을 반영하지 못 한다.

## tzname
![[Pasted image 20250529175029.png]]
위에서 BTT에 해당한다.