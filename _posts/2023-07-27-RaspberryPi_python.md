---
title: "[Linux] Linux Python3 기본 버전 변경"
date: 2023-07-27 11:00:00 +0900
categories: [On-Board Computer, Linux]
tags: [On-board Computer, Linux]  # TAG names should always be lowercase
---

> [BNO055](https://www.icbanq.com/P007406231?utm_source=google&utm_medium=cpc&utm_campaign=%EC%87%BC%ED%95%91_PerformanceMax&utm_id=%EC%87%BC%ED%95%91_PerformanceMax&utm_term=notset&utm_content=notset&gclid=Cj0KCQjw5f2lBhCkARIsAHeTvlgKHRisp9n-VB8-5nbougvhFRxZeSviyTZZ1ZXDsUcvYwuHzo48XKYaAuAsEALw_wcB "구매링크")
라는 9-DoF IMU 센서를 사용하기 위해 [Document](https://docs.circuitpython.org/projects/bno055/en/latest/ "BNO055 Python Document")에 따라

```pip3 install adafruit-circuitpython-bno055 ```
> 명령어 입력 시 **SyntaxError: future feature annotations is not defined** 가 발생했다.
> Python version과 관련된 문제라 이를 해결하기 위한 방법을 정리해 보았다.

## Python, Python3 버전 확인
```$ python --version```

```$ python3 --version```

라즈베리파이에서는 ubuntu 18.04에 관한 공식적인 지원이 중단되어 
[Unofficial Github](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial/releases "라즈베리파이 ubuntu 18.04")에서 이미지 파일을 받아서 설치했다.

![2023.07.27 기준 라즈베리파이 공식 홈페이지](/assets/img/post_img/rpi_ubuntu.png){: w="600" h="400" }
_2023.07.27 기준 라즈베리파이 공식 홈페이지_

ubuntu 18.04의 경우 기본적으로 **python >> Python 2.7.17, python3 >> Python 3.6.9** 가 설정되어 있다. 이 설정을 바꾸기 위해서는 먼저
새로운 Python 버전을 설치해야 한다.

## Python 새로운 버전 설치
```$ sudo apt-get install python[version]```
>> **Example**  
>>```$ sudo apt-get install python3.7```

설치를 완료했다고 바로 적용되는 것이 아니고 기본 버전을 변경해 주어야 한다.

## Python 기본 파일 확인
```$ ls -al /usr/bin/python``` 명령을 통해 python 이 가리키는 기본 파일을 확인할 수 있다.

> 💡 ***Tip!***  
> which, whereis 명령어로 명령어(command)의 위치를 알 수 있다.  
>> Ex. $ which python  
>> /usr/bin/python

## 등록된 Python 버전 확인
확인 할 경우 python2.7을 가리키고 있는데 이를 변경하기 위해선 먼저 설치한 python 버전을 등록해야 한다.  
먼저 등록된 python version을 확인하는 명령어는 아래와 같다.  
```$ update-alternatives --config python```  

현재는 아무것도 등록이 되어있지 않을 것이다. 이제 새로 설치한 python version을 등록한다.

## 설치한 버전 등록
> **python** 명령어에 등록  
```$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python[version] [지정 번호]```  
> **python3** 명령어에 등록
```$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python[version] [지정 번호]```

필자의 경우 pip3로 설치 과정에서 발생한 오류이기 때문에 python3의 버전을 수정해주어야 한다.  
위 명령어 실행 후 다시 ```$ update-alternatives --config python``` 명령어 입력 시 등록한 버전이 나오는 것을 확인할 수 있다.  
기본으로 실행시키고자 하는 버전을 가리키는 번호를 입력 후 enter

이후에 다시 python / python3 버전 확인시 버전이 변경된 것을 볼 수 있다.

필자의 경우 python3 버전을 변경 후 pip3를 통해 다시 설치 시에 정상적으로 설치 되는 것을 확인 할 수 있었다.

![pip3 down](/assets/img/post_img/rpi_pip3_down.png){: w="600" h="300" }
_pip3 install adafruit-circuitpython-bno055 명령어 정상실행_