---
description: 이 페이지에서는 자격 증명 구성 Adobe Experience Platform Destination SDK을 삭제하는 데 사용되는 API 호출을 보여줍니다.
title: 자격 증명 구성 삭제
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# 자격 증명 구성 삭제

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/credentials`

이 페이지는 을 사용하여 자격 증명 구성을 삭제하는 데 사용할 수 있는 API 요청 및 페이로드를 보여줍니다 `/authoring/credentials` API 엔드포인트.

## 를 사용해야 하는 경우 `/credentials` API 엔드포인트 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 ***포함하지 않음*** 를 사용해야 함 `/credentials` API 엔드포인트. 대신 를 통해 대상에 대한 인증 정보를 구성할 수 있습니다 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 엔드포인트.
> 
>읽기 [고객 인증 구성](../functionality/destination-configuration/customer-authentication.md) 지원되는 인증 유형에 대한 자세한 정보를 제공합니다.

Adobe과 대상 플랫폼 간에 글로벌 인증 시스템이 있고 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 `/credentials` API 엔드포인트.

글로벌 인증 시스템을 사용할 때는 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 에서 [대상 게재](../functionality/destination-configuration/destination-delivery.md) 구성, 설정 [새 대상 구성 만들기](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 자격 증명 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 자격 증명 구성 삭제 {#delete}

삭제할 수 있습니다 [기존](create-credential-configuration.md) 자격 증명 구성 `DELETE` 에 요청 `/authoring/credentials` 엔드포인트 `{INSTANCE_ID}`삭제할 자격 증명 구성

기존 대상 구성 및 해당 구성 가져오기 `{INSTANCE_ID}`에 대한 자세한 내용은 [자격 증명 구성 검색](retrieve-credential-configuration.md).

**API 형식**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `ID` 삭제할 자격 증명 구성의 |

다음 요청은 `{INSTANCE_ID}` 매개 변수.

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

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 `/authoring/credentials` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md) 대상 구성 프로세스에 이 단계가 어떤 영향을 주는지 이해하기 위해 노력합니다.
