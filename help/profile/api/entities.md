---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 엔티티(프로필 액세스) API 끝점
type: Documentation
description: Adobe Experience Platform을 사용하면 RESTful API 또는 사용자 인터페이스를 사용하여 실시간 고객 프로필 데이터에 액세스할 수 있습니다. 이 안내서에서는 프로필 API를 사용하여 "프로필"로 더 일반적으로 알려진 엔티티에 액세스하는 방법을 간략하게 설명합니다.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 3%

---

# 엔티티 끝점(프로필 액세스)

>[!IMPORTANT]
>
>프로필 액세스 API를 사용한 ExperienceEvent 조회는 더 이상 사용되지 않습니다. ExperienceEvents 조회가 필요한 사용 사례에 대해 계산된 속성과 같은 기능을 사용하십시오. 이 변경 사항에 대한 자세한 내용은 Adobe 고객 지원 센터에 문의하십시오.

Adobe Experience Platform을 사용하면 RESTful API 또는 사용자 인터페이스를 사용하여 [!DNL Real-Time Customer Profile] 데이터에 액세스할 수 있습니다. 이 안내서에서는 API를 사용하여 &quot;프로필&quot;로 더 일반적으로 알려진 엔티티에 액세스하는 방법을 간략하게 설명합니다. [!DNL Experience Platform] UI를 사용하여 프로필에 액세스하는 방법에 대한 자세한 내용은 [프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.

## 시작하기

이 가이드에 사용된 API 끝점은 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)의 일부입니다. 계속하기 전에 [시작 안내서](getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 [!DNL Experience Platform] API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 엔티티 검색 {#retrieve-entity}

필요한 쿼리 매개 변수와 함께 `/access/entities` 끝점에 대한 GET 요청을 만들어 프로필 엔터티를 검색할 수 있습니다.

>[!BEGINTABS]

>[!TAB 프로필 엔터티]

**API 형식**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

요청 경로에 제공된 쿼리 매개 변수는 액세스할 데이터를 지정합니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다.

프로필 엔터티에 액세스하려면 **다음 쿼리 매개 변수를 제공해야 합니다**.

- `schema.name`: 엔터티의 XDM 스키마 이름입니다. 이 사용 사례에서는 `schema.name=_xdm.context.profile`입니다.
- `entityId`: 검색하려는 엔터티의 ID입니다.
- `entityIdNS`: 검색하려는 엔터티의 네임스페이스입니다. `entityId`이(가) XID가 **아님**&#x200B;인 경우 이 값을 제공해야 합니다.

부록의 [쿼리 매개 변수](#query-parameters) 섹션에 올바른 매개 변수의 전체 목록이 제공됩니다.

**요청**

다음 요청은 ID를 사용하여 고객의 이메일과 이름을 검색합니다.

+++ ID를 사용하여 엔티티를 검색하기 위한 샘플 요청

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 요청된 엔터티와 함께 HTTP 상태 200을 반환합니다.

+++ 요청된 엔터티가 포함된 샘플 응답

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
                    "id": "johnsmith@example.com",
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

+++

>[!NOTE]
>
>관련 그래프가 50개가 넘는 ID를 연결하는 경우 이 서비스는 HTTP 상태 422와 &quot;관련 ID가 너무 많습니다&quot;라는 메시지를 반환합니다. 이 오류가 표시되면 쿼리 매개 변수를 더 추가하여 검색 범위를 좁히는 것이 좋습니다.

>[!TAB B2B 계정]

**API 형식**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

요청 경로에 제공된 쿼리 매개 변수는 액세스할 데이터를 지정합니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다.

B2B 계정 데이터에 액세스하려면 **다음 쿼리 매개 변수를 제공해야 합니다**.

- `schema.name`: 엔터티의 XDM 스키마 이름입니다. 이 사용 사례에서는 이 값이 `schema.name=_xdm.context.account`입니다.
- `entityId`: 검색하려는 엔터티의 ID입니다.
- `entityIdNS`: 검색하려는 엔터티의 네임스페이스입니다. `entityId`이(가) XID가 **아님**&#x200B;인 경우 이 값을 제공해야 합니다.

부록의 [쿼리 매개 변수](#query-parameters) 섹션에 올바른 매개 변수의 전체 목록이 제공됩니다.

**요청**

+++ B2B 계정 검색에 대한 샘플 요청

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 요청된 엔터티와 함께 HTTP 상태 200을 반환합니다.

+++ 요청된 엔터티가 포함된 샘플 응답

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB B2B 영업 기회]

**API 형식**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

요청 경로에 제공된 쿼리 매개 변수는 액세스할 데이터를 지정합니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다.

B2B 영업 기회 엔터티에 액세스하려면 **다음 쿼리 매개 변수를 제공해야 합니다**.

- `schema.name`: 엔터티의 XDM 스키마 이름입니다. 이 사용 사례에서는 `schema.name=_xdm.context.opportunity`입니다.
- `entityId`: 검색하려는 엔터티의 ID입니다.
- `entityIdNS`: 검색하려는 엔터티의 네임스페이스입니다. `entityId`이(가) XID가 **아님**&#x200B;인 경우 이 값을 제공해야 합니다.

부록의 [쿼리 매개 변수](#query-parameters) 섹션에 올바른 매개 변수의 전체 목록이 제공됩니다.

**요청**

+++ B2B 영업 기회 엔터티 검색에 대한 샘플 요청

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 요청된 엔터티와 함께 HTTP 상태 200을 반환합니다.

+++ 요청된 엔터티가 포함된 샘플 응답

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## 여러 엔티티 검색 {#retrieve-entities}

`/access/entities` 끝점에 대한 POST 요청을 만들고 페이로드에 ID를 제공하여 여러 프로필 엔터티를 검색할 수 있습니다.

>[!BEGINTABS]

>[!TAB 프로필 엔터티]

**API 형식**

```http
POST /access/entities
```

**요청**

다음 요청은 ID 목록으로 여러 고객의 이름과 이메일 주소를 검색합니다.

+++여러 엔티티를 검색하기 위한 샘플 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "orderby": "-timestamp"
      }'
```

| 속성 | 유형 | 설명 |
| -------- |----- | ----------- |
| `schema.name` | 문자열 | **(필수)** 엔터티가 속한 XDM 스키마의 이름입니다. |
| `fields` | 배열 | 문자열 배열로 반환될 XDM 필드. 기본적으로 모든 필드가 반환됩니다. |
| `identities` | 배열 | **(필수)** 액세스하려는 엔터티의 ID 목록이 포함된 배열입니다. |
| `identities.entityId` | 문자열 | 액세스하려는 엔티티의 ID입니다. |
| `identities.entityIdNS.code` | 문자열 | 액세스하려는 엔티티 ID의 네임스페이스입니다. |
| `timeFilter.startTime` | 정수 | 프로필 엔티티를 필터링할 시작 시간(밀리초)을 지정합니다. 기본적으로 이 값은 사용 가능한 시간의 시작으로 설정됩니다. |
| `timeFilter.endTime` | 정수 | 프로필 엔티티를 필터링할 종료 시간(밀리초)을 지정합니다. 기본적으로 이 값은 사용 가능한 시간의 끝으로 설정됩니다. |
| `limit` | 정수 | 반환할 최대 레코드 수입니다. 기본적으로 이 값은 1000으로 설정됩니다. |
| `orderby` | 문자열 | `(+/-)timestamp`(으)로 기록되고 기본값은 `+timestamp`인 타임스탬프별 검색된 경험 이벤트의 정렬 순서입니다. |

+++

**응답**

성공적인 응답은 요청 본문에 지정된 엔티티의 요청된 필드가 있는 HTTP 상태 200을 반환합니다.

+++ 요청된 엔터티가 포함된 샘플 응답

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

+++

>[!TAB B2B 계정]

**API 형식**

```http
POST /access/entities
```

**요청**

다음 요청은 요청된 B2B 계정을 검색합니다.

+++여러 엔티티를 검색하기 위한 샘플 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| 속성 | 유형 | 설명 |
| -------- |----- | ----------- |
| `schema.name` | 문자열 | **(필수)** 엔터티가 속한 XDM 스키마의 이름입니다. |
| `identities` | 배열 | **(필수)** 액세스하려는 엔터티의 ID 목록이 포함된 배열입니다. |
| `identities.entityId` | 문자열 | 액세스하려는 엔티티의 ID입니다. |
| `identities.entityIdNS.code` | 문자열 | 액세스하려는 엔티티 ID의 네임스페이스입니다. |

+++

**응답**

성공적인 응답은 요청된 엔티티와 함께 HTTP 상태 200을 반환합니다.

+++ 요청된 엔터티가 포함된 샘플 응답

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB B2B 영업 기회]

**API 형식**

```http
POST /access/entities
```

**요청**

다음 요청은 요청된 B2B 기회를 검색합니다.

+++ 여러 엔티티를 검색하기 위한 샘플 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| 속성 | 유형 | 설명 |
| -------- |----- | ----------- |
| `schema.name` | 문자열 | **(필수)** 엔터티가 속한 XDM 스키마의 이름입니다. |
| `identities` | 배열 | **(필수)** 액세스하려는 엔터티의 ID 목록이 포함된 배열입니다. |
| `identities.entityId` | 문자열 | 액세스하려는 엔티티의 ID입니다. |
| `identities.entityIdNS.code` | 문자열 | 액세스하려는 엔티티 ID의 네임스페이스입니다. |

+++

**응답**

성공적인 응답은 요청된 엔티티와 함께 HTTP 상태 200을 반환합니다.

+++ 요청된 엔터티가 포함된 샘플 응답

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### 후속 결과 페이지 액세스

시계열 이벤트를 검색할 때 결과에 페이지가 매겨집니다. 후속 결과 페이지가 있으면 `_page.next` 속성에 ID가 포함됩니다. 또한 `_links.next.href` 속성은 다음 페이지를 검색하기 위한 요청 URI를 제공합니다. 결과를 검색하려면 `/access/entities` 끝점에 대해 다른 GET 요청을 만들고 `/entities`을(를) 제공된 URI의 값으로 바꾸십시오.

>[!NOTE]
>
>요청 경로에서 `/entities/`을(를) 실수로 반복하지 마십시오. `/access/entities?start=...`과(와) 같은 한 번만 표시됩니다.

**API 형식**

```http
GET /access/{NEXT_URI}
```

| 매개변수 | 설명 |
|---|---|
| `{NEXT_URI}` | `_links.next.href`에서 가져온 URI 값입니다. |

**요청**

다음 요청은 `_links.next.href` URI를 요청 경로로 사용하여 다음 결과 페이지를 검색합니다.

+++ 결과의 다음 페이지에 액세스하기 위한 샘플 요청

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 다음 결과 페이지를 반환합니다. 이 응답에는 `_page.next` 및 `_links.next.href`의 빈 문자열 값이 나타내는 후속 결과 페이지가 없습니다.

+++ 엔티티의 다음 페이지를 포함하는 샘플 응답

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

+++

## 엔티티 삭제 {#delete-entity}

필요한 쿼리 매개 변수와 함께 `/access/entities` 끝점에 대한 DELETE 요청을 만들어 프로필 저장소에서 엔터티를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

요청 경로에 제공된 쿼리 매개 변수는 액세스할 데이터를 지정합니다. 앰퍼샌드(&amp;)로 구분된 여러 매개 변수를 포함할 수 있습니다.

엔터티를 삭제하려면 **다음 쿼리 매개 변수를 제공해야**&#x200B;합니다.

- `schema.name`: 엔터티의 XDM 스키마 이름입니다. 이 사용 사례에서는 **만**&#x200B;에서 `schema.name=_xdm.context.profile`을(를) 사용할 수 있습니다.
- `entityId`: 검색하려는 엔터티의 ID입니다.
- `entityIdNS`: 검색하려는 엔터티의 네임스페이스입니다. `entityId`이(가) XID가 **아님**&#x200B;인 경우 이 값을 제공해야 합니다.
- `mergePolicyId`: 엔터티의 병합 정책 ID입니다. 병합 정책에는 ID 결합 및 키-값 XDM 개체 병합에 대한 정보가 포함되어 있습니다. 이 값을 제공하지 않으면 기본 병합 정책이 사용됩니다.

**요청**

다음 요청은 지정된 엔티티를 삭제합니다.

+++ 엔티티 삭제에 대한 샘플 요청

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 빈 응답 본문과 함께 HTTP 상태 202를 반환합니다.

## 다음 단계

이 안내서를 따라 [!DNL Real-Time Customer Profile]개의 데이터 필드, 프로필 및 시계열 데이터에 성공적으로 액세스했습니다. [!DNL Experience Platform]에 저장된 다른 데이터 리소스에 액세스하는 방법에 대한 자세한 내용은 [데이터 액세스 개요](../../data-access/home.md)를 참조하세요.

## 부록 {#appendix}

다음 섹션에서는 API를 사용하여 [!DNL Profile] 데이터에 액세스하는 것과 관련된 추가 정보를 제공합니다.

### 쿼리 매개변수 {#query-parameters}

다음 매개 변수는 `/access/entities` 끝점에 대한 GET 요청 경로에 사용됩니다. 액세스하려는 프로필 엔티티를 식별하고 응답에서 반환되는 데이터를 필터링합니다. 필수 매개 변수에는 레이블이 지정되고 나머지는 선택 사항입니다.

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `schema.name` | **(필수)** 엔터티의 XDM 스키마 이름입니다. | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | `schema.name`이(가) `_xdm.context.experienceevent`인 경우 이 값 **must**&#x200B;은(는) 시계열 이벤트와 관련된 프로필 엔터티의 스키마를 지정합니다. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(필수)** 엔터티의 ID입니다. 이 매개 변수의 값이 XID가 아닌 경우 ID 네임스페이스 매개 변수(`entityIdNS`)도 제공해야 합니다. | `entityId=janedoe@example.com` |
| `entityIdNS` | `entityId`이(가) XID로 제공되지 않으면 이 필드 **은(는) ID 네임스페이스를 지정해야 합니다**. | `entityIdNS=email` |
| `relatedEntityId` | `schema.name`이(가) `_xdm.context.experienceevent`인 경우 이 값 **은(는) 관련 프로필 엔터티의 ID를 지정해야 합니다**. 이 값은 `entityId`과(와) 동일한 규칙을 따릅니다. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | `schema.name`이(가) &quot;_xdm.context.experienceevent&quot;인 경우 이 값은 `relatedEntityId`에 지정된 엔터티의 ID 네임스페이스를 지정해야 합니다. | `relatedEntityIdNS=CRMID` |
| `fields` | 응답에서 반환된 데이터를 필터링합니다. 검색할 데이터에 포함할 스키마 필드 값을 지정하려면 이 옵션을 사용합니다. 여러 필드의 경우 공백 없이 쉼표로 값을 구분하십시오. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 반환된 데이터를 제어하는 데 사용할 병합 정책을 식별합니다. 호출에 지정되지 않은 경우 해당 스키마에 대한 조직의 기본값이 사용됩니다. 기본 병합 정책이 구성되지 않은 경우 기본값은 프로필 병합 및 ID 결합 없음을 의미합니다. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 타임스탬프별로 검색된 엔티티의 정렬 순서. `(+/-)timestamp`(으)로 작성되었으며 기본값은 `+timestamp`입니다. | `orderby=-timestamp` |
| `startTime` | 엔티티를 필터링할 시작 시간(밀리초)을 지정합니다. | `startTime=1539838505` |
| `endTime` | 엔티티를 필터링할 종료 시간(밀리초)을 지정합니다. | `endTime=1539838510` |
| `limit` | 반환할 최대 엔티티 수를 지정합니다. 기본적으로 이 값은 1000으로 설정됩니다. | `limit=100` |
| `property` | 속성 값으로 필터링합니다. 이 쿼리 매개변수는 다음 평가자를 지원합니다. =, !=, &lt;, &lt;=, >, >=. 최대 3개의 속성이 지원되는 경험 이벤트에서만 사용할 수 있습니다. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
