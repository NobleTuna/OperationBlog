---
title: coinbase가 자동으로 바뀌는 문제
categories:
  - Development
  - BlockChain
tags:
  - blockchain
  - ethereum
  - geth
date: 2019-08-29 22:58:56
---


![2019-08-17 구시포 해수욕장 _ 날씨가 흐리고 사람도 적었다.](/image/gushipo.jpg)

블록체인 프로젝트 중에 coinbase가 자동으로 바뀌는 문제가 있었다.

AWS에 채굴노드 2개와 통신노드 1개로 이더리움 프라이빗 네트워크를 구축하고 채굴노드 2개를 백그라운드로 채굴시켜놨는데 자고일어났더니 노드 3개 전부다 코인베이스가 변경되 있던것

심지어 AWS노드 3개에는 없는 계좌였다.

팀원중에도 접속한사람이 없다고 하니 내가 뭔가 잘못했겠지 하고 3개다 통신노드의 0번계좌로 바꿔놓았는데 점심먹고 보니 다시 아까 그 계좌로 전부 바뀌어있다.

구글링 결과 내린 결론은 누군가 열어놓은 RPC 통신으로 접속해 계좌를 만들고 코인베이스를 변경해놓은것..
geth를 재구동 시키는 경우가 아니라면 자동으로, 심지어 없는 계좌로 코인베이스가 바뀌는 사례는 외부접속에 의한 것 뿐인것 같았다.

개발중 편의를 위해서 채굴노드의 통신을 열어놓은게 문제였다.

누군가 장난으로 바꿔놓았다기엔 팀원 외에 통신 주소를 알려준 사람이 없었다.
아마도 RPC 포트가 열려있는 geth를 타겟으로 무작위로 아이피를 바꿔가며 코인베이스를 변경하는 나쁜 사람들이 있는것 같다.
다음날 옆조에서도 같은 일이 발생했다.

해결책은 간단했다.
채굴노드의 백그라운드 실행시 rpc 통신을 빼고 구동시키는것
이틀째 문제없는 것을 보니 실제로 외부에서 누군가 접속한건 맞는것 같다.

단 일단 구동하면 계속 채굴하니 개발단계에서 불필요한 채굴로 난이도가 올라가는 문제가 있긴 하지만 현재는 이게 최선인것 같다.

깃헙에서 빌드되지 않은 geth 코드를 받아서 채굴난이도를 설정하는 함수부분의 리턴값을 고정시키는 것으로 난이도 상승을 막을 수 있다고 하니 나중에 해봐야겠다.