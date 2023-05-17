---
description: Adobe Experience Platform Destination SDK을 통해 대상 게시 요청을 제출하기 위해 API 호출 형식을 지정하는 방법을 알아봅니다.
title: 대상 게시 요청 만들기
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# 대상 게시 요청 만들기

>[!IMPORTANT]
>
>다른 Experience Platform 고객이 사용할 제품(공개) 대상을 제출하는 경우에만 이 API 엔드포인트를 사용해야 합니다. 직접 사용할 비공개 대상을 만드는 경우 게시 API를 사용하여 대상을 공식적으로 제출할 필요가 없습니다.

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

대상을 구성하고 테스트한 후 검토 및 게시를 위해 Adobe에 제출할 수 있습니다. 읽기 [Destination SDK에서 작성된 대상을 검토하도록 제출](../guides/submit-destination.md) 기타 모든 단계에 대해 대상 제출 프로세스의 일부로 수행해야 합니다.

다음과 같은 경우 게시 대상 API 엔드포인트를 사용하여 게시 요청을 제출합니다.

* Destination SDK 파트너인 경우 모든 Experience Platform 고객이 사용할 수 있도록 모든 Experience Platform 조직에서 생산화된 대상을 사용할 수 있도록 하려고 합니다.
* 다음을 수행합니다. *모든 업데이트* 참조하십시오. 구성 업데이트는 Experience Platform 팀이 승인한 새 게시 요청을 제출한 후에만 대상에 반영됩니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 게시 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 게시할 대상 구성 제출 {#create}

에 POST 요청을 만들어 게시할 대상 구성을 제출할 수 있습니다 `/authoring/destinations/publish` 엔드포인트.

**API 형식**

```http
POST /authoring/destinations/publish
```

+++요청

다음 요청은 페이로드에 제공된 매개 변수로 구성된 조직에서 게시할 대상을 제출합니다. 아래 페이로드에는 `/authoring/destinations/publish` 엔드포인트.

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
| `destinationId` | 문자열 | 게시를 위해 제출하는 대상 구성의 대상 ID입니다. 를 사용하여 대상 구성의 대상 ID를 가져옵니다 [대상 구성 검색](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API 호출. |
| `destinationAccess` | 문자열 | 사용 `ALL` 대상이 모든 Experience Platform 고객을 위한 카탈로그에 표시되도록 합니다. |

{style="table-layout:auto"}

+++응답

성공적인 응답은 대상 게시 요청의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

## API 오류 처리

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 대상에 대한 게시 요청을 제출하는 방법을 알 수 있습니다. Adobe Experience Platform 팀이 게시 요청을 검토하고 영업일 기준으로 5일이 경과하면 다시 연락을 드립니다.