---
title: 포스팅 연습하기
date: 2023-07-07 15:17:00 +0900
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [practice]     # TAG names should always be lowercase
---

# VS Code로 마크다운 문서 작성하기
## Visual Studio Code

Visual studio Code에서 Markdown Preview도 지원한다.

## 글씨체 변환

- **볼드체1** __볼드체2__

- _이탤릭_

- ***볼드+이탤릭***

- ~~취소선~~

- <u>밑줄</u>

- <u>~~***중복사용도 가능!***~~</u>

---
#### 참고
Enter는 
한번이 아닌

두번쳐야 줄바꿈이 된다

원래는 띄어쓰기 두번으로도 가능하나 Chirpy Theme에서는 지원하지 않는다.

---
줄 삽입

## 코드 블럭
```
코드삽입 Code Code 
'(작은 따옴표)가 아니라 `(백틱)이다!
```
백틱 적은 후에 해당 코드블럭이 어떤 언어인지 적어주면 코드 하이라이팅이 가능

```python
import os
print("Hello World!")
```

---
## 리스트

### 순서가 있는 리스트
1. 순서가 있는
2. 리스트는
3. 번호로!

### 순서 없는 리스트
- 순서가
- 없는 리스트는
- "*,+,-" 로 가능!

---
## 할 일

- [ ] 안했음!
- [x] 했음!

---
## 설명

Sun
  : the star around which the earth orbits

---
## 인용구

> "신은 죽었다" -니체
>> 들여쓰기도 된다
>>> 또 된다
>>>> 또또 된다

---
## 링크
Github 홈페이지 : <https://github.com>

[Github](https://github.com)

마우스 오버시 설명문 출력 : [Github](https://github.com "마우스 오버시에 출력되는 설명문!")

[현재 페이지 초반 부분으로 이동](#visual-studio-code)

현재 페이지 내에서 이동하는 것 관련
1. header를 링크로 잡고 특수문자를 지운다.
2. 가장 앞 부분에 #을 하나만 넣는다
3. 스페이스 바 부분은 모두 “-“으로 바꾼다
4. 영어 대문자는 모두 소문자로 바꾼다 
    - 예) “## 마크다운(Markdown) 기본문법” -> “#마크다운markdown-기본문법”

---
## 이미지 삽입
내 아바타 사진

![내 아바타 사진](https://github.com/ibin-study/ibin-study.github.io/blob/main/assets/img/profile.jpg)
