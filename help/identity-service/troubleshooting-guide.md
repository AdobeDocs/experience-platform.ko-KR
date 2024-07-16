---
keywords: Experience Platform;홈;인기 항목;ID 네임스페이스;ID 네임스페이스
solution: Experience Platform
title: ID 서비스 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform ID 서비스에 대해 자주 묻는 질문에 대한 답변과 일반적인 오류에 대한 문제 해결 안내서를 제공합니다.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---

# ID 서비스 문제 해결 안내서

이 문서에서는 Adobe Experience Platform [!DNL Identity Service]에 대해 자주 묻는 질문에 대한 답변과 일반적인 오류에 대한 문제 해결 안내서를 제공합니다. 일반적으로 [!DNL Platform] API에 대한 질문과 문제 해결은 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

단일 고객을 식별하는 데이터는 종종 브랜드에 참여하기 위해 사용하는 다양한 디바이스 및 시스템에서 조각화됩니다. [!DNL Identity Service]은(는) 이렇게 단편화된 ID를 함께 취합하여 고객 행동을 완벽하게 이해함으로써 효과적인 디지털 경험을 실시간으로 제공할 수 있습니다. 자세한 내용은 [ID 서비스 개요](./home.md)를 참조하세요.

## FAQ

다음은 [!DNL Identity Service]에 대한 FAQ 응답 목록입니다.

## ID 데이터란?

ID 데이터는 개인을 식별하는 데 사용할 수 있는 모든 데이터입니다. 조직 내에서 데이터를 사용하는 방식의 컨텍스트에 따라 ID 데이터에는 사용자 이름, 이메일 주소 및 CRM 시스템의 ID가 포함될 수 있습니다. 익명 사용자는 디바이스 또는 쿠키 ID로 식별할 수 있으므로 ID 데이터는 웹 사이트 또는 서비스의 등록된 사용자로 제한되지 않습니다.

## 데이터 필드에 ID 레이블을 지정하면 어떤 이점이 있습니까?

특정 데이터 필드에 레코드 및 시계열 데이터의 ID로 레이블을 지정하면 데이터의 기본 구조 내에서 ID 관계를 매핑하고 중복 데이터 크로스 채널을 조정할 수 있습니다. 자세한 내용은 [ID 서비스 개요](./home.md)를 참조하세요.

## 알려진 ID 및 익명 ID

알려진 ID는 단독으로 또는 다른 정보와 함께 사용하여 개인을 식별, 연락 또는 위치를 파악할 수 있는 ID 값을 의미합니다. 알려진 ID들의 예들은 이메일 주소들, 전화 번호들, 및 CRM ID들을 포함할 수 있다.

익명 ID는 개인(예: 쿠키 ID)을 식별, 연락 또는 찾기 위해 자체 또는 다른 정보와 함께 사용할 수 없는 ID 값을 의미합니다.

## 개인 ID 그래프란?

개인 ID 그래프는 결합된 ID와 연결된 ID 간의 관계에 대한 개인 맵으로, 조직에만 표시됩니다.

스트리밍 끝점에서 수집되거나 [!DNL Identity Service]에 대해 활성화된 데이터 세트로 전송되는 데이터에 두 개 이상의 ID가 포함되어 있으면 해당 ID가 개인 ID 그래프에 연결됩니다. [!DNL Identity Service]은(는) 이 그래프를 활용하여 특정 소비자 또는 엔터티에 대한 ID를 수집함으로써 ID 결합 및 프로필 병합을 허용합니다.

## XDM 스키마 내에 여러 ID 필드를 만들려면 어떻게 합니까?

[XDM(Experience Data Model)](../xdm/home.md) 스키마는 여러 ID 필드를 지원합니다. XDM 개인 프로필 또는 XDM ExperienceEvent 클래스를 구현하는 스키마 내의 `string` 유형의 모든 데이터 필드에 ID 필드 레이블을 지정할 수 있습니다. 레이블이 지정되면 이러한 필드에 포함된 모든 데이터가 프로필의 ID 맵에 추가됩니다.

사용자 인터페이스를 사용하여 XDM 필드에 ID 필드로 레이블을 지정하는 방법에 대한 자세한 내용은 스키마 편집기 자습서에서 [ID 섹션](../xdm/tutorials/create-schema-ui.md)을 참조하십시오. API를 사용하는 경우 스키마 레지스트리 API 자습서에서 [ID 설명자 섹션](../xdm/tutorials/create-schema-api.md)을(를) 참조하십시오.

## 일부 필드에 ID 레이블을 지정하지 말아야 하는 컨텍스트가 있습니까?

ID 필드는 각 개인에 고유한 값에 대해 예약해야 합니다. 예를 들어 고객 충성도 프로그램을 위한 데이터 세트를 생각해 보십시오. &quot;충성도 수준&quot; 필드(금, 은, 동)는 유용한 ID 필드가 아니지만 충성도 ID(고유 값)는 입니다.

우편 번호 및 IP 주소와 같은 필드는 둘 이상의 개별 사용자에게 적용될 수 있으므로 개인에 대한 ID로 레이블 지정해서는 안 됩니다. 이러한 유형의 필드는 가구 수준 마케팅 전략에 대한 ID로만 레이블이 지정되어야 합니다.

## 내 ID 필드가 예상과 연결되지 않는 이유는 무엇입니까?

ID 서비스 API에서 [`/cluster/members` 끝점](./api/list-cluster-identites.md)을 사용하여 하나 이상의 ID 필드에 대한 연결된 ID를 볼 수 있습니다. 응답이 예상한 연결된 ID를 반환하지 않는 경우 XDM 데이터에 적절한 ID 정보를 제공하고 있는지 확인하십시오. 자세한 내용은 ID 서비스 개요에서 [ID 서비스에 XDM 데이터 제공](./home.md)에 대한 섹션을 참조하십시오.

## ID 네임스페이스란 무엇입니까?

ID 네임스페이스는 ID 필드가 고객의 ID와 관련되는 방식에 대한 컨텍스트를 제공합니다. 예를 들어 &quot;전자 메일&quot; 네임스페이스의 ID 필드는 표준 전자 메일 형식(이름 <span>@emailprovider.com)을 준수해야 하지만, &quot;전화&quot; 네임스페이스를 사용하는 필드는 표준 전화 번호(예: 북미 987-555-1234)를 준수해야 합니다.

네임스페이스는 서로 다른 CRM 시스템 간에 유사한 ID 값을 구분합니다. 예를 들어 회사의 보상 프로그램과 연결된 숫자 충성도 ID가 포함된 프로필을 생각해 보겠습니다. &quot;충성도&quot;라는 네임스페이스는 이 값을 동일한 프로필에도 표시되는 전자 상거래 시스템의 유사한 숫자 ID와 구분합니다.

자세한 내용은 [ID 네임스페이스 개요](./home.md)를 참조하십시오.

## ID를 ID 네임스페이스와 연결하려면 어떻게 해야 합니까?

ID 필드를 만들 때 기존 ID 네임스페이스와 연결해야 합니다. 새 네임스페이스를 ID 필드와 연결하기 전에 API를 사용하여 [만들어야](#how-do-i-create-a-custom-namespace-for-my-organization) 합니다.

API를 사용하여 ID 설명자를 만들 때 네임스페이스를 정의하는 단계별 지침은 스키마 레지스트리 개발자 가이드의 [설명자 만들기](../xdm/tutorials/create-schema-ui.md) 섹션을 참조하십시오. UI에서 스키마 필드를 ID로 표시하려면 [스키마 편집기 자습서](../xdm/tutorials/create-schema-api.md)의 단계를 따르십시오.

## Experience Platform에서 제공하는 표준 ID 네임스페이스는 무엇입니까? {#standard-namespaces}

표준 ID 네임스페이스는 모든 조직에서 사용할 수 있는 네임스페이스입니다. 사용 가능한 표준 네임스페이스의 전체 목록은 [ID 네임스페이스 개요](./features/namespaces.md)를 참조하십시오.

## 조직에서 사용할 수 있는 ID 네임스페이스 목록은 어디에서 찾을 수 있습니까?

[ID 서비스 API](https://www.adobe.io/experience-platform-apis/references/identity-service)를 사용하면 `/idnamespace/identities` 끝점에 GET 요청을 하여 조직에서 사용 가능한 모든 ID 네임스페이스를 나열할 수 있습니다. 자세한 내용은 ID 서비스 API 개요의 [사용 가능한 네임스페이스 나열](./api/list-namespaces.md) 섹션을 참조하십시오.

## 내 조직에 대한 사용자 정의 네임스페이스를 만들려면 어떻게 해야 합니까?

[ID 서비스 API](https://www.adobe.io/experience-platform-apis/references/identity-service)를 사용하면 `/idnamespace/identities` 끝점에 POST 요청을 하여 조직에 대한 사용자 지정 ID 네임스페이스를 만들 수 있습니다. 자세한 내용은 ID 서비스 API 개요에서 [사용자 지정 네임스페이스 만들기](./api/create-custom-namespace.md)에 대한 섹션을 참조하십시오.

## 복합 ID 및 XID란 무엇입니까?

ID는 조합 ID 또는 XID에 의해 API 호출에서 참조됩니다. 복합 ID는 ID 값과 네임스페이스가 포함된 ID를 나타냅니다. XID는 복합 ID(ID와 네임스페이스)와 동일한 구문을 나타내는 단일 값 식별자이며, ID 서비스에서 지속되는 경우 새 ID에 자동으로 할당됩니다. 자세한 내용은 [ID 서비스 API 개요](./home.md)를 참조하십시오.

## ID 서비스는 PII(개인 식별 정보)를 어떻게 처리합니까?

ID 서비스에는 전화 번호 및 전자 메일에 대한 해시된 ID 값 수집을 지원하는 표준 네임스페이스가 있습니다. 그러나 값의 해싱은 사용자가 담당합니다. 플랫폼으로 수집되는 데이터 해시에 대한 자세한 내용은 [[!DNL Data Prep] 매핑 함수 가이드](../data-prep/functions.md#hashing)를 참조하세요.

## PII 기반 ID를 해싱할 때 고려할 사항이 있습니까?

해시된 PII 값을 ID 서비스로 보내는 경우 데이터 세트에서 동일한 암호화 방법을 사용해야 합니다. 이렇게 하면 데이터 세트 간에 동일한 ID 값이 동일한 해시된 값을 생성하고 ID 그래프에서 적절하게 일치하고 연결할 수 있습니다.

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

## ID 그래프 페이지 또는 API에 액세스할 수 없는 이유는 무엇입니까?

ID 그래프 데이터를 보려면 플랫폼 관리자가 `view-identity-graph` 권한으로 프로비전해야 합니다. 이 권한이 없으면 ID 그래프 뷰어 페이지 및 Platform API를 호출할 때 권한 거부 메시지를 받게 됩니다. 사용 권한에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하세요.

## 문제 해결

다음 섹션에서는 [!DNL Identity Service] API 작업 중 발생할 수 있는 특정 오류 코드 및 예기치 않은 동작에 대한 문제 해결 제안을 제공합니다.

## 오류 메시지 [!DNL Identity Service]개

다음은 [!DNL Identity Service] API를 사용할 때 발생할 수 있는 오류 메시지 목록입니다.

### 필수 쿼리 매개 변수 누락

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

이 오류는 필수 쿼리 매개 변수가 요청 경로에 포함되지 않은 경우 표시됩니다. 오류 메시지의 `detail`은(는) 누락된 매개 변수의 이름을 제공합니다. 이 오류 메시지의 변형은 다음과 같습니다.

- 필수 쿼리 매개 변수 누락 - nsId
- 필수 쿼리 매개 변수 누락 - ID
- 필수 쿼리 매개 변수 누락 - xid 또는 (nsid,id)
- 필수 쿼리 매개 변수 누락 - targetNs
- 필수 쿼리 매개 변수 누락 - xids 또는 compositeXids

표시된 매개 변수를 요청 경로에 제대로 포함했는지 확인한 후 다시 시도하십시오.

### 타임스탬프는 최근 180일 이내에 있어야 합니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service]이(가) 180일 넘는 데이터를 삭제합니다. 이 오류 메시지는 이보다 오래된 데이터에 액세스하려고 할 때 표시됩니다.

### 단일 호출에는 1000개의 XID로 제한됩니다

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

이 오류 메시지는 단일 API 호출에서 허용되는 최대 [XID](#what-are-composite-identities-and-xids) 수 이상의 ID 정보를 검색하려고 할 때 표시됩니다. 이 문제를 해결하려면 요청의 XID 수를 표시된 제한 이하로 줄이십시오.


### 단일 호출에는 1000개의 compositeXid에 대한 제한이 있습니다

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

이 오류 메시지는 단일 API 호출에서 허용되는 최대 [복합 ID](#what-are-composite-identities-and-xids) 수 이상의 ID 정보를 검색하려고 할 때 표시됩니다. 이 문제를 해결하려면 요청의 복합 ID 수를 표시된 제한 이하로 줄이십시오.

### 지정한 그래프 유형이 잘못되었습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

이 오류 메시지는 `graph-type` 쿼리 매개 변수에 요청 경로에서 잘못된 값이 지정될 때 표시됩니다. 지원되는 그래프 유형을 알아보려면 [!DNL Identity Service] 개요에서 [ID 그래프](./home.md)의 섹션을 참조하십시오.

### 서비스 토큰에 유효한 범위가 없습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

이 오류 메시지는 조직에 [!DNL Identity Service]에 대한 적절한 권한이 제공되지 않은 경우 표시됩니다. 이 문제를 해결하려면 시스템 관리자에게 문의하십시오.

### 게이트웨이 서비스 토큰이 잘못되었습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

이 오류의 경우 액세스 토큰이 잘못되었습니다. 액세스 토큰은 24시간마다 만료되며 [!DNL Platform] API를 계속 사용하려면 다시 생성해야 합니다. 새 액세스 토큰 생성에 대한 지침은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오.

### 인증 서비스 토큰이 잘못되었습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

이 오류의 경우 액세스 토큰이 잘못되었습니다. 액세스 토큰은 24시간마다 만료되며 [!DNL Platform] API를 계속 사용하려면 다시 생성해야 합니다. 새 액세스 토큰 생성에 대한 지침은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오.

### 사용자 토큰에 유효한 제품 컨텍스트가 없습니다.

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

이 오류 메시지는 액세스 토큰이 [!DNL Experience Platform] 통합에서 생성되지 않은 경우 표시됩니다. [!DNL Experience Platform] 통합을 위한 새 액세스 토큰을 생성하는 방법은 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 참조하십시오.

### ID 및 네임스페이스 코드에서 네이티브 XID를 가져올 때 내부 오류 발생

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

[!DNL Identity Service]이(가) ID를 유지하면 해당 ID의 ID와 연결된 네임스페이스 ID에 XID라는 고유 식별자가 할당됩니다. 이 메시지는 주어진 ID 값 및 네임스페이스에 대한 XID를 찾는 프로세스 중에 오류가 발생하는 경우 표시됩니다.

### IMS 조직이 [!DNL Identity Service] 사용에 대해 프로비저닝되지 않았습니다.

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

이 오류 메시지는 조직에 [!DNL Identity Service]에 대한 적절한 권한이 제공되지 않은 경우 표시됩니다. 이 문제를 해결하려면 시스템 관리자에게 문의하십시오.

### 내부 서버 오류

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

이 오류는 [!DNL Platform] 서비스 호출 실행 시 예기치 않은 예외가 발생할 때 표시됩니다. 가장 좋은 방법은 이 오류를 수신할 때 시간 간격을 두고 몇 번 요청을 다시 시도하는 자동화된 호출을 프로그래밍하는 것입니다. 문제가 지속되면 시스템 관리자에게 문의하십시오.

## 일괄 처리 수집 오류 코드

[!DNL Identity Service]은(는) 일괄 처리 수집을 사용하여 [!DNL Platform]에 업로드된 레코드 및 시계열 데이터에서 ID 데이터를 수집합니다. 일괄 처리 수집은 비동기 프로세스이므로 오류를 보려면 일괄 처리에 대한 세부 정보를 확인해야 합니다. 배치가 완료될 때까지 배치가 진행됨에 따라 오류가 누적됩니다.

다음은 [일괄 처리 수집 API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)를 사용할 때 발생할 수 있는 [!DNL Identity Service]과(와) 관련된 오류 메시지 목록입니다.

### 알 수 없는 XDM 스키마

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service]은(는) 각각 [!DNL Profile] 또는 [!DNL ExperienceEvent] 클래스를 준수하는 레코드 또는 시계열 데이터의 ID만 사용합니다. 두 클래스를 준수하지 않는 [!DNL Identity Service]에 대한 데이터를 수집하려고 하면 이 오류가 트리거됩니다.

### 처리된 배치의 처음 100행에 0개의 유효한 ID가 있습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

이 오류는 배치의 처음 100개 행에 ID가 없을 때 표시됩니다. 그러나 이 오류는 후속 레코드에서 ID를 찾을 수 없음을 명확히 나타내지는 않습니다.

### XDM 레코드당 ID가 1개만 있으므로 건너뛴 레코드

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service]은(는) 단일 레코드에 둘 이상의 ID 값이 있는 경우에만 ID를 연결합니다. 이 오류 메시지는 수집된 각 일괄 처리에 대해 한 번 발생하며 하나의 ID만 찾을 수 있고 ID 그래프가 변경되지 않은 레코드 수를 표시합니다.

### 이 IMS 조직에 대한 네임스페이스 코드가 등록되지 않았습니다.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

이 오류는 수집된 레코드가 연결된 네임스페이스가 없거나 조직에서 액세스할 수 없는 ID를 제공하는 경우 표시됩니다.

### IMS 조직이 개인 ID 그래프에 대해 프로비저닝되지 않았으므로 배치 수집 건너뛰기

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

일괄 처리 데이터를 수집할 때 조직에 [!DNL Identity Service]에 대한 적절한 권한이 제공되지 않은 경우 이 오류 메시지가 표시됩니다. 이 문제를 해결하려면 시스템 관리자에게 문의하십시오.

### 내부 오류

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

이 오류는 일괄 처리 수집 중에 예기치 않은 예외가 발생할 때 표시됩니다. 가장 좋은 방법은 이 오류를 수신할 때 시간 간격을 두고 몇 번 요청을 다시 시도하는 자동화된 호출을 프로그래밍하는 것입니다. 문제가 지속되면 시스템 관리자에게 문의하십시오.
