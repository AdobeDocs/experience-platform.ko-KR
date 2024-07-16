---
description: 이 페이지에서는 Adobe Experience Platform Destination SDK을 통해 기존 대상 서버 구성을 삭제하는 데 사용되는 API 호출을 구현합니다.
title: 대상 서버 구성 삭제
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# 대상 서버 구성 삭제

이 페이지에서는 `/authoring/destination-servers` API 끝점을 사용하여 기존 대상 서버 구성을 삭제하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다.

이 끝점을 통해 삭제할 수 있는 기능에 대한 자세한 설명은 다음 문서를 참조하십시오.

* [Destination SDK으로 생성된 대상의 서버 사양](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Destination SDK으로 만든 대상에 대한 템플릿 사양](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [메시지 포맷](../../../destination-sdk/functionality/destination-server/message-format.md)
* [파일 서식 구성](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 서버 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 대상 서버 구성 삭제 {#delete}

삭제하려는 대상 서버 구성의 `{INSTANCE_ID}`을(를) 사용하여 `/authoring/destination-servers` 끝점에 대한 `DELETE` 요청을 수행하여 [기존](create-destination-server.md) 대상 서버 구성을 삭제할 수 있습니다.

>[!TIP]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

기존 대상 서버 구성 및 해당 `{INSTANCE_ID}`을(를) 가져오려면 [대상 서버 구성 검색](retrieve-destination-server.md)에 대한 문서를 참조하십시오.

**API 형식**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 삭제할 대상 서버 구성의 `ID`입니다. |

+++요청

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++응답

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이제 이 문서를 읽고 Destination SDK `/authoring/destination-servers` API 끝점을 통해 기존 대상 서버를 삭제하는 방법을 알 수 있습니다.

이 끝점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 서버 구성 만들기](create-destination-server.md)
* [대상 서버 구성 검색](retrieve-destination-server.md)
* [대상 서버 구성 업데이트](update-destination-server.md)
