---
title: VirtualBox 에러 (0x80004005)
categories:
  - Development
  - etc.
tags:
  - vm
date: 2021-01-26 20:40:26
---



![2021-01-23 광진교 _ 한강이 건조하게 얼어붙었다.](/image/gangdong_gwangjingyo.jpg)

미뤄뒀던 토이프로젝트 시작하려고 예~전에 설치해둔 VirtualBox를 켜서 vm을 실행시키니 다음과 같은 에러가 발생했다.

*the virtual machine 'ubuntu01' has terminated unexpectedly during startup with exit code 1 (0x1) 
E_FAIL (0x80004005)*

구글링해보니 재설치를 하라, 하위버전을 설치해보라 여러 해결책이 나왔지만 재설치를 해도, 버전을 낮춰도 계속 같은 에러가 발생했다.

삽질하다 재설치를 해도 어딘가에 기존 설정이 남아있는 느낌이 강하게 들었다.

다시 삭제하고 찾아보니 `C:\Users\계정\.VirtualBox` 에 네트워크 설정등으로 보이는 파일들이 잔류해있었다.

.VirtualBox 폴더를 지우고 다시 최신버전으로 설치해보니 잘 되었다.

이상한데서 힘뺐다..


시작이 반이랬다. 오늘은 VM설치해서 만족한다.

