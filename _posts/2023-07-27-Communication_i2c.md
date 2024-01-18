---
title: "[I2C] I2C 통신이란??"
date: 2023-07-27 15:00:00 +0900
categories: [Communication Protocol, Serial]
tags: [Communication Protocol, Serial, I2C]  # TAG names should always be lowercase
---

## 1. I2C란?
I2C
  : Inter-Integrated Circuit의 약자, "아이 투 씨"라고 흔히 말하지만 정식 명칭은 "아이 스퀘어 씨"이다.  
  두개의 선을 이욯한 통신으로 TWI(Two Wire Interface)라고도 불린다.

**I2C는 데이터 통신을 위한 선(SDA)**과 **송수신 타이밍 동기화를 위한 클럭 선(SCL)**으로 구성되어 있다.  
하나의 마스터(Master)와 하나 이상, 이론상 최대 127개의 슬레이브(Slave)로 이루어진다.  

![i2c circuit](/assets/img/post_img/i2c_circuit.png)
_I2C Circuit 그림 [출처: [엔지니어스-Engineeus](https://mickael-k.tistory.com/184)]_

데이터 송수신은 마스터에서 주도하며 데이터를 송수신 하기 전 **반드시 슬레이브의 주소를 명시한 후에 통신을 시작**해야 하기 때문에 찗은 데이터 통신에 주로 사용된다.
> ❔ **Master / Slave**
>> 마스터/슬레이브는 장치나 프로세스**(마스터)**가 하나 이상의 다른 장치나 프로세스**(슬레이브)**를 통제하고 통신 허브 역할을 하는 **비대칭 통신 및 제어 모델**을 의미한다.

---
## 2. I2C 통신을 위한 조건  
위 그림에서 유의해야 할 정보는 Rp로 표기된 **풀업 저항**이다. 통신을 위해서는 기본적으로 SDA와 SCL선이 모두 High 상태여야 하기 때문에 풀업 저항을 통해 High 상태를 만들어 주는것이 중요하다.  
하지만 아두이노와 같은 보드 사용시 내부 풀업저항을 사용하기 때문에 직접 달 필요는 없다. *(찾아본 결과 라즈베리파이 역시 내부 풀업저항이 있는 것으로 보임)*

> ❔ **풀업 저항**
>> 먼저 **플로팅(Floating)**에 대해 알아야 한다. 아래 그림상에서 왼쪽의 경우 input에 0의 값이 입력되는데 오른쪽의 경우 전압이 입력되지 않는다.
그렇다면 이 경우 input이 high인지 low인지 알 수 없고 이러한 상황에서는 작은 노이즈에도 high low 사이를 빠르게 왔다갔다 하기 때문에 오작동을 유발할 수 있다.
![pull-up_resistance](/assets/img/post_img/floating.png)
_Floating 설명 그림[출처: [[기초 지식] 풀업 저항이란? (Pull-Up저항이란)](https://blog.naver.com/jamduino/220820935325)]_  
따라서 대부분 이러한 Floating을 방지하기 위해 풀업저항을 사용해 inputdp 전압을 입력시키는 것이다.  
![pull-up_resistance](/assets/img/post_img/pull-up_resistance.png)
_Pull-up 저항 그림 [출처: [풀업저항](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=emperonics&logNo=221697492619)]_  
이와 유사하게 **풀다운 회로**도 존재하는데 이는 풀업과는 반대로 GND 쪽에 저항을 연결하는 것을 말한다.

---
## 3. I2C 통신 방식  
시리얼(UART) 통신과 비교했을 때 I2C통신은 동기화 통신 방식이라는 차이가 있다. 동기화 통신 방식이란 Clock 신호를 이용해서 데이터의 전송 타이밍을 맞추기 때문에 
시리얼 통신처럼 통신 속도가 따로 정해지지 않아도 된다는 장점이 있다. SPI 통신 역시 동기화 통신안데 송신과 수신이 동시에 가능하다는
장점이 있지만 MISO, MOSI, SCK, CS 총 4개의 선이 필요하기 때문에 여러개의 슬레이브 연결 시 좀 더 복잡하기 때문에 불편한 점이 있다.

> ❔ **클럭(Clock) 신호**
>> 논리상태 H(high,논리 1)와 L(low,논리 0)이 주기적으로 나타나는 방형파(square wave) 신호로 음악에서 사용되는 메트로놈과 유사하게 동작하는 타이밍을 제어하기 위해 필요한 것이다. 

I2C 통신은 **시작 신호, 데이터 신호, 정지 신호**로 이루어진다.

![I2C Timing Diagram](/assets/img/post_img/i2c_timing_diagram.png)
_I2C 통신방식 [출처: [Wikipedia - I2C](https://en.wikipedia.org/wiki/I%C2%B2C)]_  

그림에서 볼 수 있듯이 SDA와 SCL 모두 High 상태가 기본값이고 이후 **SDA 신호가 Low로 떨어질 때를 시작신호**로 받아들인다.
이후 SCL 선으로 클럭신호를 만들게 되고, 
<span style="color:white; background-color:RoyalBlue">클럭 신호가 Low일 때가 SDA 신호를 비트신호로 바꾸는 시간(파란색 부분)</span>, 
<span style="color:white; background-color:LimeGreen">클럭 신호가 High일 때가 SDA신호를 읽는 시간이 된다.(녹색 부분)</span> 
이러한 비트신호로 바꾸고 읽는 과정을 반복하는 것이다.  
<span style="color:OrangeRed">**한 클럭에 한 비트씩**</span>  데이터 신호를 만들고, 
모든 데이터 전송이 끝난 이후 **SCL 신호가 High가 되면 SDA 신호 역시 High로 만들어 정지신호**를 만든다.

시작신호 이후 나오는 첫 7비트는 슬레이브이 주소값이고 8번째 비트의 경우 데이터를 읽어오는 신호인지, 쓰기 위한 신호인지를 나타내는 비트이다.

---
## 4. 신호의 읽기/쓰기
슬레이브의 주소 값과 읽기/쓰기 비트의 경우 **마스터에서 생성**할 수 있으며 **'쓰기'일 경우 마스터에서 데이터를 생성**, **'읽기'일 경우 슬레이브에서 데이터를 생성**한다.  
8비트 데이터 전송 후에는 슬레이브에서 **응답신호(ACK)**를 만들어 수신을 확인해준다. 아래 그림을 참고하자.  
![I2C Data write/read](/assets/img/post_img/i2c_data_rw.png)
_I2C 데이터 쓰기, 읽기 [출처: [[아두이노 강좌] 29. I2C 통신 (1) - I2C 통신이란 무엇인가](https://blog.naver.com/yuyyulee/220323559541)]_  

응답신호는 기본적으로 Low값을 가지며, 만약 슬레이브가 데이터를 전송 시 모든 데이터의 전송이 끝난 경우 High 상태가 된다. 이를 **NACK**라고 하는데
이 외의 경우에 NACK 발생 시 통신 에러 혹은 데이터 에러의 경우이다.

대부분의 칩에서 I2C 통신은 하드웨어 기능으로 구성되어 있어서 I2C 관련 레지스터의 비트를 설정하는 것 만으로도 시작, 데이터, 클럭, 정지 신호를 출력할 수 있다.  
(아두이노는 Wire라는 라이브러리를 제공해 더 쉽게 이용 가능하다고 한다.)

---
## 참고자료
[위키백과 - 마스터/슬레이브(기술)](https://ko.wikipedia.org/wiki/%EB%A7%88%EC%8A%A4%ED%84%B0/%EC%8A%AC%EB%A0%88%EC%9D%B4%EB%B8%8C_(%EA%B8%B0%EC%88%A0))  
[엔지니어스-Engineeus - I2C란?(엄청 쉽게 설명)](https://mickael-k.tistory.com/184)  
[[아두이노 강좌] 29. I2C 통신 (1) - I2C 통신이란 무엇인가](https://blog.naver.com/yuyyulee/220323559541)  
[풀업저항](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=emperonics&logNo=221697492619)  
[[기초 지식] 풀업 저항이란? (Pull-Up저항이란)](https://blog.naver.com/jamduino/220820935325)  
[위키백과 - 클럭신호](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9F%AD_%EC%8B%A0%ED%98%B8)  
[정보통신기술용어해설 - 클럭](http://www.ktword.co.kr/test/view/view.php?m_temp1=1509)