---
keywords: Experience Platform, 보안, ip 액세스, 유효성 검사, API 안내서, 쿼리 서비스, IP 확인
title: IP 유효성 검사 끝점
description: IP 유효성 검사 API 끝점을 사용하여 쿼리 서비스의 샌드박스에 대한 IP 액세스의 유효성을 검사하는 방법을 알아봅니다.
role: Developer
source-git-commit: ad1b6d8449a2a3ca9c8422e70769d12e33d8e255
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# IP 유효성 검사 끝점

IP 유효성 검사 API 끝점을 사용하여 지정된 IP 주소가 쿼리 서비스의 지정된 샌드박스에 액세스할 수 있는지 확인합니다. 이 검사는 액세스 제한이 적용되는지 또는 IP 주소가 샌드박스 내의 데이터에 액세스할 수 있는지 확인합니다.

## 샌드박스 액세스에 대한 IP 유효성 검사 {#validate-ip-for-sandbox-access}

IP 유효성 검사 끝점을 사용하여 특정 IP 주소가 지정된 샌드박스의 데이터에 액세스할 수 있는지 확인합니다. 샌드박스에 대한 IP 제한이 구성되지 않은 경우 기본적으로 모든 IP 주소가 허용됩니다. 기존 IP 또는 CIDR 제한이 있는 경우 이 API는 지정된 IP 주소가 구성된 범위와 일치하는지 확인합니다.

>[!NOTE]
>
>**사용자 토큰** 또는 **서비스 토큰**&#x200B;을 사용하여 이 끝점에 액세스할 수 있습니다. 구체적인 역할 요구 사항은 필요하지 않습니다.

**API 형식**

```http
POST /security/validate/ip-access
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**응답**

성공적인 응답은 IP가 허용되는지 여부를 나타내는 부울과 함께 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>응답의 `isAllowed` 필드는 제공된 IP가 샌드박스에 액세스할 수 있는 경우 `true`을(를) 반환하고 그렇지 않은 경우 `false`을(를) 반환합니다. 이 API는 동적으로 액세스를 검증하고 샌드박스 환경에 대한 보안 규정 준수를 보장합니다.

```json
{
"isAllowed": true
}
```
