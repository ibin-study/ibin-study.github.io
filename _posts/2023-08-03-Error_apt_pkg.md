---
title: "[Error] ModuleNotFoundError: No module named 'apt_pkg' 에러 해결"
date: 2023-08-03 10:00:00 +0900
categories: [Trouble shooting, Error]
tags: [Trouble shooting, Error]  # TAG names should always be lowercase
---
아마도(?) python 버전 변경 후에 ```sudo apt update```나 ```sudo apt install ~~``` 명령어를 사용시   
**ModuleNotFoundError: No module named 'apt_pkg'** 에러가 발생했다.

```shell
sudo apt-get install python3-apt --reinstall
cd /usr/lib/python3/dist-packages
sudo cp apt_pkg.cpython-36m-aarch64-linux-gnu.so apt_pkg.so
```

36m과 aarch64 부분은 개개인마다 차이가 있을 것이다.  
암튼 파일 명칭을 **apt_pkg.so**로 변경 시 해결이 되었다.

## 참고자료
[ImportError: No module named apt_pkg 해결](https://velog.io/@choi-yh/ImportError-No-module-named-aptpkg-%ED%95%B4%EA%B2%B0)