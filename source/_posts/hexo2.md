---
title: hexo README.md 추가하기
categories:
  - Development
  - Hexo
tags:
  - hexo
date: 2019-06-30 19:29:38
---


![2019-03-30 18:23 토요일](/image/saturdayAfternoon.JPG)

## Hexo README.md 파일 추가하기

깃에 블로그에 대한 README 파일을 남기고 싶었다.

처음엔 단순히 public 폴더안에 README.md 파일을 만들고 deploy 하면 되겠지 했는데

핵소에선 public 폴더안 생성물은 generate 때마다 source폴더 내용물을 기반으로 갱신되면서 README파일이 삭제되는 문제가 있었다.

그렇다고 source폴더에 README.md를 만들면 generate 할때 html로 렌더링해버린다.


찾아보니 다행이 _config.yml에 랜더링을 제외하는 설정이 있었다.

_config.yml 에 `skip_render: README.md`를 추가해주고 source폴더에 README.md 파일을 넣는것으로 해결되었다.
