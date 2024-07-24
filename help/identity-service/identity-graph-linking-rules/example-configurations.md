---
title: 예제 구성
description: 그래프 시뮬레이션 도구를 사용한 예제 구성에 대해 알아봅니다.
badge: Beta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 10%

---

# 그래프 구성 예

>[!AVAILABILITY]
>
>ID 그래프 연결 규칙은 현재 Beta 버전입니다. 기여도 기준에 대한 자세한 내용은 Adobe 계정 팀에 문의하십시오. 기능 및 설명서는 변경될 수 있습니다.

>[!NOTE]
>
>* &quot;CRMID&quot; 및 &quot;loginID&quot;는 사용자 정의 네임스페이스입니다. 이 문서에서 &quot;CRMID&quot;는 개인 식별자이고 &quot;loginID&quot;는 지정된 사용자와 연관된 로그인 식별자입니다.
>* 이 문서에 설명된 예제 그래프 시나리오를 시뮬레이션하려면 먼저 ID 기호가 &quot;CRMID&quot;인 네임스페이스와 ID 기호가 &quot;loginID&quot;인 네임스페이스를 두 개 사용자 정의 생성해야 합니다. ID 기호는 대/소문자를 구분합니다.

이 문서에서는 ID 데이터 작업 시 발생할 수 있는 일반적인 시나리오의 그래프 구성 예제를 간략하게 설명합니다.

## CRMID만

이는 온라인 이벤트(CRMID 및 ECID)가 수집되고 오프라인 이벤트(프로필 레코드)가 CRMID에 대해서만 저장되는 간단한 구현 시나리오의 예입니다.

**구현:**

| 사용된 네임스페이스 | 웹 동작 수집 방법 |
| --- | --- |
| CRMID, ECID | Web SDK |

**이벤트:**

다음 이벤트를 텍스트 모드에 복사하여 그래프 시뮬레이션에서 이 시나리오를 생성할 수 있습니다.

* CRMID: Tom, ECID: 111

**알고리즘 구성:**

알고리즘 구성에 대해 다음 설정을 구성하여 그래프 시뮬레이션에서 이 시나리오를 생성할 수 있습니다.

| 우선 순위 | 표시 이름 | ID 유형 | 그래프별로 고유 |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | 예 |
| 2 | ECID | 쿠키 | 아니요 |

**실시간 고객 프로필에 대한 기본 ID 선택:**

이 구성의 컨텍스트 내에서 기본 ID는 다음과 같이 정의됩니다.

| 인증 상태 | 이벤트의 네임스페이스 | 기본 ID |
| --- | --- | --- |
| Authenticated | CRMID, ECID | CRMID |
| 인증되지 않음 | ECID | ECID |

>[!BEGINTABS]

>[!TAB 이상적인 1인 그래프 시나리오]

다음은 CRMID가 고유하고 우선 순위가 가장 높은 이상적인 1인 그래프의 예입니다.

![CRMID가 고유하고 우선 순위가 가장 높은 이상적인 1인 그래프의 시뮬레이션된 예입니다.](../images/graph-examples/crmid_only_single.png)

>[!TAB 여러 사용자 그래프 시나리오]

다음은 다인용 그래프의 예입니다. 이 예에서는 &quot;공유 장치&quot; 시나리오를 표시합니다. 여기서 두 개의 CRMID가 있고 이전 링크가 설정된 CRMID가 제거됩니다.

![사람 그래프의 시뮬레이션된 예입니다. 이 예제에서는 두 개의 CRMID가 있고 이전에 설정한 링크가 제거되는 공유 장치 시나리오를 표시합니다.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## 해시된 이메일이 포함된 CRMID

이 시나리오에서 CRMID는 수집되며 온라인(경험 이벤트) 및 오프라인(프로필 레코드) 데이터를 모두 나타냅니다. 이 시나리오에는 CRMID와 함께 CRM 레코드 데이터 세트에서 전송된 다른 네임스페이스를 나타내는 해시된 이메일의 수집도 포함됩니다.

**구현:**

| 사용된 네임스페이스 | 웹 동작 수집 방법 |
| --- | --- |
| CRMID, Email_LC_SHA256, ECID | Web SDK |

**이벤트:**

다음 이벤트를 텍스트 모드에 복사하여 그래프 시뮬레이션에서 이 시나리오를 생성할 수 있습니다.

* CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRMID: Tom, ECID: 111
* CRMID: Summer, Email_LC_SHA256: summer<span>@acme.com
* CRMID: Summer, ECID: 222

**알고리즘 구성:**

알고리즘 구성에 대해 다음 설정을 구성하여 그래프 시뮬레이션에서 이 시나리오를 생성할 수 있습니다.

| 우선 순위 | 표시 이름 | ID 유형 | 그래프별로 고유 |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | 예 |
| 2 | 이메일(SHA256, 소문자) | 이메일 | 아니요 |
| 3 | ECID | 쿠키 | 아니요 |

**프로필에 대한 기본 ID 선택:**

이 구성의 컨텍스트 내에서 기본 ID는 다음과 같이 정의됩니다.

| 인증 상태 | 이벤트의 네임스페이스 | 기본 ID |
| --- | --- | --- |
| Authenticated | CRMID, ECID | CRMID |
| 인증되지 않음 | ECID | ECID |

>[!BEGINTABS]

>[!TAB 이상적인 1인 그래프 시나리오]

![이 예제에서는 각각 1인 엔터티를 나타내는 두 개의 그래프가 생성됩니다.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB 여러 사용자 그래프: 공유된 장치]

![이 예제에서 시뮬레이션된 그래프는 Tom과 Summer가 모두 동일한 ECID에 연결되어 있으므로 &quot;공유 장치&quot; 시나리오를 표시합니다.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB 여러 사용자 그래프: 고유하지 않은 전자 메일]

![이 시나리오는 &quot;공유 장치&quot; 시나리오와 유사합니다. 그러나 개인 엔터티가 ECID를 공유하게 하는 대신 동일한 전자 메일 계정과 연결됩니다.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## 해시된 이메일, 해시된 휴대폰, GAID 및 IDFA가 포함된 CRMID

이 시나리오는 이전 시나리오와 유사합니다. 그러나 이 시나리오에서는 해시된 이메일과 전화기가 세그먼트 일치에서 활용할 ID로 표시됩니다.

**구현:**

| 사용된 네임스페이스 | 웹 동작 수집 방법 |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | Web SDK |

**이벤트:**

다음 이벤트를 텍스트 모드에 복사하여 그래프 시뮬레이션에서 이 시나리오를 생성할 수 있습니다.

* CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: Tom, ECID: 111
* CRMID: Tom, ECID: 222, IDFA: A-A-A
* CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Summer, ECID: 333
* CRMID: Summer, ECID: 444, GAID:B-B-B

**알고리즘 구성:**

알고리즘 구성에 대해 다음 설정을 구성하여 그래프 시뮬레이션에서 이 시나리오를 생성할 수 있습니다.

| 우선 순위 | 표시 이름 | ID 유형 | 그래프별로 고유 |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | 예 |
| 2 | 이메일(SHA256, 소문자) | 이메일 | 아니요 |
| 3 | 휴대폰 (SHA256) | 휴대폰 | 아니요 |
| 4 | Google 광고 ID (GAID) | 장치 | 아니요 |
| 5 | Apple IDFA (Apple의 ID) | 장치 | 아니요 |
| 6 | ECID | 쿠키 | 아니요 |

**프로필에 대한 기본 ID 선택:**

이 구성의 컨텍스트 내에서 기본 ID는 다음과 같이 정의됩니다.

| 인증 상태 | 이벤트의 네임스페이스 | 기본 ID |
| --- | --- | --- |
| Authenticated | CRMID, IDFA, ECID | CRMID |
| Authenticated | CRMID, GAID, ECID | CRMID |
| Authenticated | CRMID, ECID | CRMID |
| 인증되지 않음 | GAID, ECID | GAID |
| 인증되지 않음 | IDFA, ECID | IDFA |
| 인증되지 않음 | ECID | ECID |

>[!BEGINTABS]

>[!TAB 이상적인 1인 그래프 시나리오]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->
