---
keywords: Experience Platform;홈;인기 항목;ID;클러스터 기록
solution: Experience Platform
title: ID의 클러스터 내역 가져오기
topic-legacy: API guide
description: ID는 다양한 장치 그래프 실행 과정에서 클러스터를 이동할 수 있습니다. Identity Service는 시간에 따라 지정된 ID의 클러스터 연결을 표시합니다.
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---

# ID의 클러스터 내역 가져오기

ID는 다양한 장치 그래프 실행 과정에서 클러스터를 이동할 수 있습니다. [!DNL Identity Service] 은 시간에 따른 지정된 ID의 클러스터 연결을 표시합니다.

선택적 `graph-type` 매개 변수를 사용하여 클러스터를 가져올 출력 유형을 지정합니다. 옵션은 다음과 같습니다.

- `None` - ID 스티칭을 수행하지 않습니다.
- `Private Graph` - 개인 ID 그래프를 기반으로 ID 스티칭을 수행합니다. `graph-type`을(를) 제공하지 않으면 기본값이 됩니다.

## 단일 ID의 클러스터 내역 가져오기

**API 형식**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**요청**

옵션 1:ID를 네임스페이스(`nsId`, ID별) 및 ID 값(`id`)으로 제공합니다.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 2:ID를 네임스페이스(`ns`, 이름별) 및 ID 값(`id`)으로 제공합니다.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 3:ID를 XID(`xid`)로 제공합니다. ID의 XID를 얻는 방법에 대한 자세한 내용은 [ID](./list-native-id.md)에 대한 XID 가져오기를 포함하는 이 문서의 섹션을 참조하십시오.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## 여러 ID의 클러스터 내역 가져오기

`POST` 메서드를 위에서 설명한 `GET` 메서드와 동일한 일괄 처리로 사용하여 여러 ID의 클러스터 내역을 반환합니다.

>[!NOTE]
>
>요청에는 최대 1000ID를 초과할 수 없습니다. ID가 1000개를 초과하는 요청은 400개의 상태 코드를 생성합니다.

**API 형식**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**요청 본문**

옵션 1:클러스터 구성원을 검색할 XID 목록을 제공합니다.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

옵션 2:ID 목록을 조합 ID로 제공합니다. 여기서 각 ID 값과 네임스페이스의 이름은 네임스페이스 코드로 지정됩니다.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**요청**

**부본 요청**

`x-uis-cst-ctx: stub` 헤더를 사용하면 studed 응답이 반환됩니다. 서비스가 완료되는 동안 초기 통합 개발 진행에 도움이 되는 임시 솔루션입니다. 더 이상 필요하지 않은 경우 사용되지 않습니다.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**XID 사용**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**UID 사용**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "compositeXids": [{
                "nsid": 411,
                "id": "WRbM7AAAAJ_PBZHl"
            },
            {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            }
        ],
        "graph-type": "Private Graph"
      }' | json_pp
```

**응답**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>요청의 XID가 동일한 클러스터에 속해 있는지 또는 하나 이상의 XID가 연결되어 있는지 여부에 관계없이 응답에는 항상 요청에 제공된 각 XID에 대한 하나의 항목이 있습니다.

## 다음 단계

[목록 ID 매핑](./list-identity-mappings.md)의 다음 자습서로 진행합니다.
