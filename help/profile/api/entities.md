---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 엔티티 - 실시간 고객 프로필 API
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 1%

---


# 엔터티 끝점(프로필 액세스)

Adobe Experience Platform을 사용하면 RESTful API 또는 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile] 데이터에 액세스할 수 있습니다. 이 안내서에서는 API를 사용하여 일반적으로 &quot;프로필&quot;이라고 하는 엔터티에 액세스하는 방법을 설명합니다. UI를 사용하여 프로파일에 액세스하는 방법에 대한 자세한 내용은 [!DNL Platform] 프로필 사용 안내서를 참조하십시오 [](../ui/user-guide.md).

## 시작하기

이 안내서에 사용되는 API 끝점은 [[!DNL 실시간 고객 프로필 API]의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). 계속하기 전에 [시작하기 가이드](getting-started.md) 에서 관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오 [!DNL Experience Platform] .

## ID로 프로필 데이터 액세스

종단점에 GET 요청을 하고 일련의 쿼리 매개 변수로 엔티티의 ID를 제공하여 엔터티에 액세스할 수 [!DNL Profile] `/access/entities` 있습니다. 이 ID는 ID 값(`entityId`)과 ID 네임스페이스(`entityIdNS`)로 구성됩니다.

요청 경로에 제공된 쿼리 매개 변수는 액세스할 데이터를 지정합니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다. 부칙의 [쿼리 매개 변수](#query-parameters) 섹션에 유효한 매개 변수의 전체 목록이 제공됩니다.

**API 형식**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**요청**

다음 요청은 ID를 사용하여 고객의 이메일 및 이름을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

>[!NOTE]
>
>관련 그래프가 50개 이상의 ID를 연결하는 경우 이 서비스는 HTTP 상태 422와 &quot;관련 ID가 너무 많습니다&quot;라는 메시지를 반환합니다. 이 오류가 표시되면 검색 범위를 좁히기 위해 쿼리 매개 변수를 더 추가하는 것이 좋습니다.

## ID 목록별 프로필 데이터 액세스

종단점에 POST 요청을 만들고 페이로드의 ID를 제공하여 ID로 여러 프로필 엔터티에 액세스할 수 `/access/entities` 있습니다. 이러한 ID는 ID 값(`entityId`)과 ID 네임스페이스(`entityIdNS`)로 구성됩니다.

**API 형식**

```http
POST /access/entities
```

**요청**

다음 요청은 여러 고객의 이름과 이메일 주소를 ID 목록으로 검색합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| 속성 | 설명 |
|---|---|
| `schema.name` | ***(필수)*** 엔터티가 속한 XDM 스키마의 이름입니다. |
| `fields` | 반환할 XDM 필드(문자열 배열)입니다. 기본적으로 모든 필드가 반환됩니다. |
| `identities` | ***(필수)*** 액세스하려는 개체의 ID 목록이 포함된 배열입니다. |
| `identities.entityId` | 액세스하려는 엔터티의 ID입니다. |
| `identities.entityIdNS.code` | 액세스하려는 엔티티 ID의 네임스페이스입니다. |
| `timeFilter.startTime` | 포함된 시간 범위 필터의 시작 시간입니다. 밀리 초 단위여야 합니다. 기본값이 지정되지 않은 경우 사용 가능한 시간의 시작입니다. |
| `timeFilter.endTime` | 시간 범위 필터의 종료 시간. 제외됨. 밀리 초 단위여야 합니다. 기본값이 지정되지 않은 경우 사용 가능한 시간의 끝입니다. |
| `limit` | 반환할 레코드 수입니다. 반환된 경험 이벤트 수에만 적용됩니다. 기본값:1,000명. |
| `orderby` | 기본값이 있는 것처럼 작성된 타임스탬프별 검색된 경험 이벤트 `(+/-)timestamp` 정렬 `+timestamp`순서 |
| `withCA` | 조회를 위해 계산된 속성을 활성화하는 기능 플래그. 기본값:false. |

**응답**&#x200B;성공적인 응답은 요청 본문에 지정된 개체의 요청된 필드를 반환합니다.

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## ID로 프로필에 대한 시간 시리즈 이벤트에 액세스

종단점에 GET 요청을 하여 연결된 프로필 엔터티의 ID로 시간 시리즈 이벤트에 액세스할 수 `/access/entities` 있습니다. 이 ID는 ID 값(`entityId`)과 ID 네임스페이스(`entityIdNS`)로 구성됩니다.

요청 경로에 제공된 쿼리 매개 변수는 액세스할 데이터를 지정합니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다. 부칙의 [쿼리 매개 변수](#query-parameters) 섹션에 유효한 매개 변수의 전체 목록이 제공됩니다.

**API 형식**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**요청**

다음 요청은 ID로 프로필 엔티티를 찾고 엔티티와 연관된 모든 시간 시리즈 이벤트 `endUserIDs`, 속성 `web`및 `channel` 에 대한 값을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청 쿼리 매개 변수에 지정된 시간 시리즈 이벤트 및 관련 필드의 페이지 지정 목록을 반환합니다.

>[!NOTE]
>
>요청이 하나의 한도를 지정했으므로`limit=1`, 아래 응답의 `count` 는 1이며 하나의 엔티티만 반환됩니다.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### 다음 결과 페이지에 액세스

시계열 이벤트를 검색할 때 결과는 페이지로 지정됩니다. 이후 결과 페이지가 있는 경우 속성에 ID가 `_page.next` 포함됩니다. 또한 이 `_links.next.href` 속성은 다음 페이지를 검색할 수 있는 요청 URI를 제공합니다. 결과를 검색하려면 끝점에 대해 다른 GET 요청을 `/access/entities` 하지만 제공된 URI의 값 `/entities` 으로 바꾸어야 합니다.

>[!NOTE]
>
>요청 경로에서 실수로 반복되지 않도록 `/entities/` 하십시오. 딱 한 번만 나타나야 하는데 `/access/entities?start=...`

**API 형식**

```http
GET /access/{NEXT_URI}
```

| 매개 변수 | 설명 |
|---|---|
| `{NEXT_URI}` | 가져온 URI 값 `_links.next.href`. |

**요청**

다음 요청은 URI를 요청 경로로 사용하여 다음 결과 페이지를 `_links.next.href` 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 결과 페이지를 반환합니다. 이 응답에는 and의 빈 문자열 값으로 표시된 대로 후속 결과 페이지가 `_page.next` 없습니다 `_links.next.href`.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## ID별로 여러 프로필에 대한 시계열 이벤트에 액세스

종단점에 POST 요청을 만들고 페이로드에서 프로필 ID를 제공하여 여러 연결된 프로필에서 시간 시리즈 이벤트에 액세스할 수 `/access/entities` 있습니다. 이러한 ID는 각각 ID 값(`entityId`)과 ID 네임스페이스(`entityIdNS`)로 구성됩니다.

**API 형식**

```http
POST /access/entities
```

**요청**

다음 요청은 프로필 ID 목록과 연관된 시간 시리즈 이벤트의 사용자 ID, 로컬 시간 및 국가 코드를 검색합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| 속성 | 설명 |
|---|---|
| `schema.name` | **(필수)** 검색할 엔티티의 XDM 스키마 |
| `relatedSchema.name` | 이 값 `schema.name` 이 `_xdm.context.experienceevent` 이면 시간 시리즈 이벤트가 관련된 프로필 엔터티의 스키마를 지정해야 합니다. |
| `identities` | **(필수)** 연결된 시계열 이벤트를 검색할 프로필 목록입니다. 배열의 각 항목은 다음 두 가지 방법 중 하나로 설정됩니다.1) XID를 제공하는 ID 값 및 네임스페이스로 구성된 정규화된 ID 사용 또는 2) |
| `fields` | 지정된 필드 세트로 반환된 데이터를 격리합니다. 검색된 데이터에 포함할 스키마 필드를 필터링하려면 이 옵션을 사용합니다. 예:personalEmail,person.name,person.gender |
| `mergePolicyId` | 반환된 데이터를 제어하는 병합 정책을 식별합니다. 서비스 호출에 지정되지 않은 경우 해당 스키마에 대한 조직의 기본값이 사용됩니다. 기본 병합 정책이 구성되지 않은 경우, 기본값은 프로필 병합 및 ID 연결 없음을 나타냅니다. |
| `orderby` | 기본값이 있는 것처럼 작성된 타임스탬프별 검색된 경험 이벤트 `(+/-)timestamp` 정렬 `+timestamp`순서 |
| `timeFilter.startTime` | 시계열 개체를 필터링할 시작 시간(밀리초)을 지정합니다. |
| `timeFilter.endTime` | 시계열 개체를 필터링할 종료 시간(밀리초)을 지정합니다. |
| `limit` | 반환할 최대 개체 수를 지정하는 숫자 값. 기본값:1000년 |
| `withCA` | 조회를 위해 계산된 속성을 활성화하는 기능 플래그. 기본값:false |

**응답**

성공적인 응답은 요청에 지정된 여러 프로파일과 연관된 페이지 지정 시계열 이벤트 목록을 반환합니다.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

이 예제 응답에서 첫 번째 나열된 프로필(&quot;GouAW-yD9aoRCPhRYROJ-TextAFW&quot;)은 에 대한 값을 제공합니다. 즉, 이 프로필에 대한 추가 결과 페이지가 있음을 의미합니다. `_links.next.payload` 추가 결과에 액세스하는 방법에 대한 자세한 내용은 추가 결과 [](#access-additional-results) 액세스에 대한 다음 섹션을 참조하십시오.

### 추가 결과 이용 {#access-additional-results}

시계열 이벤트를 검색할 때 반환되는 결과가 많을 수 있으므로 결과를 종종 페이지에 매깁니다. 특정 프로필에 대한 후속 결과 페이지가 있는 경우 해당 프로필에 대한 `_links.next.payload` 값에 페이로드 개체가 포함됩니다.

요청 본문에 이 페이로드를 사용하면 종단점에 대한 추가 POST 요청을 수행하여 해당 프로필에 대한 후속 시계열 데이터를 검색할 수 있습니다. `access/entities`

## 여러 스키마 엔티티에서 시간 시리즈 이벤트에 액세스

관계 설명자를 통해 연결된 여러 개체에 액세스할 수 있습니다. 다음 예제 API 호출에서는 두 스키마 사이에 관계가 이미 정의되어 있다고 가정합니다. 관계 설명자에 대한 자세한 내용은 [!DNL Schema Registry] API 개발자 가이드 [설명자 끝점 안내서를 참조하십시오](../../xdm/api/descriptors.md).

액세스할 데이터를 지정하기 위해 요청 경로에 쿼리 매개 변수를 포함할 수 있습니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다. 부칙의 [쿼리 매개 변수](#query-parameters) 섹션에 유효한 매개 변수의 전체 목록이 제공됩니다.

**API 형식**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**요청**

다음 요청은 이전에 설정한 관계 설명자를 포함하는 엔터티를 검색하여 여러 스키마에 있는 정보에 액세스합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적인 응답은 여러 엔터티와 연결된 페이지 지정 시계열 이벤트 목록을 반환합니다.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### 다음 결과 페이지에 액세스

시계열 이벤트를 검색할 때 결과는 페이지로 지정됩니다. 이후 결과 페이지가 있는 경우 속성에 ID가 `_page.next` 포함됩니다. 또한 이 `_links.next.href` 속성은 종단점에 대한 추가 GET 요청을 만들어 이후 페이지를 검색하는 요청 URI를 `access/entities` 제공합니다.

## 다음 단계

이 안내서를 따르면 데이터 필드, 프로필 및 시계열 데이터에 성공적으로 액세스했습니다. [!DNL Real-time Customer Profile] 에 저장된 다른 데이터 리소스에 액세스하는 방법 [!DNL Platform]을 알아보려면 [데이터 액세스 개요를 참조하십시오](../../data-access/home.md).

## 부록 {#appendix}

다음 섹션에서는 API를 사용한 데이터 액세스에 대한 보충 정보를 제공합니다. [!DNL Profile]

### 쿼리 매개 변수 {#query-parameters}

다음 매개 변수는 종단점에 대한 GET 요청 경로에 `/access/entities` 사용됩니다. 액세스하려는 프로필 엔티티를 식별하고 응답에서 반환된 데이터를 필터링합니다. 필수 매개 변수에는 레이블이 지정되고 나머지는 선택 사항입니다.

| 매개 변수 | 설명 | 예 |
|---|---|---|
| `schema.name` | **(필수)** 검색할 엔티티의 XDM 스키마 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | &quot;_xdm.context.experienceevent&quot; `schema.name` 인 경우 이 값은 시간 시리즈 이벤트가 관련되는 프로필 엔티티의 스키마를 지정해야 합니다. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(필수)** 엔티티의 ID입니다. 이 매개 변수의 값이 XID가 아닌 경우 ID 네임스페이스 매개 변수도 제공해야 합니다(아래 참조 `entityIdNS` ). | `entityId=janedoe@example.com` |
| `entityIdNS` | XID로 제공되지 `entityId` 않으면 이 필드에서 ID 네임스페이스를 지정해야 합니다. | `entityIdNE=email` |
| `relatedEntityId` | &quot;_xdm.context.experienceevent&quot; `schema.name` 인 경우 이 값은 관련 프로필 엔티티의 ID 네임스페이스를 지정해야 합니다. 이 값은 동일한 규칙을 따릅니다 `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | &quot;_xdm.context.experienceevent&quot; `schema.name` 인 경우 이 값은 에 지정된 엔터티의 ID 네임스페이스를 지정해야 합니다 `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | 응답에서 반환된 데이터를 필터링합니다. 검색된 데이터에 포함할 스키마 필드 값을 지정하려면 이 값을 사용합니다. 여러 필드의 경우 쉼표를 쉼표로 구분하되 공백 없이 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 반환된 데이터를 제어하는 병합 정책을 식별합니다. 호출에 지정되지 않은 경우 해당 스키마에 대한 조직의 기본값이 사용됩니다. 기본 병합 정책이 구성되지 않은 경우, 기본값은 프로필 병합 및 ID 연결 없음을 나타냅니다. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 기본값이 있는 것처럼 작성된 타임스탬프별 검색된 경험 이벤트 `(+/-)timestamp` 정렬 `+timestamp`순서 | `orderby=-timestamp` |
| `startTime` | 시계열 개체를 필터링할 시작 시간(밀리초)을 지정합니다. | `startTime=1539838505` |
| `endTime` | 시계열 개체를 필터링할 종료 시간(밀리초)을 지정합니다. | `endTime=1539838510` |
| `limit` | 반환할 최대 개체 수를 지정하는 숫자 값. 기본값:1000년 | `limit=100` |
| `withCA` | 조회를 위해 계산된 속성을 활성화하는 기능 플래그. 기본값:false | `withCA=true` |