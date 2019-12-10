---
title: Vue.js 배열 데이터 변경
categories:
  - Development
  - Vue.js
tags:
  - vue.js
date: 2019-07-23 20:36:06
---



![2019-05-19 시즈오카 이즈시 _ 소도시 여행은 소소한 것들도 기억에 남았다.](/image/sizuoka_trafficLight.JPG)

프로젝트 중 팀원의 컴포넌트에서 데이터가 앞뒤로 콘솔 찍어봐도 분명히 바뀌는데 화면이 갱신되지 않는 문제가 있었다.

검색결과 배열이 문제였다.

> #### Vue는 감시중인 배열의 변이 메소드(push, pop, shift, unshift, splice, sort, reverse)를 래핑하여 갱신을 트리거 한다.

JavaScript의 제한으로 인해 Vue는 배열에 대해 다음과 같은 변경 사항을 감지할 수 없다.

- 인덱스로 배열에 있는 항목을 직접 설정하는 경우
- 배열 길이를 수정하는 경우

때문에 직접 설정하려면 다음과 같이 써야한다.

{% codeblock %}
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)

// Array.prototype.splice
example1.items.splice(indexOfItem, 1, newValue)
{% endcodeblock %}

출처: [https://ksh-code.tistory.com/27](https://ksh-code.tistory.com/27) [알고리즘을 좋아하는 나]


문제의 부분은 v-for 에서 배열의 내용을 인덱스로 접근해 바꿔주는 부분이였고 아래와 같이 해결했다.

{% codeblock %}
export default {
  data() {
    return {
      show: [false, false, false, false]
    }
  },
  methods: {
    chageIcon(index) {
      // this.show[index] = !this.show[index]
      this.$set(this.show, index, !this.show[index]);
    }
  }
}
{% endcodeblock %}
