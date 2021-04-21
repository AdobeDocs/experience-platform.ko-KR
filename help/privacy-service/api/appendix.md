---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: Privacy Service API 안내서 부록
topic-legacy: developer guide
description: 이 문서에는 Privacy Service API 작업에 대한 추가 정보가 포함되어 있습니다.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 9%

---

# Privacy Service API 안내서 부록

다음 섹션에는 Adobe Experience Platform Privacy Service API 작업에 대한 추가 정보가 포함되어 있습니다.

## 표준 ID 네임스페이스 {#standard-namespaces}

[!DNL Privacy Service]으로 전송된 모든 ID는 특정 ID 네임스페이스에서 제공해야 합니다. ID 네임스페이스는 ID와 관련된 컨텍스트를 나타내는 [Adobe Experience Platform Identity Service](../../identity-service/home.md)의 구성 요소입니다.

다음 표는 [!DNL Experience Platform]에 의해 사용 가능한 사전 정의된 ID 유형과 연관된 `namespace` 값을 대략적으로 설명합니다.

| ID 유형 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 이메일 | 이메일 | 6 |
| 전화 | 전화 | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411년 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] 광고주 ID | IDFA | 20915년 |
| [!DNL Google] 광고 ID | GAID | 20914년 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>또한 각 ID 유형에는 `namespaceId` 정수 값이 있으며, ID의 `type` 속성을 &quot;namespaceId&quot;로 설정할 때 `namespace` 문자열 대신 사용할 수 있습니다. 자세한 내용은 [네임스페이스 한정자](#namespace-qualifiers)의 섹션을 참조하십시오.

[!DNL Identity Service] API의 `idnamespace/identities` 종단점에 GET 요청을 하여 조직에서 사용 중인 ID 네임스페이스 목록을 검색할 수 있습니다. 자세한 내용은 [ID 서비스 개발자 안내서](../../identity-service/api/getting-started.md)를 참조하십시오.

## 네임스페이스 한정자

[!DNL Privacy Service] API에서 `namespace` 값을 지정하는 경우 **네임스페이스 한정자**&#x200B;는 해당 `type` 매개 변수에 포함되어야 합니다. 다음 표에서는 서로 다른 허용되는 네임스페이스 한정자에 대해 간략히 설명합니다.

| 한정자 | 정의 |
| --------- | ---------- |
| standard | 개별 조직 데이터 세트(예: 이메일, 전화 번호 등)와 연결되지 않고 전체적으로 정의된 표준 네임스페이스 중 하나입니다. 네임스페이스 ID가 제공됩니다. |
| 사용자 지정 | [!DNL Experience Cloud]에서 공유되지 않고 조직의 컨텍스트에서 만들어진 고유한 네임스페이스입니다. 값은 검색할 친숙한 이름(&quot;이름&quot; 필드)을 나타냅니다. 네임스페이스 ID가 제공됩니다. |
| integrationCode | 통합 코드 - &quot;사용자 지정&quot;과 유사하지만, 특히 검색할 데이터 소스의 통합 코드로 정의됩니다. 네임스페이스 ID가 제공됩니다. |
| namespaceId | 네임스페이스 서비스를 통해 만들거나 매핑한 네임스페이스의 실제 ID임을 나타냅니다. |
| 미등록 | 네임스페이스 서비스에 정의되지 않고 &quot;있는 그대로&quot; 취하는 자유 형식 문자열입니다. 이러한 종류의 네임스페이스를 처리하는 모든 응용 프로그램은 이러한 네임스페이스와 비교하여 회사 컨텍스트와 데이터 세트에 적합한지 확인하고 처리합니다. 네임스페이스 ID가 제공되지 않습니다. |
| analytics | 네임스페이스 서비스가 아닌 [!DNL Analytics]에 내부적으로 매핑되는 사용자 지정 네임스페이스입니다. 네임스페이스 ID 없이 원래 요청에 지정된 대로 직접 전달됩니다. |
| target | 네임스페이스 서비스가 아니라 [!DNL Target]이 내부적으로 이해하는 사용자 정의 네임스페이스입니다. 네임스페이스 ID 없이 원래 요청에 지정된 대로 직접 전달됩니다. |

## 허용된 제품 값

다음 표에서는 작업 생성 요청의 `include` 속성에서 Adobe 제품을 지정하기 위해 허용된 값에 대해 설명합니다.

| 제품 | `include` 속성에 사용할 값 |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime 인증 | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| 고객 레코드 서비스 | &quot;CRS&quot; |
| 실시간 고객 프로필 | &quot;ProfileService&quot; |
