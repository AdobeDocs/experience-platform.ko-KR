---
title: Reactor API에서 개인 확장 패키지 공유
description: Reactor API에서 다른 비즈니스가 비공개 확장 패키지를 공유하도록 승인하는 방법에 대해 알아봅니다.
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 2%

---


# 비공개 확장 패키지 공유

>[!NOTE]
>
>확장 패키지 소유자 조직에서 `develop_extensions` 권한이 있는 사용자는 해당 확장 패키지에 대한 확장 패키지 사용 승인을 만들고, 나열하고, 삭제할 수 있습니다. `manage_properties` 권한을 가진 승인된 조직의 사용자는 해당 조직에 대한 확장 패키지 사용 권한을 나열하고 해당 확장 패키지를 사용하려는 경우 해당 상태를 `accepted`(으)로, 사용하지 않으려는 경우 `rejected`(으)로 업데이트할 수 있습니다.

확장 패키지의 소유자는 Reactor API를 통해 다른 회사가 자신의 개인 버전을 활용할 수 있는 권한을 부여할 수 있습니다. 하나의 확장 패키지에 대한 사용 라이선스는 승인된 각 비즈니스에 부여되며, 이 인증은 패키지의 현재 및 향후 모든 개인 버전에 적합합니다.

이 안내서에서는 확장 패키지 사용 승인을 구성하는 방법에 대한 높은 수준의 개요를 제공합니다. 권한 부여 구조의 JSON 예를 포함하여 Reactor API에서 권한을 관리하는 방법에 대한 자세한 지침은 [확장 패키지 사용 권한 부여 끝점 안내서](../endpoints/extension-package-usage-authorizations.md)를 참조하세요.

## 권한 부여 만들기 {#create-authorization}

새 인증을 만들려면 `develop_extensions` 권한이 있어야 합니다. 다음 예제에서는 권한을 부여하려는 회사의 `authorized_org_id`을(를) 사용하여 확장 패키지에 대한 확장 패키지 사용 권한을 만드는 방법을 보여 줍니다.

**API 형식**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 매개변수 | 설명 |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | 인증을 만들려는 확장 패키지의 `ID`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 지정된 회사에 대해 새 확장 패키지 인증을 만듭니다.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| 속성 | 설명 |
| --- | --- |
| `attributes.authorized_org_id` | 권한을 부여할 조직의 `ID`입니다. |

{style="table-layout:auto"}

인증의 초기 상태가 `pending_approval` 단계에 있습니다. 확장 패키지를 사용하기 전에 회사에서 승인을 받아야 합니다. 회사 사용자는 권한 부여가 승인 보류 중인 동안 비공개 확장 패키지를 검색할 수 있지만 설치할 수 없고 확장 카탈로그에서 찾을 수 없습니다.

## 승인 {#approve-authorization}

인증을 승인하려면 `manage_properties` 권한이 있어야 합니다. 승인된 회사는 인증의 `ID`을(를) 포함한 확장 패키지 사용 권한 부여에 PATCH 요청을 보내고 상태를 `approved`(으)로 설정해야 합니다.

**API 형식**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | 승인할 권한 부여 `ID`입니다. |

{style="table-layout:auto"}

**요청**

다음 PATCH 요청은 인증의 `state`을(를) `approved`(으)로 설정합니다.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
	          "state": "approved"
	        },
	        "id": ":extension_package_usage_authorization_id",
	        "type": "extension_package_usage_authorizations"
        }
      }
```

이제 권한 부여가 승인되면 권한 부여된 회사로서 속성에 확장 패키지를 설치할 수 있습니다.

>[!NOTE]
>
>승인이 거부되면 승인된 회사는 확장 패키지를 사용할 수 없습니다.

## 권한 부여 삭제 {#delete-authorization}

확장 패키지의 소유자는 확장 패키지 사용 권한을 삭제하여 언제든지 권한을 취소할 수 있습니다. 이렇게 하면 승인된 회사가 카탈로그에서 확장 패키지의 개인 버전을 보고 해당 속성에 설치하지 못합니다. 그러나 이미 설치된 비공개 버전은 삭제 후에도 예상대로 계속 작동합니다.

**API 형식**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | 삭제할 권한 부여 `ID`입니다. |

{style="table-layout:auto"}

**요청**

다음 DELETE 요청은 회사에 대한 인증 권한을 제거합니다.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
