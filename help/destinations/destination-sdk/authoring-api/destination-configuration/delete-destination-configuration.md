---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 기존 대상 구성을 삭제하는 데 사용되는 API 호출을 구현합니다.
title: 대상 구성 삭제
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---


# 대상 구성 삭제

이 페이지는 기존 대상 구성을 삭제하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다. `/authoring/destinations` API 엔드포인트.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 구성 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상 구성 삭제 {#delete}

다음을 삭제할 수 있습니다. [기존](create-destination-configuration.md) 다음을 수행하여 대상 서버 구성: `DELETE` 에 대한 요청 `/authoring/destinations` 이 포함된 끝점 `{INSTANCE_ID}`삭제할 대상 구성의 일부입니다.

>[!TIP]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destinations`

기존 대상 구성 및 해당 구성 가져오기 `{INSTANCE_ID}`, 다음에 대한 문서 참조: [대상 구성 검색](retrieve-destination-configuration.md).

**API 형식**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `ID` 삭제할 대상 구성의 일부입니다. |

+++요청

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++응답

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.


## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이 문서를 읽고 나면 이제 Destination SDK을 통해 기존 대상 구성을 삭제하는 방법을 알 수 있습니다 `/authoring/destinations` API 엔드포인트.

이 끝점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 구성 만들기](create-destination-configuration.md)
* [대상 구성 검색](retrieve-destination-configuration.md)
* [대상 구성 업데이트](update-destination-configuration.md)

