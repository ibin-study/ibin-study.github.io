---
title: "[GPS] GNSS 관련 정리 (Dual-band, RTK, ...)"
date: 2023-07-18 17:00:00 +0900
categories: [Sensors, GPS]
tags: [Sensors, GNSS]  # TAG names should always be lowercase
---
## 서론
> 내비게이션, 스마트폰 등에서 흔히 사용하는 GPS. 주변에서도 흔히 찾아볼 수 있기 때문에 
> 쉽게 접근할 수 있다고 생각하였으나 파면 팔수록 새로운 용어나 정보들이 쏟아져 나온다.
> 따라서 GPS에 관해 공부하며 이를 정리하기 위해 포스팅을 해본다. ~~Github Blog 관련 공부도 할 수 있고 Markdown도 연습해 볼 기회이기도 하다.~~

---

## 1. GNSS란?

GNSS
  : Global Navigation Satellite System 의 약자, 범지구적 위성항법 시스템. 즉, 모든 글로벌 위성 위치 확인 시스템을 포괄하는 용어

우리가 흔히 아는 GPS는 가장 널리 사용되는 GNSS라고 볼 수 있다. **미 국방부**에서 개발한 **GPS** 외에도 다른 국가에서 개발한 GNSS 가 있다.

- GPS : 미국
- GLONASS : 러시아
- Galileo : EU
- Beidou : 중국

범지구적 위성항법 시스템이 아닌 특정 지역에서만 서비스 하는 시스템 _(ex. IRNSS[인도], QZSS[일본]...)_ 의 경우 **RNSS(Regional Navigation Satellite System)** 이라고 부르기도 하지만 통칭 GNSS라고 부른다.

---

## 2. GNSS 원리
GPS 수신기의 경우 3개 이상의 위성에서 발신하는 마이크로파를 수신해 수신기(사용자)의 위치/고도/속도를 결정하게된다. 그러나 오차 보정을 위해 보통 4개 이상의 위성을 이용해 위치를 결정한다

각각의 GPS 위성에서는 [여러 정보](https://ko.wikipedia.org/wiki/GPS "위성에 탑재된 시계의 시각 및 오차와 위성의 상태 정보, 모든 위성과 관련된 궤도 정보와 상태(almanac), 각각의 궤도정보와 이력(ephemeris), 오차 보정을 위한 계수 등이 포함")가
포함된 항법 메시지(Navigation message)를 50[bps](https://ko.wikipedia.org/wiki/%EB%B9%84%ED%8A%B8%EB%A0%88%EC%9D%B4%ED%8A%B8 "초 마다 처리하는 비트의 수 bit per second")의 속도로 지속적으로 방송한다. 

이러한 항법메세지를 C/A 코드(Coarse/Acquisition code), P 코드(Precision code)와 같이 
<span style="color:blue">**반송파(Carrier signal)**</span>에 실어 송신한다.
여기서 C/A 코드와 P 코드에는 위성마다 고유한 의사잡음부호가 담기게 되고 C/A코드의 경우 민간에 개방되어있지만 P 코드는 군사목적으로 암호화 되어 있다.
또한 반송파란 **정보의 전달을 위해 입력 신호를 변조한 전자기파**를 말한다. 

GPS가 사용하는 반송파의 송신 주파수의 경우 L1 ~ L5까지 5개가 있는데 L3와 L4의 경우 정밀해석과 기하학적 보정을 위한 L1, L2의 합성파임으로 사실 개별적인 반송파는 **L1, L2, L5**라고 볼수 있다.