---
title: 이더리움 도메인 공부
categories:
  - Development
  - BlockChain
tags:
  - blockchain
  - ethereum
date: 2019-06-29 17:53:37
---


![2019-05-18 시즈오카 조렌폭포 옆 와사비밭](/image/sizuoka_jorenWashabi.jpg)

앞 포스팅들과 마찬가지로 난잡하다.
<hr>

### 이더리움
분산 어플리케이션(스마트 컨트랙트)을 탑재한 블록체인 2.0

분산화된 상태전이 머신
- 트랜잭션에 기반한 상태 전이
단, 이전 상태로 되돌아 갈 수 없음
- 암호화 알고리즘을 활용 -> 무작위로 상태전이가 일어나는 것을 방지
- 모든 참여자가 동일한 상태를 공유
- 블록은 해당 시점의 이더리움 상태를 나타낸다고 볼 수 있음
- 현재 블록 -> 현재 이더리움의 상태
- 최초 상태 : Genesis Block

<hr>

### 이더리움 계정의 종류
외부 소유 계정(External Owned Account)
- ETH 잔액 유지
- 개인 키를 통한 주소 관리
- ETH 전송, 컨트랙트 실행을 위한 거래 전송 가능
- 컨트랙트 코드를 가지고 있지 않음 (빈 문자열 hash 값)

컨트랙트 계정(CA Contract Account)
- ETH 잔액 유지
- 주소를 가지고 있으나 개인키는 존재하지 않음
- 컨트랙트 코드를 보유
- 거래나 메시지를 수신하면 보유하고 있는 컨트랙트 코드를 실행

<hr>

### 이더리움의 상태전이 (State Transition)
- 블록 채굴로 인한 거래 내역 추가 시 상태전이 발생
- 상태전이함수에 의해 수행

<hr>

### 트랜잭션 종류
- (외부) 트랜잭션 : 외부 소유계정에서 외부소유 계정, 외부 소유계정에서 스마트컨트랙트 까지의 트랜잭션
EOA가 다른 EOA 혹은 CA로 보내는 ‘서명된 메시지’
블록체인에 저장됨
출발지가 EOA

- 내부 트랜잭션 : 스마트컨트랙트 내부에서 진행되는 트랜잭션
CA가 다른 CA 혹은 EOA에게 전달되는 ‘서명되지 않은 메시지’
주로 컨트랙트 함수 호출에 사용
블록체인에 별도 저장되지않음
출발지가 CA

<hr>

### 블록
이더리움 장부에 기록되는 데이터의 기본 단위
트랜잭션들의 집합

<hr>

### 엉클 블록
동일한 시점에 채굴된 블록 중 채굴 난이도가 낮아 메인 체인에 연결되지 못한 블록
이더리움은 엉클 블록채굴도 보상을 줌
블록생성 시간이 빠를 수록 엉클 블록의 발생 확률이 높음

문제점
엉클블록에 포함된 트랜잭션은 승인되지 않았기 때문에 트랜잭션 처리 지연 발생
승인되지 않은 블록에 연산이 소모되어 연산량이 낭비됨
평균 블록생성 시간이 늘어나 채굴 난이도가 감소하게 되어 네트워크의 보안 수준이 낮아짐

<hr>

### 작업증명(PoW, Proof of Work)
이더리움 -> Ethash
- 채굴이 전문 채굴기에 몰리는것을 막기위한 이더리움의 작업증명
- 계산은 어렵게, 검증은 쉽게

### 지분증명(PoS, Proof of Stake)
검증자가 가진 지분에 비례한 확률로 블록 생성 권한을 획득하고 생성된 블록을 원하는 체인에 연결, 보상 획득
PoW의 문제점을 개선
- 전력 소모량, 채굴 중앙화 등
이더리움은 Casper를 통해 PoW로 전환중

### Casper FFG(Friendly Finality Gadget)
PoW + PoS 하이브리드 방식
PoW 100개 블록마다 PoS

<hr>

#### 스마트 컨트랙트 개발 언어
- Solidity : 현재 가장 많이 사용되고 있는 이더리움 스마트 컨트랙트 언어
- 하이퍼래저 패브릭이 여러 언어를 쓸 수 있는 이유 : 패쇄형 블록체인이라 언어가 다름에 따라 발생하는 과부화 위험이 적음

<hr>

### 가스
이더리움을 움직이게 하는 ‘기본 단위’
트랜잭션, 스마트 컨트랙트를 위한 수수료
스마트컨트랙트를 배포하거나 run할때 사용되는 수수료
채굴자는 가스가격이 높은것부터 스마트 컨트랙트를 수행시킴
가스 단위가 클 수록 트랜잭션의 빠른 처리 가능

각 동작마다 정해진 가스 비용이 있고 배포자가 정한 임의의 가스 리밋이 있음
스마트 컨트랙트가 수행중에 가스비용이 리밋을 초과하게 되면 롤백됨

- 가스 수수료를 통한 채굴자의 유입유도
- 개발자의 간결한 코드 유도
- 악의적인 스마트 컨트랙트의 반복을 막기 위한 시스템

<hr>

## EVM (Ethereum virtual Machine)
이더리움 스마트 컨트랙트를 실행하기 위한 가상머신

특징
- 튜링 완전머신, 스택 기반 구조, 32 Byte의 메모리
- 이더리움 주소 연산(160bit), 256 bit 암호화 알고리즘 등 이더리움 관련 구조 연산에 최적화

모든 동작을 수행하기 위해서는 사전에 가스가 지불되어야 함
-> DoS(Denial of Service)공격을 방지하기 위함

EVM의 프로그램은 내부에서만 실행되고 가상머신의 HOST 환경에는 접근 불가
EVM간 메시지를 통해 데이터를 송수신할 수 있음
결정적 머신 -> 때문에 항상 동일한 상태를 반환

EVM Memory
스마트 컨트랙트 호출 시 생성
일반적인 PC의 RAM과 마찬가지로 휘발성
Memory의 크기가 증가 시 가스가 반드시 소모되며 가스량은 지수적으로 증가
사용자 정의 함수 내부 선언된 변수

EVM Storage
key-value 저장소
key : 256qllxm, Value : 256비트
스마트 컨트랙트는 자신의 storage에만 접근 가능
스마트 컨트랙트에서 사용자 정의 함수 외부에 선언된 변수를 나타냄

<hr>

# Solidity

이더리움 스마트 컨트랙트 언어의 종류
가장 많이 활용되는 언어
Java와 유사한 문법

객체지향 언어
Class = Contract (유사)
정적 타입 언어
