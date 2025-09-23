
2가지를 본다.
- `CONFIG_MODVERSIONS=n`일 때는 → vermagic만 비교 (이름만 맞으면 심볼 연결)    
- `CONFIG_MODVERSIONS=y`일 때는 → vermagic 비교 + 심볼별 CRC 비교

## vermagic 확인 법
```
uname -r  #kernel 

modinfo <module path>   #module
```

## 심볼 crc 확인 법
`CONFIG_MODVERSIONS=y` 일 경우, 심볼의 crc가 `Module.symvers` 파일과 모듈의 `__versions` 섹션에 기록됨.
```
# kernel
grep -w <symbol> <Module.symvers path>  
ex) grep -w netif_carrier_off ../../../../root-fs/rootfs/lib/modules/4.19.91/build/Module.symvers

nm vmlinux | grep __crc_efuse_check_available_extend
adb2f83a A __crc_efuse_check_available_extend


# module
modprobe --dump-modversions <ko path> | grep <symbol>
ex) modprobe --dump-modversions ./_install_modules/lib/modules/4.19.91/kernel/drivers/net/phy/libphy.ko  | grep netif_carrier_off 
```


root@NVTEVM:/proc$ grep -w efuse_check_available_extend /proc/kallsyms
8038bb34 T efuse_check_available_extend
root@NVTEVM:/proc$ grep -w __crc_efuse_check_available_extend /proc/kallsyms
root@NVTEVM:/proc$

정상적인 경우에도,  grep -w `__crc_efuse_check_available_extend /proc/kallsyms` 는 없다.
CONFIG_KALLSYMS_ALL 는 /proc/kallsyms 에 `__crc_xxx`를 출력함.

짧게 말하면: **`CONFIG_KALLSYMS=y`는 커널이 “주소 ↔ 심볼명(함수/변수 이름)” 매핑 테이블을 내장**하게 해서, 디버깅·트레이싱 때 주소만 찍히지 않고 사람이 읽을 수 있는 **함수 이름**이 보이도록 해주는 옵션이에요.

## 무엇이 달라지나?

- **커널 Oops/Panic/백트레이스 가독성↑**  
    주소가 아니라 `do_page_fault+0x…` 같은 **함수명**으로 찍혀서 원인 파악이 쉬워집니다.
    
- **`/proc/kallsyms` 제공**  
    현재 커널/모듈의 심볼 목록을 볼 수 있어요(주소는 보안 설정에 따라 마스킹될 수 있음).
    
- **트레이싱/프로파일링 도구와 연동**  
    kprobes, ftrace, perf, eBPF(일부 경로) 등에서 **심볼 이름 기반** 지정과 리졸브가 더 쉬워집니다.
    
- **모듈 로딩/CRC와는 무관**  
    `CONFIG_MODVERSIONS`(심볼 CRC)와는 별개예요. kallsyms는 **보기/리졸브용 메타정보**, modversions는 **호환성 검사** 용도.
    

## `CONFIG_KALLSYMS_ALL`과의 차이

- `KALLSYMS=y`만 켠 기본값: 주로 **export된 심볼 중심**으로 테이블이 잡힙니다.
    
- `KALLSYMS_ALL=y`까지 켜면: **내부(비-export) 심볼까지 더 광범위하게** 수집해서 주소→이름 변환 성공률이 더 올라갑니다. (대신 커널 이미지가 조금 더 커짐)
## dependency


