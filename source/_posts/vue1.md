---
title: v-for 에서 이벤트 처리
categories:
  - Development
  - Vue.js
tags:
  - vue.js
date: 2019-07-20 12:46:29
---


![고양이는 실리콘 고양이가 있어요](/image/myCat.JPG)

웹 프로젝트 중 헤더부분 아이콘배치를 v-for문을 이용해서 반복문 처리하려는데 이벤트 처리부분이 문제가 됬다.

{% codeblock %}
<v-btn
  v-for="btnItem in btnItems"
  icon
  :title="btnItem.title"
  :key="btnItem.title">
  <v-icon @click="btnItem.clickAction">{{ btnItem.icon }} </v-icon>
</v-btn>
{% endcodeblock %}

반복문 안에서 각 버튼별로 `@click="btnItem.clickAction"` 에 다른 메소드를 실행시켜야 되는데 데이터 안에 메소드가 들어가 있는 것을 본적이 없었다.

될것같은데 생각처럼 안됬다. 구글링하니 해결책도 쉽게 나오지않았다.

생각보다 시간이 걸렸는데 해놓고 보니 역시 들인 시간에 비해 간단했다.

{% codeblock %}
export default {
  data() {
   return {
    btnItems: [
       {
         title: "Bookmark",
         clickAction: () => {
           this.favorite();
         },
         icon: "bookmark"
       },
       {
         title: "translate",
         clickAction: () => {
           this.trans();
         },
         icon: "g_translate"
       }
     ]
   };
  },
  methods:{
    favorite(){},
    trans(){}
  }
}
{% endcodeblock %}

function() 을 사용하면 함수 안에 this가 가리키는게 뷰가 되므로 에로우 펑션을 쓰던지 함수 밖에서 this를 다른 변수에 선언하고 사용해야된다.

에로우 펑션이 익숙하지 않아서인지 지금봐도
`clickAction: () => { this.favorite(); }` 부분은 어색하다.

이 방식으로 라우터 이동도 메서드로 내려서 이벤트를 모두 반복으로 처리할수 있었다.
