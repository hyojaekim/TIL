# [ETC](https://github.com/hyojaekim/TIL/tree/master/Javascript) / [🏠 Home](https://github.com/hyojaekim/Javascript)

## 스크립트의 위치

`<script> 블라블라 </script>`

위 같은 스크립트는 head 태그 안에 넣는 것이 정석이라고 한다.
요즘에는 body 태그 맨 아래에 스크립트를 넣는다. 왜 <body> 태그 맨 아래줄에 넣을까?

### 첫번째.

HTML은 위에서부터 차례대로 읽게 된다. 스크립트가 head 태그 안에 있는 경우, html을 읽기 전에 스크립트를 먼저 읽게 된다면, 스크립트를 읽는 동안 유저 입장에서는 화면이 그려지지 않고 하얀 화면이 나오게 된다. 만약 스크립트의 덩치가 커진다면, 유저는 바로 뒤로가기를 누를 가능성이 높다. 그래서 약간의 눈속임을 하려고..?

### 두번째.

`<h1>제목</h1>`

위 같은 제목을 빨간색으로 바꾸는 스크립트가 존재한다고 가정하자.
head 태그에 스크립트가 있으면, 아래 HTML을 읽기 전에 모두 읽을때 까지 기다리는 코드를 작성해야 한다.

이와 같은 이점으로 스크립트는 body 태그 안에서 맨 아래에 추가하자!



### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Javascript/js_position.md#ETC---home)
