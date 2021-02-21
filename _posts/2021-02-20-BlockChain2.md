---
layout: post
title: "[BLOCKCHAIN] 합의 알고리즘과 해시, 블록"
date: 2021-02-20 00:00:00
categories: [STUDY]
tags: [BLOCKCHAIN]
last_modified_at: 2021-02-20
---

from [https://steemit.com/kr/@yahweh87/1-consensus-problem](https://steemit.com/kr/@yahweh87/1-consensus-problem)
<br>from [https://steemit.com/kr/@yahweh87/2](https://steemit.com/kr/@yahweh87/2)
<br>from [https://www.banksalad.com/contents/%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85%ED%95%98%EB%8A%94-%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%EB%A8%B8%ED%81%B4%ED%8A%B8%EB%A6%AC-Merkle-Trees-%EB%9E%80-ilULl](https://www.banksalad.com/contents/%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85%ED%95%98%EB%8A%94-%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%EB%A8%B8%ED%81%B4%ED%8A%B8%EB%A6%AC-Merkle-Trees-%EB%9E%80-ilULl)
---


# 합의 알고리즘 Consensus Algorithm

<p>합의 알고리즘은 어떠한 방식으로 블록을 생성하고,
어떤 블럭이 진짜인지 판별하기 위한 알고리즘</p>

### 탈중앙화 Application(DApp)

<p>
: 탈중앙화된 P2P 네트워크(분산시스템)에서 동작
<br>: 어떠한 단일 노드도 DApp의 제어권을 가질 수 없음
</p>

### 합의 프로토콜(합의 알고리즘)

<p>
: 피어가 발행한 정보가 올바른지 검증하기 위한 방법
<br>: P2P 네트워크의 신뢰도를 보장하기 위함
<br>: 네트워크에서 하나의 결과에 대한 합의를 얻기 위한 알고리즘
<br>: 무결성을 보장
</p>

### 합의 알고리즘 종류
<p>
PoW(Power of Work)
<br>PoS(Power of Stake)
<br>DPos(Delegated Proof od Stake)
</p>

---

# 해쉬 Hash

### 해쉬 함수
<p>
: 해쉬 함수는 임의의 입력을 받아 고정된 길이의 랜덤 데이터를 생성.
<br>: 입력의 변화는 출력에 랜덤하게 나타남.
<br>: 일방향 함수라 출력값으로 입력값을 추적할 수 없음.
<br>: 해쉬값이 같으면 같은 객체임을 알 수 있음.
<br>: 즉, 위변조를 확인할 수 있는 무결성을 제공.
</p>

---

# 블록체인 BlockChain

<p>
: 블록과 블록을 체인형태로 연결한 자료구조
</p>

### 블록

<p>
: 다수의 거래 정보의 묶음
<br>: 일정 시간마다 생성
<br>: head와 body로 이루어져 있음
</p>

<figure>
   <img src="/Fortune/assets/BlockChain/10.jpg" style="width:50%">
</figure>

<p>
블록의 해시인 TXID(transaction ID)로 블록을 식별
<br>헤더의 모든 정보를 합산하여 SHA256 해시함수로 얻은 결과값
</p>

<p>
Version은 해당 비트 코인 프로그램의 버전 정보
</p>

<p>
Previous Block Hash는 이전 블록의 주소값(이전 블록의 해쉬값)을 가리킴
</p>

<p>
Merkle Root는 body의 트랜잭션들을 정리한 머클 트리(해시 트리)의 루트노드.
<br>리프 노드의 해시값을 합한 정보로 부모 노드의 해시값을 결정.
머클 트리를 통해, 데이터의 간편하고 확실한 인증은 물론 빠르게 검색 가능.
</p>

<p>
단일 블록내에 존재하는 트랜잭션의 무결성과 블록의 해시의 무결성을 증명할 수 있음.
</p>

<p>
Time은 해당 블록의 대략적인 생성 시간을 의미
<br>bits는 난이도 해시 목표값을 의미
<br>Nonce는 블록을 만드는 과정에서 해시값을 구할 때 필요한 값
</p>

<br>
<br>
