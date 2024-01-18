---
title: "[UART, USART] UART, USART 통신이란??"
date: 2023-11-23 16:00:00 +0900
categories: [Communication Protocol, Serial]
tags: [Communication Protocol, Serial, UART]  # TAG names should always be lowercase
---

## UART란?

UART
  : 범용 비동기화 송수신기, Universal Asynchronous Receiver/Transmitter 의 약자.  
  병렬 데이터의 형태를 직렬 방식으로 전환하여 데이터를 전송하는 컴퓨터 하드웨어의 일종이다.  

이 UART의 경우 **비동기식 통신**이라서 I2C와 같이 별도의 클럭 신호가 없다.  
따라서 데이터의 송수신 속도를 **Baud rate(보 레이트)로 정해주어야 한다.**  
또한 이전에 설명한 것처럼 **비트 블럭(보통 1byte)의 앞, 뒤에 Start bit, Stop bit**를 붙여야 하기 때문에 **동기식 통신에 비해 전송속도는 느리다.**  
또한 오류 검출을 위해서 Parity bit도 존재한다.

UART는 주로 4개의 핀으로 되어있다.

VCC
  : 보드에 전원을 공급해주는 핀으로 5V, 3.3V를 주로 사용한다.  
  다른 전원공급 장치가 있을 경우 사용하지 않아도 된다.

GND
  : 보드의 기준전압을 맞춰주는 핀. 데이터 전송을 위해 반드시 필요하다.

Tx
  : 데이터를 송신해주는 핀. 이 핀이 수신자 입장에서는 Rx로 들어간다.

Rx
  : 데이터를 수신하는 핀. 이 핀을 연결할 보드의 Tx와 연결한다.

![Tx Rx 연결](/assets/img/post_img/Communication_uart_txrx.png)
_UART 선 연결 예시 [출처 : UART 통신 이론](https://how-to-make-a-quadcopter.tistory.com/1)_
![Tx Rx 연결2](/assets/img/post_img/Communication_uart_txrx2.png)
_UART 선 연결 예시 2 [출처 : UART: 범용 비동기식 수신기/송신기를 이해하는 하드웨어 통신 프로토콜](https://ko.fmuser.net/content/?20365.html)_


위 그림과 같이 **RX, TX를 교차해서 연결**해 주어야 한다.  
또한 2번째 그림에서 볼 수 있듯이 병렬 신호(Bus)를 직렬로 바꾸어 보내주는 것이 UART이다.  

Tx, Rx 핀이 각각 존재해 **동시에 송수신이 가능(전이중)**하며 **1:1로 통신만 가능**하다는 특징이 있다.  

## USART란??
UART
  : 범용 동기/비동기화 송수신기, Universal Synchronus/Asynchronous Receiver/Transmitter 의 약자.    

즉, USART는 동기화가 된다는 것이다. 따라서 클럭 신호가 존재한다.  
동기화를 동해 클락신호의 유무만 체크하면 되므로 데이터 송수신 효율이 높고 더 빠른 전송속도를 가진다.
그러나 클럭 신호를 보내기 위한 별도의 핀이 추가로 필요하다는 단점이 있다.

현대 집적회로(IC)들 중 대부분은 동기화 통신인 USART를 함께 지원한다.  
이러한 장치들은 USARTs 또는 USART/UART 라고 부른다.  
PC에서 흔히 볼 수 있는 COM Port가 바로 이 통신을 위한 장치이다.

## 참고자료
[[아두이노 강좌] 15. Serial 통신(1) - 시리얼 통신이란 무엇인가](https://blog.naver.com/yuyyulee/220301424499)  
[[시리얼 통신] UART](https://sroongzi.tistory.com/entry/%EC%8B%9C%EB%A6%AC%EC%96%BC-%ED%86%B5%EC%8B%A0-UART)  
[출처 : UART 통신 이론](https://how-to-make-a-quadcopter.tistory.com/1)  
[하드웨어 해킹 - (7) UART](https://blog.naver.com/wnswl316/221428720820)  
[출처 : UART: 범용 비동기식 수신기/송신기를 이해하는 하드웨어 통신 프로토콜](https://ko.fmuser.net/content/?20365.html)  
[시리얼 통신의 종류(Uart/Usart, I2C, SPI)와 개념 및 차이점 정리](https://melonicedlatte.com/2021/03/25/113400.html)