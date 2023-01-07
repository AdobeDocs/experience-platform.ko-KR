---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service API 안내서 부록
description: 이 문서에는 Privacy Service API 작업을 위한 추가 정보가 포함되어 있습니다.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---

# Privacy Service API 안내서 부록

다음 섹션에는 Adobe Experience Platform Privacy Service API 작업을 위한 추가 정보가 포함되어 있습니다.

## 표준 ID 네임스페이스 {#standard-namespaces}

로 전송되는 모든 ID [!DNL Privacy Service] 는 특정 id 네임스페이스에서 제공해야 합니다. ID 네임스페이스는 [Adobe Experience Platform Identity 서비스](../../identity-service/home.md) ID와 관련된 컨텍스트를 나타냅니다.

다음 표에서는 사용 가능한 몇 가지 일반적으로 사용되는 사전 정의된 ID 유형에 대해 설명합니다. [!DNL Experience Platform]와 연관된 `namespace` 값:

| ID 유형 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 이메일 | `Email` | `6` |
| 전화 | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] 광고주용 ID | `IDFA` | `20915` |
| [!DNL Google] 광고 ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>각 ID 유형에는 도 있습니다 `namespaceId` 정수 값으로, `namespace` ID를 설정할 때 문자열 `type` &quot;namespaceId&quot;에 대한 속성입니다. 의 섹션을 참조하십시오. [네임스페이스 구분자](#namespace-qualifiers) 추가 정보.

조직에서 사용 중인 ID 네임스페이스 목록을 검색할 수 있는 경우는 GET에 요청하여 `idnamespace/identities` 의 엔드포인트 [!DNL Identity Service] API. 자세한 내용은 [Identity Service 개발자 안내서](../../identity-service/api/getting-started.md) 추가 정보.

## 네임스페이스 구분자

을 지정할 때 `namespace` 값에서 [!DNL Privacy Service] API, a **네임스페이스 한정자** 는 해당 `type` 매개 변수. 다음 표에서는 서로 다른 수락된 네임스페이스 한정자에 대해 설명합니다.

| 한정자 | 정의 |
| --------- | ---------- |
| `standard` | 전역 정의된 표준 네임스페이스 중 하나이며 개별 조직 데이터 세트(예: 이메일, 전화번호 등)에 연결되어 있지 않습니다. 네임스페이스 ID가 제공됩니다. |
| `custom` | 조직 컨텍스트에서 생성된 고유한 네임스페이스이며, [!DNL Experience Cloud]. 값은 검색할 친숙한 이름(&quot;name&quot; 필드)을 나타냅니다. 네임스페이스 ID가 제공됩니다. |
| `integrationCode` | 통합 코드 - &quot;사용자 지정&quot;과 유사하지만, 특히 검색할 데이터 소스의 통합 코드로 정의됩니다. 네임스페이스 ID가 제공됩니다. |
| `namespaceId` | 값은 네임스페이스 서비스를 통해 만들어지거나 매핑된 네임스페이스의 실제 ID임을 나타냅니다. |
| `unregistered` | 네임스페이스 서비스에 정의되어 있지 않고 &quot;있는 그대로&quot; 가져오는 자유 형식 문자열입니다. 이러한 종류의 네임스페이스를 처리하는 모든 애플리케이션은 회사의 컨텍스트 및 데이터 세트에 맞게 해당 네임스페이스와 비교하여 확인하고 적절한 경우 처리합니다. 네임스페이스 ID가 제공되지 않습니다. |
| `analytics` | 내부적으로 매핑된 사용자 지정 네임스페이스 [!DNL Analytics]네임스페이스 서비스가 아닙니다. 네임스페이스 ID 없이 원래 요청에 지정된 대로 직접 전달됩니다 |
| `target` | 에서 내부적으로 인식하는 사용자 지정 네임스페이스 [!DNL Target]네임스페이스 서비스가 아닙니다. 네임스페이스 ID 없이 원래 요청에 지정된 대로 직접 전달됩니다 |

{style=&quot;table-layout:auto&quot;}

## 수락된 제품 값

다음 테이블은에서 Adobe 제품을 지정하기 위해 허용되는 값을 간략하게 설명합니다 `include` 작업 생성 요청의 속성입니다.

| 제품 | 에서 사용할 값 `include` 특성 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (실시간 고객 프로필) | `profileService` |
| Adobe Primetime 인증 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 고객 속성(CRS) | `CRS` |
| ID 서비스 | `identity` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
