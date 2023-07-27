---
title: "[Markdown] Markdown 포스팅 연습하기"
date: 2023-07-21 14:00:00 +0900
categories: [Github, Markdown]
tags: [Markdown]     # TAG names should always be lowercase
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

- ***~~<u>중복사용도 가능!</u>~~***

- <u>***~~태그를 먼저 쓰면 적용이 안된다!~~***</u>


### 참고
Enter는 
한번이 아닌

두번쳐야 줄바꿈이 된다

~~원래는 띄어쓰기 두번으로도 가능하나 Chirpy Theme에서는 지원하지 않는다.~~  
문장 끝에 두번 띄어쓰기로도 줄바꿈이 가능하다.

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
## Todo list

- [ ] 안했음!
- [x] 했음!

---
## 설명 형식

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

![내 아바타 사진 링크로](https://raw.githubusercontent.com/ibin-study/ibin-study.github.io/main/assets/img/profile.jpg){: w="300" h="200" }
_링크로 사진 삽입_

![내 아바타 사진 파일경로로](/assets/img/profile.jpg){: w="300" h="200" }
_파일 경로로 사진 삽입_

---
## 표 만들기

|제목|내용|설명|
|------|---|---|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|

### 텍스트 정렬
> :문자로 표의 텍스트를 정렬할 수도 있음

|제목|내용|설명|
|:------|---:|:---:|
|왼쪽정렬|오른쪽정렬|중앙정렬|
|왼쪽정렬|오른쪽정렬|중앙정렬|

### 셀 확장

|제목|내용|설명|
|:---|:---:|---:|
||중앙에서확장||
|||오른쪽에서 확장|
|왼쪽에서확장||

---
## 글씨 편집

![RGB 색상표](/assets/img/post_img/RGB_colortable.png)
_RGB 색상표_

### 글씨에 색깔 넣기

<span style="color:red">빨간색</span>
<span style="color:blue">파란색</span>
<span style="color:green">초록색</span> 등등등...

### 형광펜

<span style="background-color:red">빨간색</span> 
<span style="background-color:blue">파란색</span>
<span style="background-color:green">초록색</span>

### 폰트 사이즈 조절

<span style="font-size:300%">폰트 사이즈 300%</span> 

<span style="font-size:100%">폰트 사이즈 100%</span> 

<span style="font-size:50%">폰트 사이즈 50%</span> 

### 동시에 적용

```markdown
<span style="~; ~~; ~~~;">--내용--</span> 형태로 사용하면 된다.
```

<span style="color:red; background-color:yellow; font-size:150%">
이런식으로 동시에 적용할수도 있다!!
</span>

### <span style="color:red; background-color:yellow; font-size:150%">제목에도 적용가능!!</span>

---
## Emoji 활용
🙂 😱 ⏰ 👍 👍🏻 👍🏼 👎 🖕

> 이렇게 copy & paste로 사용은 되나 markdown 문법(ex. :+1:)으로는 되지 않았다.

> 찾아보니 jekyll에서 emoji 사용을 위해서는 플러그인 설치가 필요하다.

[jekyll/jemoji](https://github.com/jekyll/jemoji)

그냥 ```window키 + .```을 눌러서 나오는 이모지를 사용하는것이 편리할 것 같다...🤔

추가적으로 필요한건 copy & paste 하는걸로...🤷‍♂️