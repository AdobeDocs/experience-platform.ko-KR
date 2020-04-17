---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 허용되는 ID 네임스페이스 및 한정자
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# 부록

## 표준 ID 네임스페이스

개인정보 보호 서비스로 전송되는 모든 ID는 특정 ID 네임스페이스로 제공되어야 합니다. ID 네임스페이스는 ID [와 관련된 컨텍스트를](../../identity-service/home.md) 나타내는 Adobe Experience Platform Identity Service의 구성 요소입니다.

다음 표는 경험 플랫폼에서 사용할 수 있도록 미리 정의된 여러 가지 ID 유형과 관련 `namespace` 값을 대략적으로 보여줍니다.

| ID 유형 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 이메일 | 이메일 | 6 |
| 전화 | 전화 | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| 광고주용 Apple ID | IDFA | 20915 |
| Google 광고 ID | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] 또한 각 ID 유형에는 `namespaceId` 정수 값이 있으며, ID의 `namespace` `type` 속성을 &quot;namespaceId&quot;로 설정할 때 문자열 대신 사용할 수 있습니다. 자세한 내용은 [네임스페이스 한정자의](#namespace-qualifiers) 섹션을 참조하십시오.

ID 서비스 API의 `idnamespace/identities` 종단점에 GET 요청을 만들어 조직에서 사용 중인 ID 네임스페이스 목록을 검색할 수 있습니다. 자세한 내용은 [ID 서비스 개발자 안내서를](../../identity-service/api/getting-started.md) 참조하십시오.

## 네임스페이스 한정자

Privacy Service API에서 `namespace` 값을 지정할 때 **네임스페이스 한정자는** 해당 `type` 매개 변수에 포함되어야 합니다. 다음 표에서는 허용된 서로 다른 네임스페이스 한정자에 대해 간략하게 설명합니다.

| 한정자 | 정의 |
| --------- | ---------- |
| standard | 개별 조직 데이터 세트(예: 이메일, 전화 번호 등)와 연결되지 않고 전체적으로 정의된 표준 네임스페이스 중 하나입니다. 네임스페이스 ID가 제공됩니다. |
| 사용자 지정 | Experience Cloud에서 공유되지 않고 조직 컨텍스트에서 작성된 고유한 네임스페이스입니다. 이 값은 검색할 친숙한 이름(&quot;이름&quot; 필드)을 나타냅니다. 네임스페이스 ID가 제공됩니다. |
| integrationCode | 통합 코드 - &quot;사용자 정의&quot;와 유사하지만, 검색할 데이터 소스의 통합 코드로 구체적으로 정의됩니다. 네임스페이스 ID가 제공됩니다. |
| namespaceId | 값이 네임스페이스 서비스를 통해 만들거나 매핑한 네임스페이스의 실제 ID임을 나타냅니다. |
| 미등록 | 네임스페이스 서비스에서 정의되지 않고 &quot;있는 그대로&quot; 취하는 자유 형식 문자열입니다. 이러한 유형의 네임스페이스를 처리하는 모든 응용 프로그램은 이러한 네임스페이스에 대해 확인하며 회사 컨텍스트 및 데이터 세트에 적합한지 여부를 처리합니다. 네임스페이스 ID가 제공되지 않습니다. |
| analytics | 네임스페이스 서비스가 아닌 Analytics에서 내부적으로 매핑되는 사용자 지정 네임스페이스입니다. 이것은 네임스페이스 ID 없이 원래 요청에 의해 지정된 대로 직접 전달됩니다 |
| target | 네임스페이스 서비스가 아니라 Target에서 내부적으로 이해하는 사용자 정의 네임스페이스입니다. 이것은 네임스페이스 ID 없이 원래 요청에 의해 지정된 대로 직접 전달됩니다 |

## 승인된 제품 값

다음 표에서는 작업 생성 요청의 속성에 Adobe 제품을 지정하는 데 허용된 값에 대해 `include` 개괄적으로 설명합니다.

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