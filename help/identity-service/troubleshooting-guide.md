---
keywords: Experience Platform;home;popular topics;identity namespace;Identity namespace
solution: Experience Platform
title: Adobe Experience Platform ID 서비스 문제 해결 가이드
topic: troubleshooting
description: 이 문서에서는 Adobe Experience Platform ID 서비스에 대한 FAQ와 일반적인 오류에 대한 문제 해결 가이드를 제공합니다.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '2248'
ht-degree: 1%

---


# ID 서비스 문제 해결 가이드

이 문서에서는 Adobe Experience Platform에 대한 FAQ와 일반적인 오류에 대한 문제 해결 안내서 [!DNL Identity Service]를 제공합니다. 일반적으로 API에 대한 질문 및 문제 해결 [!DNL Platform] 은 [Adobe Experience Platform API 문제 해결 가이드를 참조하십시오](../landing/troubleshooting.md).

단일 고객을 식별하는 데이터는 브랜드에 참여하는 데 사용하는 다양한 디바이스와 시스템에서 단편화되어 있는 경우가 많습니다. [!DNL Identity Service] 분열된 ID를 취합하여 고객 행동에 대한 완벽한 이해를 돕고 효과적이고 효과적인 디지털 경험을 실시간으로 제공할 수 있습니다. 자세한 내용은 ID 서비스 [개요를 참조하십시오](./home.md).

## FAQ

다음은 FAQ의 목록입니다 [!DNL Identity Service].

## ID 데이터란?

ID 데이터는 개인을 식별하는 데 사용할 수 있는 모든 데이터입니다. 조직 내에서 데이터가 사용되는 방식에 따라 ID 데이터에는 CRM 시스템의 사용자 이름, 이메일 주소 및 ID가 포함될 수 있습니다. 익명 사용자는 자신의 디바이스 또는 쿠키 ID로 식별될 수 있으므로 ID 데이터는 웹 사이트 또는 서비스의 등록된 사용자에게만 국한되지 않습니다.

## 데이터 필드를 ID로 표시하면 어떤 이점이 있습니까?

특정 데이터 필드에 레코드 및 시간 시리즈 데이터의 ID로 레이블을 지정하면 데이터의 자연 구조 내에서 ID 관계를 매핑하고 중복 데이터 크로스 채널을 조정할 수 있습니다. 자세한 내용은 [ID 서비스 개요를](./home.md) 참조하십시오.

## 알려진 것과 익명의 신원은?

알려진 ID는 개인 식별, 연락처 또는 찾기 위해 단독으로 또는 기타 정보와 함께 사용할 수 있는 ID 값을 의미합니다. 알려진 ID의 예에는 이메일 주소, 전화 번호 및 CRM ID가 포함될 수 있습니다.

익명 ID는 개인(예: 쿠키 ID)을 식별, 연락처 또는 찾기 위해 자체 또는 기타 정보와 함께 사용할 수 없는 ID 값을 의미합니다.

## 개인 ID 그래프란?

개인 ID 그래프는 연결된 ID와 연결된 ID 사이의 관계를 비공개 맵으로 조직에서만 볼 수 있습니다.

스트리밍 끝점에서 수집되거나 활성화된 데이터 세트에 두 개 이상의 ID가 포함된 경우 [!DNL Identity Service]이러한 ID는 개인 ID 그래프에 연결됩니다. [!DNL Identity Service] 이 그래프를 활용하여 특정 소비자 또는 엔티티에 대한 ID를 추출하고 ID 연결 및 프로필 병합을 허용합니다.

## XDM 스키마 내에서 여러 ID 필드를 만들려면 어떻게 해야 합니까?

[XDM(Experience Data Model)](../xdm/home.md) 스키마는 여러 ID 필드를 지원합니다. XDM 개인 프로필 또는 XDM ExperienceEvent 클래스를 구현하는 스키마 `string` 내의 모든 유형의 데이터 필드는 ID 필드로 레이블이 지정될 수 있습니다. 레이블이 지정되면 이 필드에 포함된 데이터는 프로필의 ID 맵에 추가됩니다.

사용자 인터페이스를 사용하여 XDM 필드에 ID 필드로 레이블을 지정하는 방법에 대한 자세한 내용은 스키마 편집기 자습서의 [ID 섹션](../xdm/tutorials/create-schema-ui.md) 을 참조하십시오. API를 사용하는 경우 스키마 레지스트리 API 자습서의 [ID 설명자 섹션을](../xdm/tutorials/create-schema-api.md) 참조하십시오.

## 일부 필드가 ID로 레이블이 지정되어서는 안 되는 컨텍스트가 있습니까?

ID 필드는 각 개인에 고유한 값에 대해 예약해야 합니다. 예를 들어 고객 충성도 프로그램의 데이터 세트를 고려합니다. &quot;충성도 수준&quot; 필드(금, 은, 브론즈)는 유용한 ID 필드가 아니지만, 충성도 ID(고유한 값)는 유용하지 않습니다.

둘 이상의 개별 사람에게 적용할 수 있으므로 ZIP 코드 및 IP 주소와 같은 필드는 개인의 ID로 레이블을 지정할 수 없습니다. 이러한 유형의 필드는 가족 수준의 마케팅 전략에 대한 ID로 표시되어야 합니다.

## 내 ID 필드가 내 예상과 연결되지 않는 이유는 무엇입니까?

ID 서비스 API의 [`/cluster/members` 끝점을](./api/list-cluster-identites.md) 사용하면 하나 이상의 ID 필드에 대해 연결된 ID를 볼 수 있습니다. 응답에서 예상한 연결된 ID를 반환하지 않는 경우 XDM 데이터에 적절한 ID 정보를 제공하는지 확인하십시오. 자세한 내용은 ID 서비스 [개요에서 XDM 데이터를 ID 서비스에](./home.md) 제공하는 섹션을 참조하십시오.

## ID 네임스페이스란 무엇입니까?

ID 네임스페이스는 ID 필드가 고객 ID와 어떻게 관련되는지 컨텍스트를 제공합니다. 예를 들어, &quot;이메일&quot; 네임스페이스의 ID 필드는 표준 이메일 형식(name<span>@emailprovider.com)을 따라야 하지만 &quot;Phone&quot; 네임스페이스를 사용하는 필드는 표준 전화 번호(예: 북미 지역의 987-555-1234)를 준수해야 합니다.

네임스페이스는 서로 다른 CRM 시스템 간에 유사한 ID 값을 구별합니다. 예를 들어, 회사의 보상 프로그램과 관련된 숫자 충성도 ID가 포함된 프로필을 고려해 보십시오. &quot;충성도&quot;의 네임스페이스는 이 값을 동일한 프로필에 표시되는 전자 상거래 시스템의 유사한 숫자 ID와 구분합니다.

자세한 내용은 [ID 네임스페이스 개요를](./home.md) 참조하십시오.

## ID를 ID 네임스페이스와 연결하려면 어떻게 해야 합니까?

ID 필드는 만들 때 기존 ID 네임스페이스와 연결해야 합니다. 새로운 네임스페이스는 API를 사용하여 [만들어야 ID](#how-do-i-create-a-custom-namespace-for-my-organization) 필드에 연결할 수 있습니다.

API를 사용하여 ID 설명자를 만들 때 네임스페이스를 정의하는 단계별 지침을 보려면 스키마 레지스트리 개발자 안내서에서 설명자 [를 만드는](../xdm/tutorials/create-schema-ui.md) 섹션을 참조하십시오. UI에서 스키마 필드를 ID로 표시하려면 스키마 편집기 자습서의 [단계를 따릅니다](../xdm/tutorials/create-schema-api.md).

## Experience Platform에서 제공하는 표준 ID 네임스페이스는 무엇입니까? {#standard-namespaces}

Experience Platform 내의 모든 조직에서 사용할 수 있도록 다음과 같은 표준 네임스페이스가 제공됩니다.

| 표시 이름 | ID | 코드 | 설명 |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | 레거시 이름:&quot;Adobe AudienceManager&quot; |
| ECID | 4 | ECID | 별칭:&quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; |
| 이메일 | 6 | 이메일 |  |
| 이메일(SHA256, 소문자 구분) | 11 | 이메일 | 사전 해시된 이메일의 표준 네임스페이스입니다. 이 네임스페이스에 제공된 값은 SHA-256으로 해싱하기 전에 소문자로 변환됩니다. |
| 전화 | 7 | 전화 |  |
| Windows AID | 8 | WAID |  |
| AdCloud | 411 | AdCloud | 별칭:Ad Cloud |
| Adobe Target | 9 | TNTID | Target ID |
| Google 광고 ID | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | 광고주의 ID |

## 조직에서 사용할 수 있는 ID 네임스페이스 목록은 어디에서 찾을 수 있습니까?

ID [서비스 API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)사용하면 `/idnamespace/identities` 종단점에 GET 요청을 하여 조직에 대해 사용 가능한 모든 ID 네임스페이스를 나열할 수 있습니다. 자세한 내용은 Identity Service API [개요에서 사용 가능한 네임스페이스](./api/list-namespaces.md) 목록에 대한 섹션을 참조하십시오.

## 조직의 사용자 지정 네임스페이스를 만들려면 어떻게 해야 합니까?

ID [서비스 API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)사용하면 `/idnamespace/identities` 종단점에 POST 요청을 하여 조직에 대한 사용자 지정 ID 네임스페이스를 만들 수 있습니다. 자세한 내용은 ID 서비스 API 개요에서 사용자 정의 네임스페이스 [](./api/create-custom-namespace.md) 만들기에 대한 섹션을 참조하십시오.

## 복합 ID와 XID란 무엇입니까?

ID는 합성 ID 또는 XID로 API 호출에서 참조됩니다. 복합 ID는 ID 값과 네임스페이스를 포함하는 ID를 나타냅니다. XID는 복합 ID(ID 및 네임스페이스)와 동일한 구문을 나타내는 단일 값 식별자로, Identity Service에서 지속되는 경우 자동으로 새 ID에 할당됩니다. 자세한 내용은 [ID 서비스 API 개요를](./home.md) 참조하십시오.

## ID 서비스는 PII(개인 식별 정보)를 어떻게 처리합니까?

ID 서비스는 값을 지속하기 전에 PII의 강력한 단방향 암호화 해시를 만듭니다. &quot;Phone&quot; 및 &quot;Email&quot; 네임스페이스의 ID 데이터는 SHA-256을 사용하여 자동으로 해시되고 &quot;Email&quot; 값은 해싱 전에 소문자로 자동 변환됩니다.

## Platform으로 보내기 전에 모든 PII를 암호화해야 합니까?

PII 데이터를 플랫폼에 인제스트하기 전에 수동으로 암호화할 필요는 없습니다. Platform(플랫폼)은 모든 해당 데이터 필드에 `I1` 데이터 사용 레이블을 적용하여 수집 시 이러한 필드를 해시된 ID 값으로 자동 변환합니다.

데이터 사용 레이블을 적용하고 관리하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 자습서를 참조하십시오](../data-governance/labels/user-guide.md).

## PII 기반 ID를 해시 할 때 고려해야 할 사항이 있습니까?

해시된 PII 값을 ID 서비스로 전송하는 경우 데이터 세트에서 동일한 암호화 방법을 사용해야 합니다. 이렇게 하면 데이터 세트 간에 동일한 ID 값이 해시된 동일한 값을 생성하며 ID 그래프에서 적절하게 대응하고 연결할 수 있습니다.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## 문제 해결

다음 섹션에서는 [!DNL Identity Service] API 작업 시 발생할 수 있는 특정 오류 코드와 예기치 않은 동작에 대한 문제 해결 제안을 제공합니다.

## [!DNL Identity Service] 오류 메시지

다음은 [!DNL Identity Service] API를 사용할 때 발생할 수 있는 오류 메시지 목록입니다.

### 필수 쿼리 매개 변수가 없습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

이 오류는 필수 쿼리 매개 변수가 요청 경로에 포함되지 않은 경우 표시됩니다. 오류 메시지 `detail` 는 누락된 매개 변수의 이름을 제공합니다. 이 오류 메시지의 변형은 다음과 같습니다.

- 필요한 쿼리 매개 변수가 없습니다. nsId
- 필수 쿼리 매개 변수 - id가 없습니다.
- 필요한 쿼리 매개 변수 - xid 또는 (nsid,id)가 없습니다.
- 필수 쿼리 매개 변수 - targetNs이 없습니다.
- 필수 쿼리 매개 변수 누락 - xds 또는 compositeXids

다시 시도하기 전에 요청 경로에 표시된 매개 변수를 올바르게 포함하고 있는지 확인하십시오.

### 타임스탬프는 마지막 180일 이내여야 합니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 180일 이전의 데이터를 삭제합니다. 이 오류 메시지는 이보다 오래된 데이터에 액세스하려고 하면 표시됩니다.

### 단일 호출에는 1000개의 XID로 제한됩니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

이 오류 메시지는 단일 API 호출에서 허용되는 최대 XID 수 이상의 ID 정보 [를](#what-are-composite-identities-and-xids) 검색하려고 할 때 표시됩니다. 이 문제를 해결하기 위해 요청에 있는 XID 수를 표시된 제한 아래로 줄입니다.


### 단일 호출에서 1000개의 compositeXids에 대한 제한 사항이 있습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

이 오류 메시지는 단일 API 호출에서 허용되는 최대 [복합 ID](#what-are-composite-identities-and-xids) 수를 초과하여 ID 정보를 검색하려고 할 때 표시됩니다. 이 문제를 해결하기 위해 요청의 복합 ID 수를 표시된 제한 아래로 줄입니다.

### 지정한 그래프 유형이 잘못되었습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

이 오류 메시지는 `graph-type` 쿼리 매개 변수가 요청 경로에 잘못된 값을 지정되면 표시됩니다. 지원되는 그래프 유형을 살펴보려면 [개요의 ID 그래프에](./home.md) [!DNL Identity Service] 대한 섹션을 참조하십시오.

### 서비스 토큰의 범위가 잘못되었습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

이 오류 메시지는 IMS 조직에 적절한 권한이 제공되지 않을 때 표시됩니다 [!DNL Identity Service]. 이 문제를 해결하려면 시스템 관리자에게 문의하십시오.

### 게이트웨이 서비스 토큰이 잘못되었습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

이 오류의 경우 액세스 토큰이 잘못되었습니다. 액세스 토큰은 24시간마다 만료되며 [!DNL Platform] API를 계속 사용하려면 다시 생성해야 합니다. 새 액세스 토큰을 생성하는 방법에 대한 지침은 [인증 자습서를](../tutorials/authentication.md) 참조하십시오.

### 인증 서비스 토큰이 잘못되었습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

이 오류의 경우 액세스 토큰이 잘못되었습니다. 액세스 토큰은 24시간마다 만료되며 [!DNL Platform] API를 계속 사용하려면 다시 생성해야 합니다. 새 액세스 토큰을 생성하는 방법에 대한 지침은 [인증 자습서를](../tutorials/authentication.md) 참조하십시오.

### 사용자 토큰에 올바른 제품 컨텍스트가 없습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

이 오류 메시지는 [!DNL Experience Platform] 통합에서 액세스 토큰이 생성되지 않은 경우에 표시됩니다. 통합을 위한 새 액세스 토큰을 생성하는 방법에 대한 지침은 [인증 자습서를](../tutorials/authentication.md) 참조하십시오 [!DNL Experience Platform] .

### ID 및 네임스페이스 코드에서 기본 XID를 가져오는 동안 내부 오류가 발생했습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

ID가 [!DNL Identity Service] 지속되면 ID의 ID와 관련 네임스페이스 ID에 XID라는 고유한 식별자가 할당됩니다. 이 메시지는 지정된 ID 값과 네임스페이스에 대한 XID를 찾는 동안 오류가 발생하는 경우 표시됩니다.

### IMS 조직이 [!DNL Identity Service] 사용되도록 제공되지 않습니다.

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

이 오류 메시지는 IMS 조직에 적절한 권한이 제공되지 않을 때 표시됩니다 [!DNL Identity Service]. 이 문제를 해결하려면 시스템 관리자에게 문의하십시오.

### 내부 서버 오류

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

이 오류는 [!DNL Platform] 서비스 호출 실행에서 예기치 않은 예외가 발생하는 경우에 표시됩니다. 이 오류를 수신할 때 시간 간격에서 요청을 몇 번 다시 시도하도록 자동화된 호출을 프로그래밍하는 것이 좋습니다. 문제가 계속되면 시스템 관리자에게 문의하십시오.

## 일괄 처리 처리 오류 코드

[!DNL Identity Service] 일괄 처리 습성을 사용하여 업로드된 레코드 및 시간 시리즈 데이터의 ID 데이터 [!DNL Platform] 를 인제스트합니다. 일괄 처리가 비동기 프로세스이므로, 일괄 처리에 대한 세부 사항을 확인하여 오류를 확인해야 합니다. 배치가 완료될 때까지 배치가 진행되면 오류가 누적됩니다.

다음은 [!DNL Identity Service] 데이터 통합 API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)사용 시 발생할 수 있는 관련 오류 메시지 목록입니다.

### 알 수 없는 XDM 스키마

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 각각 [!DNL Profile] 또는 [!DNL ExperienceEvent] 클래스를 준수하는 레코드 또는 타임 시리즈 데이터에 대해 ID만 사용합니다. 어느 클래스와 일치하지 않는 데이터 [!DNL Identity Service] 를 인제스트하려고 하면 이 오류가 발생합니다.

### 처리된 배치의 처음 100개 행에 0개의 유효한 ID가 있습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

이 오류는 일괄 처리의 처음 100개 행이 ID를 표시하지 않을 때 표시됩니다. 하지만 이 오류는 이후 레코드에서 ID가 없다는 결론을 내지는 않습니다.

### XDM 레코드당 ID가 1개이므로 레코드를 건너뜁니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 단일 레코드가 두 개 이상의 ID 값을 나타낼 때 ID만 연결합니다. 이 오류 메시지는 인제스트된 각 배치에 대해 한 번 발생하고 ID가 하나만 찾을 수 있고 ID 그래프가 변경되지 않는 레코드 수를 표시합니다.

### 네임스페이스 코드가 이 IMS 조직에 등록되어 있지 않습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

이 오류는 인제스트된 레코드가 연결된 네임스페이스가 없거나 IMS 조직에서 액세스할 수 없는 ID를 나타낼 때 표시됩니다.

### IMS 조직으로서 일괄 처리를 건너뜁니다. 개인 ID 그래프에 대해 제공되지 않습니다.

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

일괄 처리 데이터를 인제스트할 때 이 오류 메시지는 IMS가 조직에 적절한 권한이 제공되지 않을 때 표시됩니다 [!DNL Identity Service]. 이 문제를 해결하려면 시스템 관리자에게 문의하십시오.

### 내부 오류

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

이 오류는 일괄 처리 중 예기치 않은 예외가 발생하는 경우에 표시됩니다. 이 오류를 수신할 때 시간 간격에서 요청을 몇 번 다시 시도하도록 자동화된 호출을 프로그래밍하는 것이 좋습니다. 문제가 계속되면 시스템 관리자에게 문의하십시오.
