---
title: "[Linux] Ubuntu 18.04 에서 Wine 사용하기"
date: 2023-12-08 14:00:00 +0900
categories: [On-Board Computer, Linux]
tags: [Wine, Linux]     # TAG names should always be lowercase
---

## 서론
> BLHeli 펌웨어를 지원하는 ESC를 사용해서 모터의 Delay time 측정 시에 Jetson Nano를 사용하는데,  
Jetson Nano의 Ubuntu 18.04 환경에서 BLHelisuite를 사용하면 추가적인 노트북 없이도 세팅 변경이 가능하므로  
Ubuntu에서 BLHelisuite를 사용하기 위한 방법에 대해 정리했다.

## Wine 프로그램이란?
Wine은 Wine Is Not an Emulator의 약어로 리눅스, macOS, BSD와 같은 POSIX 호환 운영체제에서 Windows 프로그램을 실행할 수 있는 호환성 레이어다. 
가상 머신이나 에뮬레이터와 같이 내부 Windows 로직을 시뮬레이션하는 대신 Wine은 Windows API 호출을 POSIX 시스템 호출로 즉시 대체하여 작동한다. 
다른 방식과 다르게 성능이나 메모리 문제가 적으며, Windows 프로그램을 데스크톱에 깔끔하게 통합할 수 있다는 특징이 있다.

## Wine 설치
현재 기준(23.12.8), Ubuntu 18.04 LTS는 지원이 끝났고 그에 따라 Wine 역시 **20.04 부터 source file이 존재**한다.  

> 💡 Ubuntu 버전 확인
>> ```lsb_release -a``` 를 통해 자신의 버전을 확인할 수 있다.  
>> ![lsb_release -a 결과](/assets/img/post_img/Ubuntu_lsb_release.png)
_```lsb_release -a``` 의 결과_

음... Jetson Nano의 Architecture는 aarch64인데... Wine에서 지원하는 건 amd64와 i386 뿐인 것 같다.  
좀 더 찾아본 결과, Wine의 소스코드를 가져와서 직접 Build 해서 사용하는 방법도 있는 것 같은데..  
이 방법은 이후 시간이 나면 조사해서 정리해야 핧 것 같다. 😫

직접 빌드하는 것 말고 터미널을 통한 설치 방법은 
[Wine 홈페이지](https://winehq.org/) 
에서 **디운로드** 로 갈 경우 잘 정리되어 있으므로 그 document를 참고하면 된다.  


## 참고자료
[How To Flash BLHeli_S Firmware To EFM8BB21F16G](https://www.bertfpv.com/how-to-flash-blheli_s-firmware-to-efm8bb21f16g/)  
[[20.04 LTS] Wine 설치 및 구성](https://itlearningcenter.tistory.com/entry/%E3%80%90Ubuntu-2004-LTS%E3%80%91%EC%B9%B4%EC%B9%B4%EC%98%A4%ED%86%A1-%EC%84%A4%EC%B9%98)  
[Wine 홈페이지](https://winehq.org/)  
[Ubuntu WineHQ Repository - Ubuntu Wine 다운방식 설명](https://wiki.winehq.org/Ubuntu)  
