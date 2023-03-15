---
keywords: Experience Platform;홈;인기 항목;ID;클러스터 내역
solution: Experience Platform
title: ID의 클러스터 내역 가져오기
description: ID는 다양한 장치 그래프 실행 과정에서 클러스터를 이동할 수 있습니다. ID 서비스는 시간 경과에 따라 주어진 ID의 클러스터 연결을 볼 수 있도록 합니다.
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---

# ID의 클러스터 내역 가져오기

ID는 다양한 장치 그래프 실행 과정에서 클러스터를 이동할 수 있습니다. [!DNL Identity Service] 시간이 지남에 따라 주어진 id의 클러스터 연결을 확인할 수 있습니다.

선택 사항 사용 `graph-type` 클러스터를 가져올 출력 유형을 나타내는 매개 변수입니다. 옵션은 다음과 같습니다.

- `None` - ID 결합을 수행하지 않습니다.
- `Private Graph` - 개인 ID 그래프를 기반으로 ID 결합을 수행합니다. 없는 경우 `graph-type` 이(가) 제공되면 기본값입니다.

## 단일 ID의 클러스터 내역 가져오기

**API 형식**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**요청**

옵션 1: ID를 네임스페이스(`nsId`, ID별) 및 ID 값(`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 2: ID를 네임스페이스(`ns`, 이름별) 및 ID 값(`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 3: ID를 XID(`xid`). ID의 XID를 얻는 방법에 대한 자세한 내용은 이 문서의 다음 내용 섹션을 참조하십시오 [id에 대한 XID를 가져오는 중](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## 여러 ID의 클러스터 내역 가져오기

사용 `POST` 메서드와 동일한 일괄 처리 `GET` 위에서 설명한 방법으로 여러 id의 클러스터 기록을 반환합니다.

>[!NOTE]
>
>요청은 최대 1000개의 ID를 초과하지 않아야 합니다. ID가 1000개를 초과하는 요청은 400개 상태 코드를 생성합니다.

**API 형식**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**요청 본문**

옵션 1: 클러스터 멤버를 검색할 XID 목록을 제공합니다.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

옵션 2: ID 목록을 복합 ID로 제공합니다. 각 ID는 네임스페이스 코드로 ID 값과 네임스페이스를 지정합니다.

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

**스텁 요청**

사용 `x-uis-cst-ctx: stub` 헤더가 스터브된 응답을 반환합니다. 이는 서비스가 완료되는 동안 조기 통합 개발 진행을 용이하게 하기 위한 임시 솔루션입니다. 더 이상 필요하지 않으면 더 이상 사용되지 않습니다.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>요청의 XID가 동일한 클러스터에 속하는지 또는 하나 이상에 클러스터가 전혀 연결되어 있는지에 관계없이 응답에는 요청에 제공된 각 XID에 대해 항상 하나의 항목이 있습니다.

## 다음 단계

다음 튜토리얼을 진행하십시오. [id 매핑 나열](./list-identity-mappings.md)
