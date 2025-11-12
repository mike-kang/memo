SDIO data line : 4 or 8  -->  4bit or 8bit

eMMC는 SD 카드와 유사한 버스 구조를 가지며, `CMD`, `CLK`, `DAT[0:7]` 선으로 통신합니다.

- **4bit 모드**: `DAT0~DAT3` 사용    
- **8bit 모드**: `DAT0~DAT7` 사용


## 초기화 시 데이터 버스 폭 변화 순서

|단계|버스폭|설명|
|---|---|---|
|**① Power-on / Reset 후**|**1-bit**|모든 eMMC는 CMD/DAT0 한 쌍만으로 기본 동작. (표준 규격상 기본 모드)|
|**② CMD0 (GO_IDLE_STATE)**|1-bit|카드 리셋|
|**③ CMD1 (SEND_OP_COND)**|1-bit|카드 전압 협상|
|**④ CMD2~CMD3**|1-bit|RCA (Relative Card Address) 할당|
|**⑤ CMD7 (SELECT_CARD)**|1-bit|카드 선택|
|**⑥ CMD8 (SEND_EXT_CSD)**|1-bit|확장 레지스터 읽기 (여기서 지원 가능 모드 확인)|
|**⑦ CMD6 (SWITCH)**|1-bit → 4-bit 또는 8-bit|`EXT_CSD[183] BUS_WIDTH` 레지스터를 통해 버스 폭 전환|
|**⑧ 고속 모드 진입**|4/8-bit|이후 HS200/HS400 등의 고속 모드 가능|

