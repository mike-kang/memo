
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
grep -w <symbol> <Module.symvers path>  #kernel
ex) grep -w netif_carrier_off ../../../../root-fs/rootfs/lib/modules/4.19.91/build/Module.symvers

modprobe --dump-modversions libphy.ko | grep netif_carrier_off # odule
```


root@NVTEVM:/proc$ grep -w efuse_check_available_extend /proc/kallsyms
8038bb34 T efuse_check_available_extend
root@NVTEVM:/proc$ grep -w __crc_efuse_check_available_extend /proc/kallsyms
root@NVTEVM:/proc$

정상적인 경우에도,  grep -w __crc_efuse_check_available_extend /proc/kallsyms 는 없다.


## dependency


