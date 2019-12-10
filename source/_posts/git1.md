---
title: Git 원격 저장소 여러개 연결하기
categories:
  - Development
  - etc.
tags:
  - git
date: 2019-07-02 21:32:29
---


![2019-03-31 13:56 아파트 벚꽃](/image/aptCherryBlossom.jpg)

## Git 원격 저장소 여러개 연결하기

원격저장소를 한개씩만 써봤는데 깃랩과 깃허브 두개를 연동할 일이 생겨서 구글링하고 정리했다.

`git remote add "저장소명" "url"`

형태로 add 만 붙여주면 됬다


깃허브에서 로컬로 클론해온 후 깃랩과 연동하는 과정을 나열해보면

`git clone https://github.com/NobleTuna/example.git`
깃허브에서 로컬로 클론, 이 경우 저장소 명은 origin 이 된다

`cd example`
프로젝트 폴더로 이동

`git remote add gitLab https://lab.tmp.com/NobleTuna/example.git`
깃랩에 생성해둔 example 저장소를 gitLab 으로 명시하고 연결

`git remote -v`
원격 저장소 목록을 확인하는 명령어

{% codeblock %}
gitLab https://lab.tmp.com/NobleTuna/example.git(fetch)
gitLab https://lab.tmp.com/NobleTuna/example.git(push)
origin https://github.com/NobleTuna/example.git(fetch)
origin https://github.com/NobleTuna/example.git(push)
{% endcodeblock %}
명시하지 않은 저장소 origin 과 명시하고 추가한 gitLab 저장소 확인 가능

이후 push 나 pull 할 경우 각각 저장소를 명시하면 된다.

`git pull origin master`
origin(깃허브)에서 pull

`git push gitLab master`
gitLab(깃랩)으로 push

반대의 경우도 같다.

push를 하기위에 두번씩 치기 귀찮을 경우 [stackoverflow](https://stackoverflow.com/questions/849308/pull-push-from-multiple-remote-locations/3195446#3195446)를 참고


추가로 원격저장소 주소를 변경하는 경우
`git remote set-url "저장소명" "새로운URL"`

원격저장소 명시한 이름을 변경하는 경우
`git remote rename "현재저장소명" "새로운저장소명"`
