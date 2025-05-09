---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service API 안내서 부록
description: 이 문서에는 Privacy Service API 작업에 대한 추가 정보가 포함되어 있습니다.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

---

# Privacy Service API 안내서 부록

다음 섹션에는 Adobe Experience Platform Privacy Service API 작업에 대한 추가 정보가 포함되어 있습니다.

## 표준 ID 네임스페이스 {#standard-namespaces}

[!DNL Privacy Service] (으)로 전송되는 모든 ID는 특정 ID 네임스페이스에 제공되어야 합니다. ID 네임스페이스는 [Adobe Experience Platform ID 서비스](../../identity-service/home.md)의 구성 요소로서 ID와 관련된 컨텍스트를 나타냅니다.

다음 표에서는 [!DNL Experience Platform]에서 일반적으로 사용되는 사전 정의된 ID 유형과 관련 `namespace` 값을 간략하게 설명합니다.

| ID 유형 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 이메일 | `Email` | `6` |
| 휴대폰 | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| 광고주용 [!DNL Apple] ID | `IDFA` | `20915` |
| [!DNL Google] 광고 ID | `GAID` | `20914` |
| [!DNL Windows] 지원 | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>각 ID 유형에는 `namespaceId` 정수 값도 있습니다. 이 값은 ID의 `type` 속성을 &quot;namespaceId&quot;로 설정할 때 `namespace` 문자열 대신 사용할 수 있습니다. 자세한 내용은 [네임스페이스 한정자](#namespace-qualifiers)의 섹션을 참조하십시오.

[!DNL Identity Service] API의 `idnamespace/identities` 끝점에 대한 GET 요청을 통해 조직에서 사용 중인 ID 네임스페이스 목록을 검색할 수 있습니다. 자세한 내용은 [ID 서비스 개발자 안내서](../../identity-service/api/getting-started.md)를 참조하십시오.

## 네임스페이스 한정자

[!DNL Privacy Service] API에서 `namespace` 값을 지정할 때 **네임스페이스 한정자**&#x200B;이(가) 해당 `type` 매개 변수에 포함되어야 합니다. 다음 표에서는 허용되는 다양한 네임스페이스 한정자에 대해 설명합니다.

| 한정자 | 정의 |
| --------- | ---------- |
| `standard` | 개별 조직 데이터 세트(예: 이메일, 전화번호 등)에 연결되지 않고 전역적으로 정의된 표준 네임스페이스 중 하나입니다. 네임스페이스 ID가 제공됩니다. |
| `custom` | [!DNL Experience Cloud]에서 공유되지 않는 조직 컨텍스트에서 만들어진 고유한 네임스페이스입니다. 검색할 친숙한 이름(&quot;name&quot; 필드)을 나타내는 값입니다. 네임스페이스 ID가 제공됩니다. |
| `integrationCode` | 통합 코드 - &quot;사용자 정의&quot;와 유사하지만 특히 검색할 데이터 소스의 통합 코드로 정의됩니다. 네임스페이스 ID가 제공됩니다. |
| `namespaceId` | 값이 네임스페이스 서비스를 통해 만들어지거나 매핑된 네임스페이스의 실제 ID임을 나타냅니다. |
| `unregistered` | 네임스페이스 서비스에 정의되지 않고 &quot;있는 그대로&quot; 사용되는 자유 형식 문자열입니다. 이러한 종류의 네임스페이스를 처리하는 모든 애플리케이션은 이러한 네임스페이스에 대해 확인하고 회사 컨텍스트 및 데이터 세트에 적합하면 처리합니다. 네임스페이스 ID가 제공되지 않았습니다. |
| `analytics` | 네임스페이스 서비스가 아닌 [!DNL Analytics]에서 내부적으로 매핑된 사용자 지정 네임스페이스입니다. 네임스페이스 ID 없이 원래 요청에서 지정한 대로 직접 전달됩니다. |
| `target` | 네임스페이스 서비스가 아닌 [!DNL Target]이(가) 내부적으로 이해하는 사용자 지정 네임스페이스입니다. 네임스페이스 ID 없이 원래 요청에서 지정한 대로 직접 전달됩니다. |

{style="table-layout:auto"}

## 허용된 제품 값

다음 표에서는 작업 생성 요청의 `include` 특성에서 Adobe 제품을 지정하는 데 허용되는 값을 간략하게 설명합니다.

>[!NOTE]
>
>제품 목록의 값은 대/소문자를 구분하지 않습니다. Camel-case가 권장되지만 적용되지 않습니다.

| 제품 | `include` 특성에 사용할 값 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (데이터 레이크) | `aepDataLake` |
| Adobe Experience Platform (실시간 고객 프로필) | `profileService` |
| Adobe Pass 인증 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 고객 속성(CRS) | `CRS` |
| 고객 여정 관리 | `cjm` |
| ID 서비스 | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
