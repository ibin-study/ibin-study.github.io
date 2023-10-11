---
title: "[Jetson] Jetson Nano PWM 신호 사용 가능하게 만들기"
date: 2023-10-11 12:00:00 +0900
categories: [On-Board Computer, Jetson]
tags: [Jetson, PWM]  # TAG names should always be lowercase
---
Jetson Nano에서 PWM 신호를 사용하고자 했을 때 쉽게 찾을 수 있는 블로그 등에서 설명했듯이
간단하게 설정만 바꾸는 것으로는 코드 상으로 PWM신호가 출력이 되지 않았다.  
따라서 여러 정보를 찾던 도중 이 방법으로 PWM신호가 출력되어 해결 방법을 정리하고자 한다.

## 1. Jetson Pin Configuration
터미널에서  
```terminal
$ sudo /opt/nvidia/jetson-io/jetson-io.py  
```  
명령어를 치고 들어가면 아래와 같은 화면이 출력된다.

![Jetson 핀 설정](/assets/img/post_img/Jetson_Expansion_Header_Tool_1.png)
_Jetson Expansion Header Tool_

**화살표와 ENTER키**를 이용해 **"Configure Jetson 40pin Header"**로 들어간다.

![Jetson 핀 설정](/assets/img/post_img/Jetson_Expansion_Header_Tool_2.png)
_Jetson Expansion Header Tool_  
> 현재는 설정 이후 캡쳐한 사진이라 32번, 33번 핀이 pwm0, pwm2로 표시되어 있지만  
> 처음 들어갈 경우 **unused**로 나올 것이다.

**"Configure header pins manually"**로 들어간다.

![Jetson 핀 설정](/assets/img/post_img/Jetson_Expansion_Header_Tool_3.png)
_Jetson Expansion Header Tool_  

이 화면에서 pwm0(32), pwm2(33)을 선택 후에 back 으로 돌아간다. 

![Jetson 핀 설정](/assets/img/post_img/Jetson_Expansion_Header_Tool_4.png)
_Jetson Expansion Header Tool_   
**"Save pin changes"**로 저장한다.

![Jetson 핀 설정](/assets/img/post_img/Jetson_Expansion_Header_Tool_5.png)
_Jetson Expansion Header Tool_  
이제 **"Save and reboot to reconfigure pins"**로 저장 후 재부팅한다.

>>🤔 대부분의 글에서 이 과정만으로 PWM 신호를 사용했다고 하지만 필자의 경우 오실로스코프로 확인해 본 결과
PWM 신호가 출력되지 않았다.

## 2. PWM 상태 확인
```terminal
$ sudo cat /sys/kernel/debug/pwm
``` 
이 명령어를 통해 현재 PWM status를 알 수 있다.  
![PWM 상태 확인](/assets/img/post_img/Jetson_pwm_status_1.png)  
현재는 추가적인 명령어를 입력하지 않아 pwm-0과 pwm-2 모두 null로 표시되어 있다.

## 3. busybox 명령어를 통해 핀 사용 설정
> ❔ busybox 란?
>> 수많은 UNIX 명령행 유틸리티의 기능을 하나의 실행 파일 안에 통합시킨 소프트웨어  
>> 400개 가량의 Linux 커맨드라인 명령어들을 모아놓은 단일 실행파일

필자의 경우 busybox가 설치되어있지 않았으므로 간단하게 apt명령어를 활용해 설치해 주었다.
```terminal
$ sudo apt install busybox
```
설치 이후 아래의 명령어를 실행해 준다.
```terminal
### Enable Pin 32 / PWM0
$ sudo busybox devmem 0x700031fc 32 0x45
$ sudo busybox devmem 0x6000d504 32 0x2

### Enable Pin 33/ PWM2
$ sudo busybox devmem 0x70003248 32 0x46
$ sudo busybox devmem 0x6000d100 32 0x00
```

> ❗ 재부팅시에는 다시 입력해 주어야 PWM신호가 정상적으로 출력된다.

## 4. echo 명령어를 통해 테스트
```terminal
$ echo 0 > /sys/class/pwm/pwmchip0/export
$ echo 50000 > /sys/class/pwm/pwmchip0/pwm0/period
$ echo 25000 > /sys/class/pwm/pwmchip0/pwm0/duty_cycle
$ echo 1 > /sys/class/pwm/pwmchip0/pwm0/enable
```
> duty_cycle을 먼저 입력할 경우 PWM status에서 확인 가능하듯이 period가 0이기 때문에
```bash: echo: write error: Invalid argument``` 오류가 뜬다.
먼저 Period를 설정 후에 입력 시 오류가 발생하지 않는다.

위 명령어를 입력 후 Oscilloscope로 테스트 시 정상적으로 파형이 출력되는 것을 확인할 수 있었다.  
![오실로스코프 테스트](/assets/img/post_img/PWM_Oscilloscope.jpg){: w="400" h="300" } 
_Oscilloscope로 테스트_

> 💡 PWM 신호의 경우 10대 1 비율로 보는것이 사진처럼 명확하게 나온다!


## 참고자료
[Nvidia Forum - Jetson Nano PWM not working](https://forums.developer.nvidia.com/t/jetson-nano-pwm-not-working/154939/14)  
[나무위키 - busybox](https://namu.wiki/w/BusyBox)  
[Busybox 소개와 사용법 - LainyZine:프로그래머 가이드](https://www.lainyzine.com/ko/article/busybox/)