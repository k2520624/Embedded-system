# Embedded-system

**ㆍ팀원**  
* 강동훈  
* 이승헌
* dsfsf

※ **영상주소**  
https://www.youtube.com/watch?v=524T28MoZyY  

※ **블럭도**  
  
![블럭도](https://user-images.githubusercontent.com/94602281/174634629-fbf67d49-8fea-4d10-8dd1-56cd1eca2711.PNG)

※ **Node-red dashboard**  
  
![imbeded](https://user-images.githubusercontent.com/94602281/174634908-e282e40a-89a9-4271-ad0f-3b7896b6db5d.png)

**1. IMU(SLM6DSOX)**  
* 3축 가속도와 3축 자이로 센서를 조합한 후 각각의 센서 출력을 내보내는 장치를 관성측정장치(IMU;Inertial Measurement Unit)이라고 부른다.  
* 종류에 따라 자이로스코프 가속도계만 있는 6축센서, 자이로스코프와 가속도계, 지자기센서까지 포함한 9축센서도 있다.  
* 스마트폰에도 탑재되어 있을 정도로 그 용도가 근래에 흔하며, 비행기의 항법 장치에 필수적인 요소입니다.  
  
**2. Omnidirectional Digital Microphone(MP34DT05)**  
* IMP34DT05는 정전 용량 감지 요소와 I2C 인터페이스로 제작된 초소형, 저전력, 무지향성, 디지털 MEMS 마이크입니다.  
* IMP34DT05는 신호 대 잡음비가 64dB이고 감도가 -26dBFS ±3dB인 저왜곡 디지털 마이크입니다.  
* IMP34DT05는 상단 포트, SMD 호환, EMI 차폐 패키지로 제공되며 -40°C ~ +85°C의 확장된 온도 범위에서 작동하도록 보장됩니다.  

**3. Mbed OS**  
* Mbed OS는 IOT의 T를 위해 설계된 무료, 오픈소스의 운영체제입니다.  
* Mbed OS에는 광범위한 표준 MCU 주변 장치에 대한 드라이버 지원이 포함되어 있습니다.  
* 간단한 USB 드래그 앤 드롭 프로그래밍을 통해 값비싼 디버그 하드웨어 없이 빠르게 프로토타입을 만들 수 있습니다.  

**4. ARM**  
* ARM은 Advanced RISC Machine의 약자로 임베디드 기기에 주로 사용되는 32bit 프로세서입니다.  
* ARM은 고성능 MPU와 더불어 다양한 병렬 제어 유닛과 통신 인터페이스를 갖추고 있어 다양한 응용을 지원하는 강력한 아키텍처를 구성하고 있습니다.  

**5. Microchip ATECC608A**  
* 보안 하드웨어 기반 키 스토리지가 있는 암호화 코프로세서이다.  
* 대칭 알고리즘에 대한 하드웨어를 지원한다.  
* 메모리의 다양한 섹션에 대한 액세스는 다양한 방법으로 제한될 수 있으며 변경을 방지하기 위해 구성을 잠글 수 있습니다.  

**6. I2C**  
* I2C 통신은 2개의 선을 이용하는 통신 방식이다.  
* 하나의 마스터에 여러 개의 슬레이브 기기가 연결될 수 있다는 장점이 있다.  
* 클럭 신호를 사용하는 동기식 통신 방식이기 때문에 시간에 자유롭다는 장점이 있다.  
* 슬레이브 선택을 위해 항상 주소 데이터가 붙기 때문에 긴 데이터에는 부적합하다는 단점이있다.  

**7. python callback**  
* 프로그래밍에서 콜백(callback)은 다른 코드의 인수로서 넘겨주는 실행 가능한 코드를 말한다.  
* 콜백(callback)을 넘겨받는 코드는 이 콜백(callback)을 필요에 따라 즉시 실행할 수도 있고, 아니면 나중에 실행할 수도 있다.  

**8. uf2**  
* UF2는 USB 플래싱 형식을 나타내는 Microsoft에서 설계한 파일 형식입니다.  
* 이 형식은 PXT(Microsoft MakeCode라고도 함)용으로 설계되었으며 대용량 저장소 클래스(이동식 드라이브)를 통해 보드를 프로그래밍할 수 있습니다.  
* UF2를 사용하면 하나의 부트로더에서 MakeCode를 작성하고, Circuit Python을 사용하고, Arduino IDE를 사용할 수 있습니다.  
