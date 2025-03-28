---
title: API를 사용하여 소스 데이터 흐름에 대한 사용자 액세스를 관리하기 위해 액세스 레이블 적용
description: 흐름 서비스 API를 사용하여 액세스 레이블을 적용하고 소스 데이터 흐름에 대한 사용자 액세스를 관리하는 방법을 알아봅니다.
exl-id: 572d6838-3e4c-4fd5-89fa-32cad6280325
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 3%

---

# API를 사용하여 소스 데이터 흐름에 대한 사용자 액세스를 관리하기 위해 액세스 레이블 적용

Real-Time CDP의 [특성 기반 액세스 제어](../../../access-control/abac/overview.md)에서 제공하는 기능을 사용하여 소스 데이터 흐름에 레이블을 적용할 수 있습니다. 이 기능을 사용하면 조직의 사용자 하위 집합만 특정 소스 데이터 흐름에 액세스할 수 있습니다.

특정 데이터 흐름에 액세스 레이블을 추가하면 해당 레이블이 할당된 역할에 액세스할 수 있는 사용자만 해당 데이터 흐름을 보고 편집할 수 있습니다. 소스 데이터 흐름이 레이블로 표시되지 않으면 조직에 속한 모든 사용자가 볼 수 있습니다. 예를 들어 C12 레이블을 데이터 흐름에 적용하면 C12 레이블이 없는 역할에 할당된 사용자는에서 C12 레이블을 사용하여 데이터 흐름을 보고 편집할 수 없습니다.

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)를 사용하여 소스 데이터 흐름에 액세스 레이블을 적용하는 방법에 대한 자세한 내용은 이 안내서를 참조하십시오.

## 시작하기

액세스 제어 레이블을 사용하기 전에 먼저 속성 기반 액세스 제어 기능을 숙지해야 합니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [속성 기반 액세스 제어 개요](../../../access-control/abac/overview.md)
* [속성 기반 액세스 제어 엔드투엔드 가이드](../../../access-control/abac/end-to-end-guide.md)
* [속성 기반 액세스 제어 API 안내서](../../../access-control/abac/api/overview.md)
* [데이터 사용 레이블 용어](../../../data-governance/labels/reference.md)

## 소스 데이터 흐름에 액세스 레이블 적용

>[!NOTE]
>
>* 플로우 실행에는 레이블을 적용할 수 없습니다. 그러나 흐름 실행은 상위 데이터 흐름에 적용하는 모든 레이블을 상속합니다.
>
>* 데이터 흐름에 대한 보기 액세스 권한이 없는 경우 해당 흐름 실행을 볼 수도 없습니다.

데이터 흐름에 레이블을 추가하려면 `/flows` 끝점에 PATCH 요청을 하고 업데이트할 데이터 흐름의 ID를 제공하십시오.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{FLOW_ID}` | 업데이트할 데이터 흐름의 ID입니다. |

**요청**

>[!TIP]
>
>PATCH 요청을 수행하려면 업데이트할 데이터 흐름의 버전/태그를 `if-match` 헤더 매개 변수로 제공하십시오.

다음 요청은 ID가 `84224def-1e2a-4d95-9ea2-132d697ed2aa`인 데이터 흐름에 C12 레이블을 추가합니다.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| 속성 | 설명 |
| --- | --- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 업데이트할 데이터 흐름의 일부입니다. |
| `value` | 속성을 업데이트할 새 값입니다. |



**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 흐름 ID를 제공하면서 [!DNL Flow Service] API에 대한 GET 요청을 만들어 업데이트를 확인할 수 있습니다.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

데이터 흐름에 액세스 레이블을 성공적으로 구성했으면 해당 레이블에 대한 액세스 권한이 없는 모든 사용자는 더 이상 데이터 흐름을 검색할 수 없습니다. 예를 들어 C12 레이블이 없는 사용자가 ID가 `84224def-1e2a-4d95-9ea2-132d697ed2aa`인 데이터 흐름을 검색하기 위해 GET 요청을 수행하면 다음 응답을 받게 됩니다.

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

마찬가지로 C12 레이블에 대한 액세스 권한이 없는 사용자는 업데이트된 데이터 흐름에 대해 PATCH 또는 DELETE 요청을 수행할 수 없으며 다음 응답을 받게 됩니다.

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## 다음 단계

이제 소스 데이터 흐름에 액세스 레이블을 적용하는 방법을 알 수 있습니다. 이제 조직의 특정 사용자 그룹만 특정 소스 데이터 흐름에 액세스할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

* [UI의 소스 데이터 흐름에 액세스 레이블 적용](../ui/labels.md)
* [액세스 제어 개요](../../../access-control/home.md)
