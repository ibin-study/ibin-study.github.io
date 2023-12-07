---
title: "[Markdown] Chirpy github blog에서 Markdown 수식 사용하기"
date: 2023-12-06 14:00:00 +0900
categories: [Github, Markdown]
tags: [Markdown]     # TAG names should always be lowercase
use_math: True
---


## 서론
> Markdown 문법을 활용해 블로그를 작성하다 보니 수식이나 그리스 문자를 입력해야 할 경우가 생겼다.  
> 이런 경우에 참고할 수 있는 자료를 만들기 위해 블로그에 정리해 두려고 한다.  
> 그리 간단하지 않은 것 같다...😫

## 기본 설정
블로그 글을 Markdown 형식으로 작성하는 거라 당연히 그냥 Markdown 수식 사용방법과 동일하게  
달러 표시하면 되는 줄 알았지만 그게 아니었다.  
이 블로그는 Jekyll Github 블로그이기 때문에 수식 표시를 위해서는 **Mathjax**를 사용해야 한다...😑  
그냥 $만 붙이면 되는 줄~

### config.yml 파일 수정
먼저 모든 블로그에 있는 **_config.yml** 파일을 열어서 수정해주어야 한다.
```
# Math equation
markdown: kramdown
highlighter: rouge
lsi: false
excerpt_separator: "\n\n"
incremental: false
``` 
위에 기술된 인자가 있다면 맞게 수정해 주면 되고, 현재 내가 사용중인 Chirpy 테마의 경우 위 내용이 아예 없어서 복붙해서 추가해 주었다.
```ctrl + F``` 로 찾아보고 넣는 것을 추천한다.

### Mathjax 사용을 위한 include 파일 생성
포스트 작성 시 달러표시와 같은 수식 문법이 실제 웹에서 구현될 수 있게끔 하기 위해 html 스크립트를 설정해 주어야 한다.  
**_includes 폴더** 안에 **"mathjax_support.html"**이라는 파일을 만들어 준다.  
그 파일 안에 아래 내용을 복붙한 뒤 저장한다.

```html
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        TeX: {
          equationNumbers: {
            autoNumber: "AMS"
          }
        },
        tex2jax: {
        inlineMath: [ ['$', '$'] ],
        displayMath: [ ['\\[', '\\]'] ],
        processEscapes: true,
      }
    });
    MathJax.Hub.Register.MessageHook("Math Processing Error",function (message) {
          alert("Math Processing Error: "+message[1]);
        });
    MathJax.Hub.Register.MessageHook("TeX Jax - parse error",function (message) {
          alert("Math Processing Error: "+message[1]);
        });
</script>
<script type="text/javascript" async
    src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```
여기서 **inlineMath** 의 경우  
```$x+y=a$``` 와 같이 사용하고 그 결과물은 $x+y=a$ 처럼 나온다.  
**displayMath** 의 경우 ```\\[x+y=a\\]``` 와 같이 사용하고  
\\[x+y=a\\] 와 같이 수식이 글 중앙에 나온다.  

>  😫😫😫 Chirpy의 경우 ```$$ ~~~ $$``` 로 displayMath를 하고자 할 경우 ```\(x+y=a\)```와 같이 출력된다.  
~~Chirpy의 문제인 것인지 다른 문제인지는 확실하지 않지만 다른 theme의 블로그에서는 잘 되는 것을 보면...~~  
따라서 달러모양만으로 적용을 하기 위해 displayMath를 ```\(~~~\)```로 주어도  
달러 입력시 수식이 출력되지 않았다. 달러 2개만 따로 사용시 달러로 잘 출력이 되지만  
```$$x+y=a$$```처럼 사용 시 **$$x+y=a$$** 처럼 출력된다. (지금 달러 2개 친거임...)  
문제의 원인은 아직 찾지 못했다...  

> 또한 ```\[\]``` 나 ```\(\)```를 사용 시 그냥 []와 ()를 입력해도 수식으로 인식하는 경우가 생겼다.  
이 역시도 정확히 문제를 찾지 못해 일단 현재로써는 ```\\[ \\]``` 방식을 사용할 예정이다.  
>> Github blog는 어렵구나... 😭


### mathjax_support.html을 _layout에 포함시키기
위와 같이 html을 만들었다면 이것을 레이아웃에 포함시켜주어야 적용이 된다.  
**_layouts 폴더** 내에서 post와 관련이 있는 파일**(ex. post.html)**을 찾아서 수정해 주어도 되나,  
Chirpy의 경우 다른 사람들의 사례와 좀 다른것 같아 보였다. ~~(골칫덩어리네..)~~  
html 관련해서 아는 것이 없는 상태에서 괜히 건드리기 무서워서 필자의 경우
**_includes 폴더에 있는 head.html** 파일을 수정해 주었다.

![head파일에 삽입할 코드](/assets/img/post_img/Markdown_head.png)
_head파일에 삽입할 코드_

위 내용을 헤드 파일 사이에 넣어주면 된다.
```html
<head>
~~~
</head>
```

### 포스트 작성 시 적용
처음 포스팅 시 맨 위에 아래와 같은 코드를 적어준다.
```md
---
title: "제목"
date: 2000-00-00 00:00:00 +0900
categories: [카테1, 카테2]
tags: [태그 1, 2, ...]     # TAG names should always be lowercase
---
```
이제 수식 코드를 사용하기 위해선 위와 같은 코드에 **"use_math: true"**를 추가하면 된다.

```md
---
title: "제목"
date: 2000-00-00 00:00:00 +0900
categories: [카테1, 카테2]
tags: [태그 1, 2, ...]     # TAG names should always be lowercase
use_math: true
---
```
이렇게 할 경우 LaTex 수식 코드를 사용하기 위한 모든 세팅이 끝난다!

원래는 수식 코드들을 정리하기 위해서 만들려고 했으나 내용이 너무 길어질 것 같아  
이는 다음 포스팅에 정리할 예정이다.


## 참고자료
[github.io에 마크다운 작성 및 수식 입력하기](https://junia3.github.io/blog/markdown)  
[[GitHub] Github 블로그 수식 추가 (kiko-now)](https://m.blog.naver.com/PostView.naver?blogId=prt1004dms&logNo=221525385428&proxyReferer=)  
[[BoostCamp AI Tech 심화포스팅] Jekyll Blog와 MathJax](https://cow-coding.github.io/posts/githubblog/)  

