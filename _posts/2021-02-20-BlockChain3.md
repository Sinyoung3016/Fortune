---
layout: post
title: "[BLOCKCHAIN] 공개키 암호 방식"
date: 2021-03-01 00:00:00
categories: [STUDY]
tags: [BLOCKCHAIN]
last_modified_at: 2021-03-01
---

from [https://academy.binance.com/ko/articles/what-is-public-key-cryptography](https://academy.binance.com/ko/articles/what-is-public-key-cryptography)
<br>from [https://academy.binance.com/ko/articles/private-public-and-consortium-blockchains-whats-the-difference#private-blockchains](https://academy.binance.com/ko/articles/private-public-and-consortium-blockchains-whats-the-difference#private-blockchains)

---

# 공개 키 암호 방식 PKI, Public Key Infrastructure

__공개키를 통한 암호화 + 전자서명__

<p>
비대칭 암호 방식, 개인 키와 공용키를 사용하는 체계를 의미.
<br>대칭 암호 방식보다 높은 수준의 보안을 제공
</p>

### PKI 구성 요소
<p>
1. 공개키 알고리즘
<br>: 비대칭키 암호화 알고리즘으로 메시지의 암호화 및 서명에 사용.
</p>

<p>
2. 공개키 인증서(Public-key Certificate)
<br>: 공개키에 관한 정보와 인증기관의 서명
<br>: 공개키의 무결성, 신빙성을 보증
</p>

<p>
3. 인증기관(CA)
<br>: 인증 객체에 대한 인증서를 발급 또는 폐기.
<br>: 신뢰된 인증기관에서 발급한 인증서는 공개키와 공개키의 주체를 연결시켜주는 고리
<br>: 공개된 인증서 보관소에 인증서를 저장.
</p>

---

# 공개키 알고리즘

<figure>
  <center><img src="/Fortune\assets\BlockChain\5.png"></center>
</figure>

### Signature
<p>
Signing Key는 Public과 Private로 구분.
공용(Public) 키는 전송자가 정보를 암호화하는데 사용하고(암호화키),
개인(Private) 키는 수신자가 암호를 해독하는데 사용(복호화키).
둘은 RSA 알고리즘으로 만들어지지만, 공용 키로 개인 키를 찾아내기 어려움.
</p>

<p>
보안성과 메시지의 무결성을 확인할 수 있는 장점이 있지만,
암호복호화 과정에서 복잡한 수학적 계산으로, 대량의 데이터를 처리할 경우 느려질 수 있음.
또한 개인키가 공유될 경우 보안이 위협받고, 분실하면 데이터에 접근할 수 없음.
</p>

<figure>
  <center><img src="/Fortune\assets\BlockChain\4.png"></center>
</figure>

### 공개키 사용한 암호
<figure>
  <center><img src="/Fortune\assets\BlockChain\6.png"></center>
</figure>

### 공개키 사용한 인증
<figure>
  <center><img src="/Fortune\assets\BlockChain\7.png"></center>
</figure>

---

# 전자성명, Digital Signature
<p>
: 디지털 데이터 스트림으로 구성된 서명키 이용방식
<br>: 위조, 변조, 부인 불가
</p>

### 전자성명 체계

<figure>
  <center><img src="/Fortune\assets\BlockChain\8.png">
  <figcaption>송신자</figcaption>
  </center>
</figure>

<figure>
  <center><img src="/Fortune\assets\BlockChain\9.png">
    <figcaption>수신자</figcaption></center>
</figure>

---

# 인증기관 CA, Certificate Authority

<p>
디지털 인증서를 발급하는 단위
</p>


<br>
<br>


