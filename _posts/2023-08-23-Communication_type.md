---
title: "통신 방식에 따른 분류 (serial/parallel, 동기/비동기...)"
date: 2023-08-23 16:00:00 +0900
categories: [Communication Protocol, Basic]
tags: [Communication Protocol]  # TAG names should always be lowercase
---

## Serial 통신 / Parallel 통신
Serial 과 Parallel 즉, 직렬 병렬 통신은 말 그대로 서로 다른 장치를 디지털 통신을 통해 직렬 혹은 병렬로 연결하는 것이다.
아래의 그림은 '십진수 100' 이라는 값을 직렬, 병렬 통신으로 전송하는 것을 나타낸 것이다.  

![Serial, Parallel 통신 비교](/assets/img/post_img/serial_parallel_commu.png)
_Serial 통신과 Parallel 통신 예시_

**<span style="background-color:Pink">Serial 통신</span>은 대개 하나의 신호선을 이용**하여 데이터를 주고받는 통신을 말한다.
신호선이 하나이기 때문에 데이터를 일정 시간 간격으로 전송하게 되므로 모든 데이터를 전송하기 위해서는 시간이 좀 더 소요된다.
그러나 이렇게 적은 수의 신호선을 사용하기 때문에 저렴한 비용으로 통신을 할 수 있고, 단말 장치 역시 소형화가 가능하다.

> 👀 Serial 통신 시스템 종류
>> **UART/USART** (Universal Synchronous and Asynchronous serial Receiver and Transmitter)  
**SPI** (Serial Peripheral Interface)  
[**I2C** (Inter-Integrated Circuit)](https://ibin-study.github.io/posts/Communication_i2c/)  
**CAN**(Controller Area Network)  
**LIN**(Local Interconnect Network)  
RS-232, RS-422, RS-485
>>>Serial 통신의 각 시스템에 대해서는 다른 포스팅에 차차 정리할 예정이다. 정리가 되면 링크로 첨부하겠다.

**<span style="background-color:PowderBlue">Parallel 통신</span>은 여러 개의 신호선을 사용**해
단위 시간당 전송되는 데이터 bit의 양은 직렬에 비해 많다.
그러나 이러한 **병렬 통신은 고속 통신규격에 있어서 쇠퇴**하고 있는데 그 이유는 아래와 같다.

- 통신 거리가 길어질 경우 이 많은 선들은 모두 연장해주어야 하므로 **통신 비용이 올라감**
- 데이터 통신에 필요한 단자 역시 **소형화하기 어려움**  
- 각 병렬 통신 규격의 스펙에 비해 실제로 원활하게 작동(혹은 IO) 요구되는 통신량(속도)가 높기 때문에
일반적인 **소비자가 접하는 환경에서는 병렬 통신 규격이 더 느린 경우가 많음**
- 통신 속도가 더 빨라지면서 통신 속도를 늘리기 위해 통신 쓰루풋(주파수)을 늘리다 보면 **데이터 신호가 주변 선에 간섭하는 현상** 발생
- 선이 수십가닥인 만큼 **간섭 수준이 데이터의 무결성에 영향**을 줄 정도로 커짐
- 모든 선을 **절연, 차폐 하기에는 비용이 많이 듬**
- **타이밍 틀어짐(timing skew)** or **클럭 틀어짐(clock skew)** 현상으로 높은 데이터 전송 속도가 필요한 곳에서는 심각한 문제 초래 가능성  
![Parallel 통신 타이밍 틀어짐(timing skew)](/assets/img/post_img/parallel_timing_skew.png)
_Parallel 통신에서 Timing skew(Clock skew)_

- **<span style="color:Red">LVDS</span>** 라는 새로운 기술의 발명으로 인해 직렬 통신의 데이터 전송 속도 향상과 제조 단가의 절감 달성

> 💡 LVDS란??
>> Low Voltage Differential Signalling(저전압 차등 시그널링)  
저렴한 연선 구리케이블에 고속으로 동작이 가능한 전기적 신호 시스템을 말한다.  
데이터를 낮은 전압과 적은 전위차로 전송해 데이터 송수신 속도를 향상하고 노이즈에 강하게 하고 전력 소모를 적게 하기 위한 통신방법이다.

> 👀 Parallel 통신 시스템 종류
>> 컴퓨터 주변 기기용 버스: [ISA](https://ko.wikipedia.org/wiki/ISA_%EB%B2%84%EC%8A%A4) ,
[ATA](https://ko.wikipedia.org/wiki/AT_%EA%B2%B0%ED%95%A9) ,
[SCSI](https://ko.wikipedia.org/wiki/SCSI) ,
[PCI](https://ko.wikipedia.org/wiki/PCI_%EB%B2%84%EC%8A%A4) ,
[프론트 사이드 버스](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%A0%ED%8A%B8_%EC%82%AC%EC%9D%B4%EB%93%9C_%EB%B2%84%EC%8A%A4) ,
[IEEE-1284(센트로닉스 포트)](https://ko.wikipedia.org/wiki/IEEE-1284)  
[IEEE-488](https://ko.wikipedia.org/wiki/IEEE-488)  
주로 CPU 근거리에 있는 주변장치들과 통신하거나 과거의 프린터, 스캐너 등과 통신 시에 사용되었다.

--- 

## 동기(Synchronous)식 통신 / 비동기(Asynchronous)식 통신
동기식 통신과 비동기식 통신의 가장 큰 차이는 **클럭(clock) 신호의 유무**이다. 

**<span style="background-color:Pink">동기식 통신</span>**은 동시에 시스템을 작동시키기 위해
이러한 신호 주기로 보내겠다는 클럭신호에 따라서 그에 맞게 데이터를 전송하는 방법이다.
따라서 data를 통신하기 위한 선 외에도 클럭 주기를 맞추기 위한 선이 하나 더 필요하다.  
연결된 장치 사이에는 지속적으로 클럭신호가 이동하고 있으며 데이터의 전송이 없을 때에도 클럭신호는 계속해서 주고 받는다.
하나의 클럭마다 사용자가 정해놓은 일정한 데이터 비트를 송수신 하는 방식으로 데이터를 주고 받는다.  
동기 통신의 경우 서로 start bit와 같은 신호가 필요없이 데이터만 보내면 되기 때문에 전송 속도가 빠르다.

**<span style="background-color:PowderBlue">비동기식 통신</span>**은 클럭신호를 보내지 않는다.
대신 보낼 데이터가 있을 때 Start bit를 보낸 후 데이터를 전부 보낸 후에는 Stop bit를 보내게 된다.
이러한 방식으로 인해 동기 통신에 비해 전송속도가 느리다.


## 참고자료
[[아두이노 강좌] 15. Serial 통신(1) - 시리얼 통신이란 무엇인가](https://blog.naver.com/yuyyulee/220301424499)  
[RS-232, RS-422, RS-485 시리얼(직렬) 통신에 대해서 알아보자~!](https://www.dsun.kr/90)  
[시리얼 통신(Serial Communication)이란 무엇인가?](https://m.blog.naver.com/ansdbtls4067/220886156177)  
[병렬 통신 - 나무위키](https://namu.wiki/w/%EB%B3%91%EB%A0%AC%20%ED%86%B5%EC%8B%A0)  
[병렬 통신 - 위키백과](https://ko.wikipedia.org/wiki/%EB%B3%91%EB%A0%AC_%ED%86%B5%EC%8B%A0)  
[통신방식의 비교](https://powerdeng.tistory.com/11)  

