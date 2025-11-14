| 패턴         | 의미                            |     |
| ---------- | ----------------------------- | --- |
| `tools/`   | directory 무시                  |     |
| `tools/*`  | 한 단계 아래 파일/폴더만 무시 (하위 재귀 X)   |     |
| `tools/**` | tools 아래 모든 파일/폴더 재귀적으로 전부 무시 |     |

u-boot 라고 명시하면, 
u-boot 무시
aaa/u-boot 무시

현재 경로의 u-boot만 무시하려면,
/u-boot

무시하는 것은 aaa 라고하면, 하위 경로까지 싹 무시되지만,
무시를 예외처리하는 !aaa 는 현재 경로에만 적용된다.
예외의 경우, 꼭 전체 path를 적어야 한다.

## directory 안에 있는 것들을 무시하고 directory만 남겨놓으려면,
```
rootfs/lib/*
!rootfs/lib/.gitexist

```
