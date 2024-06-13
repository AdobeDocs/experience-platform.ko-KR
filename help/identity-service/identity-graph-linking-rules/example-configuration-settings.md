---
title: 예제 구성
description: 그래프 시뮬레이션 도구를 사용한 예제 구성에 대해 알아봅니다.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 22%

---

# 그래프 구성 예

>[!NOTE]
>
>&quot;CRM ID&quot;는 사용자 지정 네임스페이스입니다. 따라서 아래 예제에서는 표시 이름과 ID 기호가 &quot;CRM ID&quot;인 사용자 지정 네임스페이스를 만들어야 합니다.

다음 섹션에서는 그래프 시뮬레이션에서 발생할 수 있는 그래프 시나리오에 대해 설명합니다.

## CRM ID만

이벤트:

* CRM ID: Tom, ECID: 111

알고리즘 구성:

| 우선 순위 | 표시 이름 | ID 심볼 | ID 유형 | 그래프별로 고유 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | CROSS_DEVICE | 예 |
| 2 | ECID | ECID | 쿠키 | 아니요 |

+++시뮬레이션된 그래프를 보려면 선택

+++

## 해시된 이메일이 있는 CRM ID

이 시나리오에서 CRM ID는 수집되며 온라인(경험 이벤트) 및 오프라인(프로필 레코드) 데이터를 모두 나타냅니다. 이 시나리오에는 CRM ID와 함께 CRM 레코드 데이터 세트에서 전송된 다른 네임스페이스를 나타내는 해시된 이메일의 수집도 포함됩니다.

이벤트:

* CRM ID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRM ID: Tom, ECID: 111
* CRM ID: Summer, Email_LC_SHA256: summer<span>@acme.com
* CRM ID: Summer, ECID: 222

알고리즘 구성:

| 우선 순위 | 표시 이름 | ID 심볼 | ID 유형 | 그래프별로 고유 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | CROSS_DEVICE | 예 |
| 2 | 이메일(SHA256, 소문자) | Email_LC_SHA256 | 이메일 | 아니요 |
| 3 | ECID | ECID | 쿠키 | 아니요 |

+++시뮬레이션된 그래프를 보려면 선택

+++

## 해시된 이메일, 해시된 휴대폰, GAID 및 IDFA가 있는 CRM ID

이벤트:

* CRM ID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRM ID: Tom, ECID: 111
* CRM ID: Tom, ECID: 222, IDFA: A-A-A
* CRM ID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM ID: Summer, ECID: 333
* CRM ID: Summer, ECID: 444, GAID:B-B-B

알고리즘 구성:

| 우선 순위 | 표시 이름 | ID 심볼 | ID 유형 | 그래프별로 고유 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | CROSS_DEVICE | 예 |
| 2 | 이메일(SHA256, 소문자) | Email_LC_SHA256 | 이메일 | 아니요 |
| 3 | 휴대폰 (SHA256) | Phone_SHA256 | 휴대폰 | 아니요 |
| 4 | Google 광고 ID (GAID) | GAID | 장치 | 아니요 |
| 5 | Apple IDFA (Apple의 ID) | IDFA | 장치 | 아니요 |
| 6 | ECID | ECID | 쿠키 | 아니요 |

+++시뮬레이션된 그래프를 보려면 선택

+++