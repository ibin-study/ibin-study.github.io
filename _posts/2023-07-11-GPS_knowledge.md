---
title: "[GPS] GNSS 관련 정리 (Dual-band, RTK, ...)"
date: 2023-07-18 17:00:00 +0900
categories: [Sensors, GPS]
tags: [Sensors, GNSS]  # TAG names should always be lowercase
---
## 서론
내비게이션, 스마트폰 등에서 흔히 사용하는 GPS. 주변에서도 흔히 찾아볼 수 있기 때문에 
쉽게 접근할 수 있다고 생각하였으나 파면 팔수록 새로운 용어나 정보들이 쏟아져 나온다.
따라서 GPS에 관해 공부하며 이를 정리하기 위해 포스팅을 해본다. ~~Github Blog 관련 공부도 할 수 있고 Markdown도 연습해 볼 기회이기도 하다.~~

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
GPS 수신기의 경우 3개 이상의 위성에서 발신하는 마이크로파를 수신해 수신기(사용자)의 위치/고도/속도를 결정하게된다. 