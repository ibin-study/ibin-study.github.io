---
title: "[Error] Failed building wheel for numpy 등 pip3로 설치 시 에러 해결"
date: 2023-08-11 13:00:00 +0900
categories: [Trouble shooting, Error]
tags: [Trouble shooting, Error]  # TAG names should always be lowercase
---
Python3 버전을 새로 깐 후에 기본 버전을 변경하니 Numpy가 설치되어있지 않았다. 따라서 Numpy를 설치하기 위해
```pip3 install numpy``` 명령어를 실행 시   
**Failed building wheel for numpy**등 여러 에러가 발생했다.
이 오류를 해결하기 위해 찾아본 결과 pip의 업그레이드가 필요하다는 얘기가 있었다.

> 💡 pip란?
>> 파이썬으로 작성된 패키지 라이브러리를 설치 및 관리해주는 시스템. Ubuntu에서 apt-get, CentOS의 yum과 유사한 개념이다.  
그냥 pip의 경우 python2 버전이고 python3 버전에 설치하기 위해서는 pip3를 사용해야 한다. 

```shell
pip3 install --upgrade pip
```
위 명령어를 입력하니 pip3가 업그레이드가 되었고, 다시 ```pip3 install numpy``` 실행 시 정상적으로 설치가 되었다.


## 참고자료
[Stack overflow - How to upgrade pip3?](https://stackoverflow.com/questions/38613316/how-to-upgrade-pip3)  
[파이썬(PIP) numpy, pandas, matplotlib 설치 실패(에러) 해결 방법](https://archivers.tistory.com/669)  