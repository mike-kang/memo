## 🧭 요약 플로우

1. **Live USB로 부팅**
    
2. 새 파티션 포맷 및 마운트
    
3. 기존 루트 파티션 마운트
    
4. `rsync`로 전체 복사
    
5. `fstab`, `grub`, `initramfs` 수정
    
6. grub을 새 디스크에 설치
    
7. 재부팅 및 테스트
    
8. (선택) 기존 루트 파티션 정리
    

---

## 🛠️ 명령어 예제 상세

Live USB 부팅 후 터미널에서 진행:

### 1. 마운트 준비

bash

복사편집

`sudo mkdir /mnt/oldroot /mnt/newroot sudo mount /dev/sda1 /mnt/oldroot         # 기존 루트 sudo mount /dev/sdb1 /mnt/newroot         # 새 파티션`

### 2. 새 파티션 포맷 (ext4 예시)

bash

복사편집

`sudo mkfs.ext4 /dev/sdb1`

### 3. `rsync`로 복사

bash

복사편집

`sudo rsync -aAXv /mnt/oldroot/ /mnt/newroot/ \   --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"}`

### 4. 바인드 마운트 후 `chroot`

bash

복사편집

`for d in dev proc sys run; do     sudo mount --bind /$d /mnt/newroot/$d done  sudo chroot /mnt/newroot`

### 5. `/etc/fstab` 수정

bash

복사편집

`blkid /dev/sdb1  # UUID 복사 nano /etc/fstab  # 루트 파티션 UUID 수정`

### 6. grub 설치 및 재설정

bash

복사편집

`grub-install /dev/sdb          # /dev/sdb 전체에 설치 update-grub update-initramfs -u`

### 7. 마무리 및 재부팅

bash

복사편집

`exit sudo umount -R /mnt/newroot sudo reboot`

BIOS에서 `/dev/sdb` (새 디스크)로 부팅 설정을 바꾸는 것도 잊지 마세요.