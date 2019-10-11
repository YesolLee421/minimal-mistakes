---
title: "[블록체인] 8주차_블록체인과 암호기술 2"
categories:
  - BlockChain
  - 블록체인
comments : true
---
*이 내용은 K-MOOC [알기쉬운블록체인] 강의를 듣고 정리한 내용입니다.*
<br>

[알기쉬운블록체인]: http://www.kmooc.kr/courses/course-v1:SJCU+SJCU01+2019_2/courseware/145ba5714d1246c1b65fe1b081d52db0/e1af1659e74343579fe5727acdfcfbc7/?child=last

<br>

# 거래 데이터의 신뢰성
## 전자서명의 필요성
### 1. 블록체인에 전자서명(electric signature)가 필요한 이유
- 분산 시스템의 서로 다른 장부가 같은지 확인하기 위해 `해시값` 비교
- 그런데 `해시 함수` 만으로 전체 시스템 `무결성` 확보 가능할까?
- 변경된 내용에 대한 새로운 해시값 생성해서 전송 -> 새로운 해시값도 형식은 유효하기 때문에 해당 값 자체만 보고 위, 변조 여부 확인하기는 어렵다.
- 검증값으로 확인하려면? `제 3의 신뢰할 수 있는 자(trusted third party)`가 공개한 검증값과 내가 받은 검증값을 비교하면 된다.
- 공개 검증값 없는 경우는?<br>

### 2. 공개된 네트워크에서 주고 받는 데이터를 어떻게 신뢰할 수 있을까?
1. *이 메시지는 정당한(legimate) 송신자가 보낸 것이 맞는가?*
    - "A가 보냈다는 데이터를 받았는데 이게 진짜 A가 보낸 것이 맞는가?"
    - 예시) 편지 봉투 겉면에 '보내는 사람'만 보고 송신자가 바뀌지 않았음을 알수 있나? (쉽게 다른 사람 이름으로 변조 가능)
2. *송신자가 보낸 메시지가 맞는가?*
    - "A가 보낸 메시지는 맞는데 내용도 원본과 일치하는가?"
    - 예시) 편지 내용만 보고 이 사람이 보낸 내용이 맞다고 확신할 수 있나? (내용만 보고는 편지 내용이 변경되지 않았는지 알기 힘들다)<br>

### 3. 편지의 위, 변조를 막기 위해 사용한 방법
- 중세시대 밀랍과 인장: 편지 내용을 보호하고 아무나 열지 못하도록, 또는 개봉되었음을 쉽게 식별하기 위해 편지 봉인해서 보냄
- 편지에 `서명(signature)`: 위조가 어렵게 하고, 내가 해당 문서에 동의 혹은 해당 문서를 내가 만들었다는 것을 표현함
- 수결 (손바닥 모양대로 본 뜨기): 글을 쓰지 못하는 경우
- 고유 도장 사용
- 온라인에서도 이와 유사하게 서명과 같은 행위 필요해짐<br>

### 4. 전자서명의 필요성
- 인터넷: `비대면`으로 데이터 주고 받음
- 온라인 비대면 거래가 증가하며 상대방 확인할 새로운 방법 필요
- 디지털 데이터의 특성 상 쉽게 위, 변조가 가능하
- 일상생활에서 계약서에 서명하는 것과 같은 상황을 온라인에서 구현해야 함
- 결과) `전자서명` 도입<br>


## 전자서명의 특징
### 1. 전자서명(Digital Signature)이란?
- 디지털 데이터에 서명하는 방법
- 서명된 메시지가 디지터 데이터로 표현됨 -> 당연히 컴퓨터 네트워크를 통해 송신, 수신 가능
- 필요 기능
    1. 신뢰성 제공: 이 디지털 데이터(전자서명)을 생성한 사람이 누구인지 `인증(Authentication)`
    2. 무결성 기능: 디지털 데이터가 원본과 다름없이 변조되지 않았음을 식별할 수 있어야 한다.<br>

### 2. 기존 서명 VS 전자 서명
- 기존 서명
    - 물리적으로 서명된 문서의 일부임 (문서 / 서명 분리 불가)
    - 원본 서명과 인쇄한 복제본이 확연히 식별 가능
    - 사용 방식) 신용카드로 물건 구매하는 경우: 신용카드 뒤 서명(원본)과 수기로 쓴 서명을 대조해서 해당 서명이 정당한지 판단
- 전사 서명
    - 디지털 데이터 값으로 존재 -> 문서 내용과 서명값이 별도 값으로 존재
    - 따라서 원본 데이터와 데이터에 대한 서명값 묶는 역할 필요
    - 비교할 데이터와 서명값이 주어진 상황에서 누구나 손쉽게 서명 진의 여부 확인해야 함
    - 사용 방식) 공개적으로 알려진 정보를 사용하여 메시지에 대응하는 서명값을 누구나 확인, 검증할 수 있다.
    - 데이터 복제가 쉽다 -> 원본과 사본이 동일 ->재사용 방지 대책 필요
    - 재사용 방지: 거래 당시의 날짜 정보, 혹은 거래 번호 등 서명을 생성할 때마다 동일한 서명값이 나오지 않도록 만들 수 있는 체계 필요<br>


### 3. 전자 서명의 요구조건
1. 위조 불가 (Unforgeable): 정당한 서명자(legimate signer)만이 전자서명 생성 가능
    - 다른 사람의 서명 쉽게 만들 수 없도록 한다
    - 기존 서명) 필적대조, 인감도장 사용 등 위조 방지를 위한 노력
    - 디지털 데이터 변조 시 사람보다 훨씬 빠른 계산능력을 가진 컴퓨터가 수행하니 매우 어려워야 함<br>

2. 서명자 인증 (Authentic): 누구든지 서명자 확인 가능
    - 기존 서명) 우리가 직접 적은 서명과 대조본 비교해서 서명 진위여부 판단
    - 온라인 상 데이터: 누구나 데이터를 보고 이것이 정당한 서명자가 인증한 것임을 확인할 수 있어야 한다.
    - 또한 확인 과정은 비교적 빠른 시간 내 이루어져야 한다.<br>

3. 재사용 불가 (Not Reusable): 다른 문서의 서명으로 사용 불가
    - 어떤 문서에 서명을 할 시 그 문서에 대한 `서명값` 생성됨
    - 다른 사람이 다른 문서의 서명으로 주어진 서명값을 사용하는 게 불가능하도록 해야 한다.<br>

4. **변경 불가 (Unalterable): 서명된 문서의 내용 변경 불가**
    - 기존 서명) 내용과 서명이 물리적으로 분리 불가능 -> 문서 위조를 위해 서명도 위조해야 한다.
    - 디지털 데이터 특성 상 데이터(내용)과 데이터에 대한 서명값은 별도 값으로 존재
    - 따라서 다른 데이터에 대한 같은 서명값이 나오거나, 다른 서명값이 원래 문서에 대응한다는 증명이 불가능하도록 설계해야 한다.<br>

5. 부인 방지 (Nonrepudiation): 서명 사실 부인 불가
    - 기존 서명) 수표 발행 시 *'이서'*하고 발행 -> 수표 발행 후 발행 사실 부인해도 이서한 것과 내 서명이 같으면 내가 발행한 사실을 부인할 수 없다.
    > 이서하다: 법률> 「…에」 [같은 말] 배서하다(2. 민법에서, 채권 양도(債權讓渡)의 의사 표시를 증권의 뒷면에 기재하다). 예시: 수표에 이서해 주십시오.
    - 전자 서명) 나와 내가 한 서명이 `매핑`되어야 함
    - 데이터에 대한 서명값 생성 시 **'키(key)'** 필요
    - 이 key의 소유자가 나라는 것을 다시 매핑하는 연결고리 필요
    - 예시) 공인인증서 발급 시 여러 가지 채널로 '나'임을 증명 (ARS, 아이핀, 문자 인증 등등)
    - 인증서 등 전자서명: '나'에 대한 정보 + 공개 키 정보값 + 그걸 검증해 준 사람의 서명 ~ `신뢰할 수 있는 제 3자`가 보장해주는 기능 포함<br>
 