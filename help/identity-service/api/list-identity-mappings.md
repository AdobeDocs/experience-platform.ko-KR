---
keywords: Experience Platform;홈;인기 항목;ID;ID
solution: Experience Platform
title: 목록 ID 매핑
description: 매핑은 지정된 네임스페이스에 대한 클러스터의 모든 ID의 컬렉션입니다.
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# 목록 ID 매핑

매핑은 지정된 네임스페이스에 대한 클러스터의 모든 ID의 컬렉션입니다.

## 단일 ID에 대한 ID 매핑 가져오기

ID가 주어지면 요청에서 ID로 표현되는 것과 동일한 네임스페이스에서 모든 관련 ID를 검색합니다.

**API 형식**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**요청**

옵션 1: ID를 네임스페이스(`nsId`, ID별) 및 ID 값(`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 2: ID를 네임스페이스(`ns`, 이름별) 및 ID 값(`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 3: ID를 XID(`xid`). ID의 XID를 얻는 방법에 대한 자세한 내용은 이 문서의 다음 내용 섹션을 참조하십시오 [id에 대한 XID를 가져오는 중](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 여러 ID에 대한 ID 매핑 가져오기

사용 `POST` 메서드와 동일한 일괄 처리 `GET` 위에서 설명한 여러 id에 대한 매핑을 검색하는 방법입니다.

>[!NOTE]
>
>요청은 최대 1000개의 ID를 초과하지 않아야 합니다. ID가 1000개를 초과하는 요청은 400개 상태 코드를 생성합니다.

**API 형식**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**요청 본문**

옵션 1: 매핑을 검색할 XID 목록을 제공합니다.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

옵션 2: ID 목록을 복합 ID로 제공합니다. 여기서 각 ID는 네임스페이스 ID별로 ID 값 및 네임스페이스를 지정합니다. 이 예에서는 기본값을 덮어쓰면서 이 메서드를 사용하는 방법을 보여 줍니다 `graph-type` 비공개 그래프의

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**요청**

**XID 사용**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**UID 사용**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
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
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

입력한 내용과 관련된 ID가 없는 경우 `HTTP 204` 응답 코드가 내용 없이 반환됩니다.

**응답**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: 입력 ID가 이 ID와 마지막으로 연결된 시점의 타임스탬프입니다.
- `regions`: 를 제공합니다. `regionId` 및 `lastAssociationTime` 신원 확인

## 다음 단계

다음 튜토리얼을 진행하십시오. [사용 가능한 네임스페이스 나열](./list-namespaces.md).
