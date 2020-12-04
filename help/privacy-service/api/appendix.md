---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 허용되는 ID 네임스페이스 및 한정자
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 10%

---


# 부록

## 표준 ID 네임스페이스 {#standard-namespaces}

전송될 모든 ID는 특정 ID 네임스페이스에서 제공되어야 [!DNL Privacy Service] 합니다. Identity namespaces are a component of [Adobe Experience Platform Identity Service](../../identity-service/home.md) that indicate the context to which an identity relates.

다음 표에서는 관련 값과 함께 일반적으로 사용되는 사전 정의된 ID 유형 [!DNL Experience Platform]`namespace` 에 대해 설명합니다.

| ID 유형 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 이메일 | 이메일 | 6 |
| 전화 | 전화 | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] 광고주의 ID | IDFA | 20915 |
| [!DNL Google] 광고 ID | GAID | 20914 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>각 ID 유형에는 `namespaceId` 정수 값이 있으며, ID의 속성을 &quot;namespaceId&quot;로 설정할 때 `namespace` 문자열 대신 사용할 수 있습니다 `type` . 자세한 내용은 [네임스페이스 한정자](#namespace-qualifiers) 섹션을 참조하십시오.

API의 종단점에 GET 요청을 함으로써 조직에서 사용 중인 ID 네임스페이스 목록을 검색할 수 `idnamespace/identities` [!DNL Identity Service] 있습니다. 자세한 내용은 [ID 서비스 개발자 가이드를](../../identity-service/api/getting-started.md) 참조하십시오.

## 네임스페이스 한정자

API에서 값 `namespace` 을 지정할 때 해당 매개 변수 [!DNL Privacy Service] 에 **네임스페이스 한정자를** 포함해야 `type` 합니다. 다음 표에서는 서로 다른 허용되는 네임스페이스 한정자에 대해 설명합니다.

| 한정자 | 정의 |
| --------- | ---------- |
| standard | 개별 조직 데이터 세트(예: 이메일, 전화 번호 등)와 연결되지 않고 전체적으로 정의된 표준 네임스페이스 네임스페이스 ID가 제공됩니다. |
| 사용자 지정 | 조직 컨텍스트에서 만들어지는 고유한 네임스페이스이며, 조직 간에 공유되지 않습니다 [!DNL Experience Cloud]. 이 값은 검색할 친숙한 이름(&quot;이름&quot; 필드)을 나타냅니다. 네임스페이스 ID가 제공됩니다. |
| integrationCode | 통합 코드 - &quot;사용자 지정&quot;과 유사하지만, 검색할 데이터 소스의 통합 코드로 구체적으로 정의됩니다. 네임스페이스 ID가 제공됩니다. |
| namespaceId | 네임스페이스 서비스를 통해 만들거나 매핑한 네임스페이스의 실제 ID임을 나타냅니다. |
| 미등록 | 네임스페이스 서비스에서 정의되지 않고 &quot;있는 그대로&quot; 취하는 자유 형식 문자열입니다. 이러한 종류의 네임스페이스를 처리하는 모든 응용 프로그램은 이러한 네임스페이스와 비교하여 회사 컨텍스트 및 데이터 세트에 적합한지 확인하고 처리합니다. 네임스페이스 ID가 제공되지 않습니다. |
| analytics | 네임스페이스 서비스가 아니라 내부적으로 매핑되는 사용자 지정 네임스페이스 [!DNL Analytics]입니다. 이것은 네임스페이스 ID 없이 원래 요청에 의해 지정된 대로 직접 전달됩니다 |
| target | 네임스페이스 서비스가 아니라 내부에서 [!DNL Target]이해하는 사용자 정의 네임스페이스입니다. 이것은 네임스페이스 ID 없이 원래 요청에 의해 지정된 대로 직접 전달됩니다 |

## 승인된 제품 값

다음 표에서는 작업 생성 요청의 속성에 Adobe 제품을 지정하기 위해 허용된 값을 `include` 개략적으로 설명합니다.

| 제품 | 속성에 사용할 `include` 값 |
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