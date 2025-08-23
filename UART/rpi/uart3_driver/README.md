이 프로젝트는 Ubuntu 에서 ARM용으로 크로스 컴파일하고, 생성된 바이너리를 Raspberry Pi 4(타깃) 에서 실행합니다.(Build on Ubuntu → Run on Raspberry Pi)<br>
추가로 라즈베리 파이와 STM32를 UART로 연결해 에코백 테스트를 수행하는 예제입니다.

## 실행 방법

**ubuntu**
```bash
# 산출물(.ko, 앱)이 NFS 공유 디렉터리(/srv/nfs_ubuntu/uart3)로 자동 배치됨
make
```

**raspberry**
```bash
# 커널 모듈 로드
sudo insmod uart3_driver_mknod.ko

# 생성된 노드 확인
ls -l /dev/uart3_raw || dmesg | tail

# 앱 실행 (권한 필요 시 sudo)
./uart3_app
```

## 해제

**raspberry**
```bash
# 모듈 제거
sudo rmmod uart3_driver_mknod

# 디바이스 노드 삭제
sudo rm -f /dev/uart3_raw
```