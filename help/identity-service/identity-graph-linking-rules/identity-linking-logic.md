---
title: ID 서비스 연결 논리
description: ID 서비스에서 다양한 ID를 연결하여 고객에 대한 포괄적인 보기를 만드는 방법에 대해 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 03228eef47100096e98666966c4e5065eb7f478a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# ID 서비스 연결 논리

ID 네임스페이스와 ID 값이 일치하면 두 ID 간의 링크가 설정됩니다.

다음과 같이 연결되는 두 가지 유형의 ID가 있습니다.

* **프로필 레코드**: 이러한 ID는 일반적으로 CRM 시스템에서 가져옵니다.
* **경험 이벤트**: 이러한 ID는 일반적으로 WebSDK 구현 또는 Adobe Analytics 소스에서 가져옵니다.

## ID 서비스 연결 논리 이해

ID는 ID 네임스페이스와 ID 값으로 구성됩니다.

* ID 네임스페이스는 지정된 ID 값 의 컨텍스트입니다. ID 네임스페이스의 일반적인 예로는 CRM ID, 이메일 및 전화 등이 있습니다.
* ID 값은 실제 엔티티를 나타내는 문자열입니다. 예: &quot;julien<span>@acme.com&quot;은 이메일 네임스페이스에 대한 ID 값이고 555-555-1234는 전화 네임스페이스에 대한 해당 ID 값일 수 있습니다.

>[!TIP]
>
>ID 네임스페이스가 중요한 이유는 ID 값이 없으면 ID 값의 컨텍스트가 손실되어 ID를 일치시킬 충분한 정보가 없기 때문입니다.

ID 서비스 연결 로직의 작동 방식을 시각적으로 표현하려면 다음 다이어그램을 참조하십시오.

>[!BEGINTABS]

>[!TAB 기존 그래프]

세 개의 연결된 ID가 있는 기존 ID 그래프가 있다고 가정해 봅시다.

* 전화:(555)-555-1234
* 이메일:julien<span>@acme.com
* CRM ID:60013ABC

![기존 그래프](../images/identity-settings/existing-graph.png)

>[!TAB 수신 데이터]

ID 쌍이 그래프에 수집되고 이 쌍에는 다음이 포함됩니다.

* CRM ID:60013ABC
* ECID:100066526

![들어오는 데이터](../images/identity-settings/incoming-data.png)

>[!TAB 업데이트된 그래프]

ID 서비스는 CRM ID:60013ABC가 그래프 내에 이미 있음을 인식하므로 새 ECID만 연결합니다

![업데이트된 그래프](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## 고객 시나리오

데이터 엔지니어이며 Experience Platform 대상으로 다음 CRM 데이터 세트(프로필 레코드)를 수집합니다.

| CRM ID** | 전화* | 이메일* | 이름 | 성 |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | 줄리엔<span>@acme.com | 줄리엔 | Smith |
| 31260XYZ | 777-777-6890 | 에번<span>@acme.com | 에번 | Smith |

>[!NOTE]
>
>* `**` - 기본 ID로 표시된 필드를 나타냅니다.
>* `*` - 보조 ID로 표시된 필드를 나타냅니다.
>
>ID 서비스는 기본 ID와 보조 ID를 구분하지 않습니다. 필드가 ID로 표시되는 한 ID 서비스로 수집됩니다.

또한 WebSDK를 구현하고 다음 데이터 테이블로 WebSDK 데이터 세트 (경험 이벤트)를 수집했습니다.

| 타임스탬프 | 이벤트의 ID* | 이벤트 |
| --- | --- | --- |
| `t=1` | ECID:38652 | 홈 페이지 보기 |
| `t=2` | ECID:38652, CRM ID:31260XYZ | 신발 검색 |
| `t=3` | ECID:44675 | 홈 페이지 보기 |
| `t=4` | ECID:44675, CRM ID: 31260XYZ | 구매 내역 보기 |

>[!NOTE]
>
>* `*` - ID로 표시된 필드를 나타내며 ECID는 기본 필드로 표시됩니다.
>* 기본적으로 개인 식별자(이 경우 CRM ID)가 기본 ID로 지정됩니다. 개인 식별자가 없으면 쿠키 식별자(이 경우 ECID)가 기본 ID가 됩니다.

이 예제에서는

* `t=1`데스크탑 컴퓨터(ECID:38652)와 를 사용하여 익명으로 홈 페이지를 검색했습니다.
* `t=2`와 동일한 데스크탑 컴퓨터를 사용하고 (CRM ID:31260XYZ)에 로그인한 다음 신발을 검색했습니다.
   * 사용자가 로그인하면 이벤트가 ECID와 CRM ID를 모두 ID 서비스로 보냅니다.
* `t=3`랩톱 컴퓨터(ECID:44675)를 사용하고 익명으로 검색했습니다.
* `t=4`와 동일한 랩톱 컴퓨터를 사용하고 (CRM ID: 31260XYZ)에 로그인한 다음 구매 내역을 열람했습니다.


>[!BEGINTABS]

>[!TAB timestamp=0]

위치 `timestamp=0`, 두 개의 서로 다른 고객을 위한 두 개의 id 그래프가 있습니다. 두 사람은 모두 세 개의 연결된 ID로 표시됩니다.

| | CRM ID | 이메일 | 전화 |
| --- | --- | --- | --- |
| 고객 1 | 60013ABC | 줄리엔<span>@acme.com | 555-555-1234 |
| 고객 2 | 31260XYZ | 에번<span>@acme.com | 777-777-6890 |

![timestamp-0](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

위치 `timestamp=1`, 한 고객이 노트북을 사용하여 전자 상거래 웹 사이트를 방문하고 홈 페이지를 열람하며 익명으로 탐색합니다. 이 익명 브라우징 이벤트는 ECID:38652으로 식별됩니다. Identity Service는 두 개 이상의 ID가 있는 이벤트만 저장하므로 이 정보는 저장되지 않습니다.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

위치 `timestamp=2`, 고객은 동일한 노트북을 사용하여 전자 상거래 웹 사이트를 방문합니다. 사용자 이름과 암호 조합으로 로그인하여 신발을 찾습니다. ID 서비스는 CRM ID: 31260XYZ에 해당하므로 로그인할 때 고객의 계정을 식별합니다. 또한 ID 서비스는 ECID:38562과 CRM ID:31260XYZ를 관련시킵니다. 둘 다 동일한 디바이스에서 동일한 브라우저를 사용하기 때문입니다.

![timestamp-2](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

위치 `timestamp=3` 고객이 태블릿을 사용하여 전자 상거래 웹 사이트를 방문하고 익명으로 탐색합니다. 이 익명 브라우징 이벤트는 ECID:44675으로 식별됩니다. Identity Service는 두 개 이상의 ID가 있는 이벤트만 저장하므로 이 정보는 저장되지 않습니다.

![timestamp-](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

위치 `timestamp=4`, 고객은 동일한 태블릿을 사용하고 계정(CRM ID:31260XYZ)에 로그인하며 구매 내역을 봅니다. 이 이벤트는 CRM ID:31260XYZ를 익명 검색 활동에 할당된 쿠키 식별자 ECID:44675에 연결하고 ECID:44675을 고객 2의 ID 그래프에 연결합니다.

![timestamp-](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

## 다음 단계

ID 그래프 연결 규칙에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [ID 그래프 연결 규칙 개요](./overview.md)
* [ID 그래프 연결 규칙을 구성하기 위한 예제 시나리오](./example-scenarios.md)
* [ID 서비스 및 실시간 고객 프로필](identity-and-profile.md)
