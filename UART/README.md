## UART: Raspberry Pi 4 (UART3) ↔ STM32 (USART6)

### 핀 & 디바이스
- **Raspberry Pi 4**  
  - UART3: **TXD3=GPIO4**, **RXD3=GPIO5**  → 디바이스: **/dev/ttyAMA3**  
- **STM32F411RE (USART6)**  
  - **TX = PA11 (USART6_TX)**  
  - **RX = PA12 (USART6_RX)**  

### 배선
- RPi **GPIO4 (TXD3)** → STM32 **PA12 (USART6_RX)**
- RPi **GPIO5 (RXD3)** ← STM32 **PA11 (USART6_TX)**
- **GND ↔ GND** (공통)
- 전압 레벨: **3.3V TTL** (5V 연결 금지)

### Raspberry Pi 설정 (`/boot/firmware/config.txt`)
```ini
# 추가 UART 활성화
dtoverlay=uart3
```
```bash
# 재부팅 후 확인
ls -l /dev/ttyAMA3
dtoverlay -h uart3 
raspi-gpio get 4,5
```