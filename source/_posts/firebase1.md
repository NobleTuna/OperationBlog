---
title: Firebase 'auth/account-exists-with-different-credential' 에러 처리
categories:
  - Development
  - Firebase
tags:
  - firebase
date: 2019-07-15 20:35:58
---


![2019-05-19 야마나시 모토스 호수 _ 날씨가 좋았으면 구름대신 후지산이 보였을텐데](/image/shizuoka_motosu.jpg)

웹 프로젝트를 진행하면서 Firebase로 서버를 구현중에 로그인 중복처리 문제가 있었다.

구글계정으로 회원가입이 되어있는데 같은 이메일 주소의 페이스북으로 가입하려면 `auth/account-exists-with-different-credential` 에러가 발생한다.

당연한 에러긴 한데 Firebase 완전한 해결 메서드를 제공하지 않아서 linkWithCredential메서드를 이용해 처리해야한다.

구글링을 해서 어찌어찌 해결되나 싶더니 팝업관련 에러가 난다.

페이스북 로그인창에서 또 팝업창을 요청하니 브라우져에서 막아 발생하는 에러였다.

Firebase 에서 Redirect 방식의 로그인처리를 지원해주었기 때문에 이걸로 해결했다.

필요시 사용자에게 계정 연결 안내 메시지를 띄워주면 되겠다.


Swal.fire는 SweetAlert2 라는 alert를 예쁘게 해주는 외부 라이브러리니 신경쓰지 않아도 된다.


{% codeblock %}
loginWithFacebook() {
    var provider = new firebase.auth.FacebookAuthProvider();
    return firebase.auth().signInWithPopup(provider).then(function(result) {
      let accessToken = result.credential.accessToken
      let user = result.user
      return result
    }).catch(function(error) {
      if (error.code === 'auth/account-exists-with-different-credential') {
        firebase.auth().fetchSignInMethodsForEmail(error.email).then(function(providers) {
          if (providers[0] == 'google.com') {
            var provider = new firebase.auth.GoogleAuthProvider();
            // popup 에러때문에 리디렉 signInWithRedirect
            firebase.auth().signInWithRedirect(provider).then(function(result) {
              firebase.auth().signInWithCredential(result.credential).then(user => {
                user.linkWithCredential(error.credential)
              }).catch(function(e) {
              })
            }).catch(function(e) {
            })
          }
        })
      } else {
        Swal.fire({
          title: 'Error!',
          text: '예기치 않은 문제가 발생했습니다. 관리자에게 문의바랍니다. ErrorCode : ' + error.code,
          type: 'error',
          confirmButtonText: 'Ok!'
        })
      }
    })
  }

{% endcodeblock %}
