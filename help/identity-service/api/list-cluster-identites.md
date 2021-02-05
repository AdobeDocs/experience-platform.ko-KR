---
keywords: Experience Platform;홈;인기 항목;목록 ID;목록 클러스터
solution: Experience Platform
title: 클러스터의 모든 ID 나열
topic: API guide
description: 네임스페이스와 관계없이 ID 그래프에 관련된 ID는 해당 ID 그래프에서 동일한 "클러스터"의 일부로 간주됩니다. 아래 옵션은 모든 클러스터 구성원에 액세스할 수 있는 수단을 제공합니다.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# 클러스터의 모든 ID 나열

네임스페이스와 관계없이 ID 그래프에 관련된 ID는 해당 ID 그래프에서 동일한 &quot;클러스터&quot;의 일부로 간주됩니다. 아래 옵션은 모든 클러스터 구성원에 액세스할 수 있는 수단을 제공합니다.

## 단일 ID에 대해 연결된 ID 받기

단일 ID에 대해 모든 클러스터 멤버를 검색합니다.

선택적 `graph-type` 매개 변수를 사용하여 클러스터를 가져올 ID 그래프를 표시할 수 있습니다. 옵션은 다음과 같습니다.

- 없음 - ID 스티칭을 수행하지 않습니다.
- 비공개 그래프 - 개인 ID 그래프를 기반으로 ID 스티칭을 수행합니다. `graph-type`을(를) 제공하지 않으면 기본값이 됩니다.

**API 형식**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**요청**

옵션 1:ID를 네임스페이스(`nsId`, ID별) 및 ID 값(`id`)으로 제공합니다.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 2:ID를 네임스페이스(`ns`, 이름별) 및 ID 값(`id`)으로 제공합니다.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

옵션 3:ID를 XID(`xid`)로 제공합니다. ID의 XID를 얻는 방법에 대한 자세한 내용은 [ID](./list-native-id.md)에 대한 XID 가져오기를 포함하는 이 문서의 섹션을 참조하십시오.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## 여러 ID에 대해 연결된 ID 받기

`POST`을(를) 위에서 설명한 `GET` 메서드와 동일한 일괄 처리로 사용하여 여러 ID 클러스터의 ID를 반환합니다.

>[!NOTE]
>
>요청에는 최대 1000ID를 초과할 수 없습니다. ID가 1000개를 초과하는 요청은 400개의 상태 코드를 생성합니다.

**API 형식**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**요청**

다음 요청에서는 클러스터 구성원을 검색할 XID 목록을 제공하는 방법을 보여 줍니다.

**부본 요청**

`x-uis-cst-ctx: stub` 헤더를 사용하면 studed 응답이 반환됩니다. 서비스가 완료되는 동안 초기 통합 개발 진행에 도움이 되는 임시 솔루션입니다. 더 이상 필요하지 않은 경우 사용되지 않습니다.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**XID를 사용하여 호출**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**UID를 사용하여 호출**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**&#39;studed&#39; 응답**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**전체 응답**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>요청의 XID가 동일한 클러스터에 속해 있는지 또는 하나 이상의 XID가 연결되어 있는지 여부에 관계없이 응답에는 항상 요청에 제공된 각 XID에 대한 하나의 항목이 있습니다.

## 다음 단계

다음 튜토리얼로 진행하여 [ID](./list-cluster-history.md)의 클러스터 내역 나열