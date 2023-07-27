---
title: "[I2C] I2C 통신이란??"
date: 2023-07-27 15:00:00 +0900
categories: [Communication Protocol, I2C]
tags: [Communication Protocol, I2C]  # TAG names should always be lowercase
---

## 1. I2C란?
I2C
  : Inter-Integrated Circuit의 약자, "아이 투 씨"라고 흔히 말하지만 정식 명칭은 "아이 스퀘어 씨"이다.  
  두개의 선을 이욯한 통신으로 TWI(Two Wire Interface)라고도 불린다.

I2C는 데이터 통신을 위한 선**(SDA)**과 송수신 타이밍 동기화를 위한 클럭 선**(SCL)**으로 구성되어 있다.  
하나의 마스터(Master)와 하나 이상, 이론상 최대 127개의 슬레이브(Slave)로 이루어진다.  

![i2c circuit](/assets/img/post_img/i2c_circuit.png)
_I2C Circuit 그림 [출처: [엔지니어스-Engineeus](https://mickael-k.tistory.com/184)]_

데이터 송수신은 마스터에서 주도하며 데이터를 송수신 하기 전 반드시 슬레이브의 주소를 명시한 후에 통신을 시작해야 하기 때문에 찗은 데이터 통신에 주로 사용된다.
> ❔ **Master / Slave**
>> 마스터/슬레이브는 장치나 프로세스**(마스터)**가 하나 이상의 다른 장치나 프로세스**(슬레이브)**를 통제하고 통신 허브 역할을 하는 **비대칭 통신 및 제어 모델**을 의미한다.

## 2. I2C 통신을 위한 조건  
위 그림에서 유의해야 할 정보는 Rp로 표기된 **풀업 저항**이다. 통신을 위해서는 기본적으로 SDA와 SCL선이 모두 High 상태여야 하기 때문에 풀업 저항을 통해 High 상태를 만들어 주는것이 중요하다.  
하지만 아두이노와 같은 보드 사용시 내부 풀업저항을 사용하기 때문에 직접 달 필요는 없다. *(찾아본 결과 라즈베리파이 역시 내부 풀업저항이 있는 것으로 보임)*

> ❔ **풀업 저항**
>> ㄴㅇ  
![pull-up_resistance](/assets/img/post_img/pull-up_resistance.png)
_Pull-up 저항 그림 [출처: [풀업저항](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=emperonics&logNo=221697492619)]_



## 참고자료
[위키백과 - 마스터/슬레이브(기술)](https://ko.wikipedia.org/wiki/%EB%A7%88%EC%8A%A4%ED%84%B0/%EC%8A%AC%EB%A0%88%EC%9D%B4%EB%B8%8C_(%EA%B8%B0%EC%88%A0))  
[엔지니어스-Engineeus - I2C란?(엄청 쉽게 설명)](https://mickael-k.tistory.com/184)  
[[아두이노 강좌] 29. I2C 통신 (1) - I2C 통신이란 무엇인가](https://blog.naver.com/yuyyulee/220323559541)  
[풀업저항](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=emperonics&logNo=221697492619)  
