---
keywords: Experience Platform, 보안, ip 액세스, QS-Auth, API 안내서, 쿼리 서비스, IP 범위
title: IP 액세스 끝점
description: IP 액세스 API 끝점을 사용하여 쿼리 서비스의 샌드박스 액세스에 대한 IP 범위를 관리하는 방법을 알아봅니다.
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 3%

---

# IP 액세스 끝점

>[!AVAILABILITY]
>
>이 기능은 Data Distiller 추가 기능을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

지정된 Query Service 샌드박스 내에서 데이터 액세스를 보호하려면 IP 액세스 끝점을 사용하여 허용된 IP 범위를 관리합니다. 이 API를 사용하여 조직의 ID와 연결된 IP 범위를 가져오거나 구성하거나 삭제할 수 있습니다.

IP 액세스 API를 사용하여 다음 작업을 수행할 수 있습니다.

- **모든 IP 범위 가져오기**
- **새 IP 범위 설정**
- **기존 IP 범위 삭제**

이 문서에서는 `/security/ip-access` 끝점에서 만들고 받을 수 있는 요청 및 응답을 다룹니다.

>[!NOTE]
>
>이 API를 호출하려면 사용자 토큰이 있어야 합니다. 각 헤더에 필요한 값을 가져오는 방법은 [시작 안내서](./getting-started.md)를 참조하십시오.

## 모든 IP 범위 가져오기 {#fetch-all-ip-ranges}

샌드박스에 대해 구성된 모든 IP 범위 목록을 검색합니다. 설정된 IP 범위가 없는 경우 기본적으로 모든 IP가 허용되며, 응답이 `allowedIpRanges`에 빈 목록을 반환합니다.

**API 형식**

```http
GET /security/ip-access
```

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 샌드박스에서 허용되는 IP 범위 목록과 함께 HTTP 상태 200을 반환합니다.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

다음 표에서는 응답 스키마 속성에 대한 설명과 그 예를 제공합니다.

| 속성 | 설명 | 예 |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | 샌드박스에 대한 조직 ID입니다. | `{ORG_ID}` |
| `sandboxName` | IP 제한이 적용되는 샌드박스의 이름. | `prod` |
| `channel` | IP 제한에 대한 액세스 모드입니다. 현재 허용되는 값은 `data_distiller`뿐입니다. 이 값은 IP 제한이 PSQL 또는 JDBC 연결에 적용됨을 나타냅니다. | `data_distiller` |
| `allowedIpRanges` | CIDR 또는 고정 IP 형식의 허용된 IP 목록입니다. 각 항목에는 선택적 설명이 포함될 수 있습니다. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>`allowedIpRanges` 필드에는 두 가지 유형의 IP 사양이 포함될 수 있습니다. <br><ul><li>**CIDR**: IP 범위를 정의하는 표준 CIDR 표기법(예: `"136.23.110.0/23"`).</li><li>**고정 IP**: 개별 액세스 권한에 대한 단일 IP(예: `"101.10.1.1"`).</li></ul>

## 새 IP 범위 설정

샌드박스에 대한 새 목록을 설정하여 기존 IP 범위를 덮어씁니다. 이 작업을 수행하려면 변경되지 않은 IP 범위를 포함한 전체 IP 범위 목록이 필요합니다.

**API 형식**

```http
PUT /security/ip-access
```

**요청**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**응답**

성공적인 응답은 새로 구성된 IP 범위에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## IP 범위 삭제 {#delete-ip-ranges}

샌드박스에 대해 구성된 모든 IP 범위를 제거합니다. 이 작업은 IP 범위를 삭제하고 삭제된 IP 목록을 반환합니다.

>[!NOTE]
>
>삭제 작업은 조직(`imsOrg`) ID에 적용되며 샌드박스에 대해 구성된 모든 IP 범위에 영향을 줍니다.

**API 형식**

```http
DELETE /security/ip-access
```

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 삭제된 IP 범위의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
