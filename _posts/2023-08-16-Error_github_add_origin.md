---
title: "[Error] fatal: not a git repository (or any of the parent directories): .git 해결"
date: 2023-08-16 17:00:00 +0900
categories: [Trouble shooting, Error]
tags: [Trouble shooting, Error]  # TAG names should always be lowercase
---
Github 활용해서 Repository에 파일을 추가하려고 했는데 ```git remote add``` 명령어 사용시  
**fatal: not a git repository (or any of the parent directories): .git** 에러가 발생했다.

오류의 발생 원인은 현재 add하려고 하는 폴더에 git에 대한 정보를 담은 파일이 없기 때문이었다. 매우 간단하게 해결 할 수 있다.

```shell
$ git init
$ git remote add origin [repository 주소] 
```

위와 같이 ```git init``` 명령어 입력 이후 ```git remote add``` 명령어를 사용하면 에러가 발생하지 않는다,


## 참고 자료
x