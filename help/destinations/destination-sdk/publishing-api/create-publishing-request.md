---
description: Adobe Experience Platform Destination SDK을 통해 대상 게시 요청을 제출하기 위해 API 호출 형식을 지정하는 방법을 알아봅니다.
title: 대상 게시 요청 만들기
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 대상 게시 요청 만들기

>[!IMPORTANT]
>
>다른 Experience Platform 고객이 사용할 제품화된(공개) 대상을 제출하는 경우 이 API 끝점만 사용하면 됩니다. 직접 사용할 개인 대상을 만드는 경우 게시 API를 사용하여 대상을 공식적으로 제출할 필요가 없습니다.

>[!IMPORTANT]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

대상을 구성하고 테스트한 후 검토 및 게시를 위해 Adobe에 제출할 수 있습니다. 대상 제출 프로세스의 일부로 수행해야 하는 다른 모든 단계에 대해 [Destination SDK에서 작성된 대상을 검토하려면 제출](../guides/submit-destination.md)을 읽으십시오.

다음과 같은 경우에 게시 요청을 제출하려면 게시 대상 API 엔드포인트를 사용합니다.

* Destination SDK 파트너는 모든 Experience Platform 고객이 사용할 수 있도록 모든 Experience Platform 조직에서 제품화된 대상을 사용할 수 있도록 하고자 합니다.
* 구성에 대해 *모든 업데이트*&#x200B;합니다. 구성 업데이트는 Experience Platform 팀에서 승인하는 새 게시 요청을 제출한 후에만 대상에 반영됩니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 게시 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 게시할 대상 구성 제출 {#create}

`/authoring/destinations/publish` 끝점에 POST 요청을 수행하여 게시할 대상 구성을 제출할 수 있습니다.

**API 형식**

```http
POST /authoring/destinations/publish
```

+++요청

다음 요청은 페이로드에 제공된 매개 변수로 구성된 조직에 게시를 위한 대상을 제출합니다. 아래 페이로드에는 `/authoring/destinations/publish` 끝점에서 허용하는 모든 매개 변수가 포함되어 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시를 위해 제출하는 대상 구성의 대상 ID입니다. [대상 구성 검색](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API 호출을 사용하여 대상 구성의 대상 ID를 가져옵니다. |
| `destinationAccess` | 문자열 | 대상에 대해 `ALL`을(를) 사용하여 모든 Experience Platform 고객의 카탈로그에 표시하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 대상 게시 요청의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

+++

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. Experience Platform 문제 해결 안내서에서 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이제 이 문서를 읽고 대상에 대한 게시 요청을 제출하는 방법을 알 수 있습니다. Adobe Experience Platform 팀이 게시 요청을 검토하고 영업일 기준으로 5일 후에 다시 연락드리겠습니다.
