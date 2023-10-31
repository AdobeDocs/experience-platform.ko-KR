---
description: 이 페이지는 자격 증명 구성 Adobe Experience Platform Destination SDK을 삭제하는 데 사용되는 API 호출을 예시합니다.
title: 자격 증명 구성 삭제
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# 자격 증명 구성 삭제

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/credentials`

이 페이지는 를 사용하여 자격 증명 구성을 삭제하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다. `/authoring/credentials` API 엔드포인트.

## 사용 시기 `/credentials` API 엔드포인트 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 ***금지*** 을(를) 사용해야 함 `/credentials` API 엔드포인트. 대신 를 통해 대상에 대한 인증 정보를 구성할 수 있습니다. `customerAuthenticationConfigurations` 매개 변수 `/destinations` 엔드포인트.
> 
>읽기 [고객 인증 구성](../functionality/destination-configuration/customer-authentication.md) 를 참조하십시오.

이 API 끝점을 사용하여 Adobe과 대상 플랫폼 및 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 구성을 만들어야 합니다. `/credentials` API 엔드포인트.

글로벌 인증 시스템을 사용하는 경우 다음을 설정해야 합니다. `"authenticationRule":"PLATFORM_AUTHENTICATION"` 다음에서 [대상 게재](../functionality/destination-configuration/destination-delivery.md) 구성, 시기 [새 대상 구성 만들기](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 자격 증명 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 자격 증명 구성 삭제 {#delete}

다음을 삭제할 수 있습니다. [기존](create-credential-configuration.md) 다음을 수행하여 자격 증명 구성 `DELETE` 에 대한 요청 `/authoring/credentials` 이 포함된 끝점 `{INSTANCE_ID}`삭제할 자격 증명 구성 중 입니다.

기존 대상 구성 및 해당 구성 가져오기 `{INSTANCE_ID}`, 다음에 대한 문서 참조: [자격 증명 구성 검색](retrieve-credential-configuration.md).

**API 형식**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `ID` 삭제할 자격 증명 구성 중 입니다. |

다음 요청은 다음에 의해 정의된 자격 증명 구성을 삭제합니다. `{INSTANCE_ID}` 매개 변수.

+++요청

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이제 이 문서를 읽고 다음을 사용하여 자격 증명 구성을 삭제하는 방법을 이해할 수 있습니다. `/authoring/credentials` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.
