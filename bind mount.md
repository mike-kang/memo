| 구분    | 일반 마운트                | 바인드 마운트                     |
| ----- | --------------------- | --------------------------- |
| 사용 목적 | 디바이스나 파일시스템을 디렉터리에 연결 | 기존 ==디렉터리==를 ==다른 위치==에 재노출 |
| 대상    | `/dev/sdb1` 같은 장치     | 기존의 디렉터리 (예: `/dev`)        |
| 결과    | 파일시스템 트리에 새로 추가됨      | 해당 디렉터리를 _복사 없이 공유_         |
**같은 inode를 공유함.**
/dev           → inode: 1234567
/mnt/chroot/dev → 같은 inode: 1234567 (공유됨)

ex) sudo mount --bind /dev /mnt/chroot/dev