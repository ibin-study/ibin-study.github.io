---
title: "[I2C] Raspberry Pi에서 I2C 사용해 BNO055 모듈 사용"
date: 2023-08-02 15:00:00 +0900
categories: [Communication Protocol, I2C]
tags: [Communication Protocol, I2C, Raspberry Pi]  # TAG names should always be lowercase
---

## 0. I2C란??
I2C 관련 내용은 이전에 정리한 포스팅 참고.  
[[I2C] I2C 통신이란??](https://ibin-study.github.io/posts/Communication_i2c/ "ibin's study - [I2C] I2C 통신이란??")

## 1. Raspberry Pi I2C 기능 활성화
라즈베리파이에서 Command 창을 킨 후  
**```$ sudo raspi-config```** 명령어 입력  
![RPi config](/assets/img/post_img/RPi-config.png)  
입력하면 이러한 창이 뜨게 되는데 여기에서 화살표로 **5 Interfacing Options**로 이동 후 Enter  
![RPi config2](/assets/img/post_img/RPi-config_2.png)  
이러한 창이 뜨면 다시 5번째의 I2C로 이동 후 Enter  
ARM I2C interface를 활성화 할거냐는 창이 뜨게 되는데 **Yes**선택 후 Enter  
이제 화살표 오른쪽을 눌러서 Finish를 통해 설정창을 종료한다.

## 2. i2c-tools 설치
터미널에서 연결된 센서의 정보를 확인하기위해 i2c-tools 설치
```shell
$ sudo apt-get update
$ sudo apt-get install i2c-tools
```

## 3. 계정 권한부여
사용 계정에 i2c에 접근할 수 있는 권한을 부여해야 한다. (굳이 진행하지 않아도 되는것 같지만 하는 것이 좋아보인다.)  
```$ sudo adduser <계정명> i2c```

이제 설정이 끝났으므로 라즈베리파이를 재부팅 한다.  
```$ sudo reboot now```

## 4. i2c모듈, 드라이버 활성화 확인
lsmod 명령어를 통해 라즈베리파이에 설치된 모듈을을 모두 확인할 수 있다. i2c만 확인하기 위해서 grep을 활용한다.  
```$ lsmod | grep i2c```  
![RPi lsmod](/assets/img/post_img/RPi-lsmod.png)  
이런 식으로 출력되는 경우 정상적으로 설정된 것이다.

i2c 관련 드라이버도 생성되었는지 확인해보자.  
```$ ls -l /dev/*i2c*```  
![RPi dev](/assets/img/post_img/RPi-dev.png)  
정상적으로 존재하는 것을 확인할 수 있다. 
> 💡 리눅스에서는 장치도 모두 파일로 다루어지며 그 파일들은 /dev/ 폴더에 있다.

이제 BNO055 모듈을 사용하기 위한 작업을 해야한다.

## 5. BNO055 필요 라이브러리 설치
라즈베리파이에서 BNO055 모듈을 사용하기 위해서는  
``` shell
pip3 install adafruit-circuitpython-bno055
```  
로 설치가 필요한데 이 과정에서 **SyntaxError: future feature annotations is not defined** 에러가 발생했다.
따라서 이를 해결하기 위해 Python3의 버전을 바꿔주었는데 관련 내용은 [이전 포스팅](https://ibin-study.github.io/posts/RaspberryPi_python/)을 참고하기 바란다.

이제 라즈베리파이와 BNO055 모듈을 선으로 연결해 주어야 한다.

## 6. Raspberry Pi와 모듈 선으로 연결
필자의 경우 브래드보드를 사용해 연결해 주었다. 연결하는 방법은 어렵지 않다. 아래의 pinmap을 참고해서  
**3.3V는 VIN, GND 는 GND, SCL은 SCL, SDA는 SDA**에 연결해주면 된다. (당연한 말이네...🤔)

### Raspberry Pi4 Pin map
![RPi Pinmap](/assets/img/post_img/RPi-GPIO-Pinout.png)
_Raspberry Pi Pinmap [출처: [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)]_

> ❕ Pinmap에서 처음에는 4, 6번 핀에 팬이 꽃혀있기도 했고 비슷한 위치에 선을 모으기 위해 *(17, 20에 VIN, GND 연결)* 
**27, 28번 핀에 SDA, SCL핀을 연결**했었는데 계속 장치를 인식을 못해서 **3, 5번 핀에 연결**하니 정상적으로 인식했다. 
27, 28도 I2C의 일종이나 다른 기능이 있는 것 같다...

### 연결된 장치 확인
전에 설치해둔 i2c-tools를 활용해 라즈베리파이와 연결된 i2c 장치를 확인해보자.  
```$ i2cdetect -y 1```  
![RPi Pinmap](/assets/img/post_img/RPi-i2cdetect.png)
_연결된 장치 확인_  
정상적으로 연결된 경우 위 사진 처럼 해당 칸에 16진수 형식으로 주소가 표시된다.  
사진의 경우 **"0x28"** 이라는 것을 알 수 있다.

### 코드 작성  

```python
import board
import busio
# from adafruit_extended_bus import ExtendedI2C as I2C
import adafruit_bno055

i2c = board.I2C()
sensor = adafruit_bno055.BNO055_I2C(i2c)

while True:
    print('Temperature: {} degrees C'.format(sensor.temperature))
    # print('Accelerometer (m/s^2): {}'.format(sensor.accelerometer))
    # print('Magnetometer (microteslas): {}'.format(sensor.magnetometer))
    # print('Gyroscope (deg/sec): {}'.format(sensor.gyroscope))
    print('Euler angle: {}'.format(sensor.euler))
    print('Quaternion: {}'.format(sensor.quaternion))
    print('Linear acceleration (m/s^2): {}'.format(sensor.linear_acceleration))
    print('Gravity (m/s^2): {}'.format(sensor.gravity))
    print()
```




## 참고자료
[Github - Acafruit_CircuitPython_BNO055](https://github.com/adafruit/Adafruit_CircuitPython_BNO055)  
[라즈베리파이 I2C 사용방법](https://m.blog.naver.com/chgy2131/221922893758)  
[라즈베리파이 mpu6050 가속도 센서 제어하는 방법](https://hoho325.tistory.com/224)  


