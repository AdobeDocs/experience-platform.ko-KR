---
description: 대상 테스트 API를 사용하여 메시지 변환 템플릿을 기반으로 스트리밍 대상에 대한 출력을 확인하는 방법을 알아봅니다.
title: 내보낸 프로필 구조 유효성 검사
exl-id: e64ea89e-6064-4a05-9730-e0f7d7a3e1db
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 1%

---


# 내보낸 프로필 구조 유효성 검사 {#render-template-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

이 페이지에서는 를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/testing/template/render` API 엔드포인트. 대상에 따라 대상의 예상 형식과 일치하는 내보낸 프로필을 렌더링합니다. [메시지 변환 템플릿](../../functionality/destination-server/message-format.md#using-templating). 이 종단점에서 지원하는 기능에 대한 설명은 다음을 참조하십시오 [템플릿 만들기](create-template.md).

## 렌더링 템플릿 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 메시지 변환 템플릿을 기반으로 내보낸 프로필 렌더링 {#render-exported-data}

에 POST 요청을 수행하여 내보낸 프로필을 렌더링할 수 있습니다 `authoring/testing/template/render` 엔드포인트 및 대상 구성의 대상 ID와 을 사용하여 만든 템플릿 제공 [샘플 템플릿 API 엔드포인트](sample-template-api.md).

먼저 간단한 템플릿을 사용하여 변형을 적용하지 않고 원시 프로필을 내보낸 다음 보다 복잡한 템플릿으로 이동하여 프로파일에 변형을 적용할 수 있습니다. 단순 템플릿의 구문은 다음과 같습니다. <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

>[!TIP]
>
>* 여기에서 사용해야 하는 대상 ID는 `instanceId` 대상 구성에 해당하며 `/destinations` 엔드포인트. 을(를) 참조하십시오. [대상 구성 검색](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 자세한 내용


**API 형식**


```http
POST authoring/testing/template/render
```

| 요청 매개 변수 | 설명 |
| -------- | ----------- |
| `destinationId` | 내보낸 프로필을 렌더링하는 대상 구성의 ID입니다. |
| `template` | 내보낸 프로필을 렌더링하는 데 따라 템플릿의 문자 이스케이프 처리된 버전입니다. |
| `profiles` | *선택 사항입니다*. 요청 본문에 프로필을 추가할 수 있습니다. 프로필을 추가하지 않는 경우 Experience Platform이 자동으로 프로필을 생성하여 요청에 추가합니다. <br> 호출 본문에 프로필을 추가하려면 [샘플 프로필 생성 API](sample-profile-generation-api.md). |

{style="table-layout:auto"}

렌더링 템플릿 API 끝점에서 반환되는 응답은 대상 집계 정책에 따라 다릅니다. 대상에 구성 가능한 집계 정책이 있는 경우, 프로필이 집계되는 방법을 결정하는 집계 키도 응답에서 반환됩니다. 자세한 내용 [집계 정책](../../functionality/destination-configuration/aggregation-policy.md) 자세한 내용

| 응답 매개 변수 | 설명 |
| -------- | ----------- |
| `aggregationKey` | 대상 내보내기에서 프로필을 집계하는 정책을 나타냅니다. 이 매개 변수는 선택 사항이며 대상 집계 정책이 `CONFIGURABLE_AGGREGATION`. |
| `profiles` | 요청에 제공된 프로필 또는 요청에 제공된 프로필이 없는 경우 자동으로 생성된 프로필을 표시합니다. |
| `output` | 제공된 메시지 변환 템플릿을 기반으로 프로필 또는 프로필을 이스케이프 처리된 문자열로 렌더링했습니다. |

아래 섹션에서는 위에서 설명한 두 가지 사례에 대한 자세한 요청 및 응답을 제공합니다.

* [요청 본문에 포함된 우수 활동 합계 및 프로필](#best-effort)
* [요청 본문에 포함된 구성 가능한 집계 및 프로필](#configurable-aggregation)

### 최상의 노력 집계를 사용하여 내보낸 프로필을 렌더링하고 요청 본문에 포함된 단일 프로필을 렌더링합니다. {#best-effort}

**요청**

다음 요청은 대상이 기대하는 형식과 일치하는 내보낸 프로필을 렌더링합니다. 이 예에서 대상 ID는 최상의 노력 집계가 있는 대상 구성에 해당하며 샘플 프로필은 요청 본문에 포함되어 있습니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "947c1c46-008d-40b0-92ec-3af86eaf41c1",
    "template": "{#- THIS is an example template for a single profile -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"identities\": [\r\n    {%- for idMapEntry in input.profile.identityMap -%}\r\n    {%- set namespace = idMapEntry.key -%}\r\n        {%- for identity in idMapEntry.value %}\r\n        {\r\n            \"type\": \"{{ namespace }}\",\r\n            \"id\": \"{{ identity.id }}\"\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n        {%- for segment in input.profile.segmentMembership.ups | added %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n        {#- Alternative syntax for filtering segments by status: -#}\r\n        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "gaid": [
                    {
                        "id": "gaid-BLAcJ"
                    }
                ],
                "idfa": [
                    {
                        "id": "idfa-Iv5AG"
                    }
                ],
                "email": [
                    {
                        "id": "email-rbN62"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**응답**

응답은 템플릿 렌더링 결과 또는 발생한 모든 오류를 반환합니다.
성공적인 응답은 내보낸 데이터의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 에서 내보낸 프로필을 찾습니다. `output` 매개 변수(이스케이프 처리된 문자열)입니다.
실패한 응답은 발생한 오류에 대한 설명과 함께 HTTP 상태 400을 반환합니다.

```json
{
    "results": [
        {
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                                "status": "realized"
                            },
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                                "status": "exited"
                            },
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "gaid": [
                            {
                                "id": "gaid-BLAcJ"
                            }
                        ],
                        "idfa": [
                            {
                                "id": "idfa-Iv5AG"
                            }
                        ],
                        "email": [
                            {
                                "id": "email-rbN62"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"identities\": [\r\n        {\r\n            \"type\": \"gaid\",\r\n            \"id\": \"gaid-BLAcJ\"\r\n        },\r\n        {\r\n            \"type\": \"idfa\",\r\n            \"id\": \"idfa-Iv5AG\"\r\n        },\r\n        {\r\n            \"type\": \"email\",\r\n            \"id\": \"email-rbN62\"\r\n        }\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            \"segmentid1\",\r\n            \"segmentid2\"\r\n        ],\r\n        \"remove\": [\r\n            \"segmentid3\"\r\n        ]\r\n    }\r\n}"
        }
    ]
}    
```

### 요청 본문에 포함된 구성 가능한 집계 및 프로필을 사용하여 내보낸 프로필을 렌더링합니다. {#configurable-aggregation}

**요청**


다음 요청은 대상이 기대하는 형식과 일치하는 내보낸 프로필을 여러 개 렌더링합니다. 이 예에서 대상 ID는 구성 가능한 집계가 있는 대상 구성에 해당합니다. 요청 본문에 두 개의 프로필이 포함되며, 각각 세 개의 세그먼트 자격 및 5개의 ID가 있습니다. 를 사용하여 호출 시 전송할 프로필을 생성할 수 있습니다 [샘플 프로필 생성 API](sample-profile-generation-api.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
    "destinationId": "c2bc84c5-589c-43a1-96ea-becfa941f5be",
    "template": "{#- THIS is an example template for multiple profiles -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"profiles\": [\r\n    {%- for profile in input.profiles %}\r\n        {\r\n            \"identities\": [\r\n            {%- for idMapEntry in profile.identityMap -%}\r\n            {%- set namespace = idMapEntry.key -%}\r\n                {%- for identity in idMapEntry.value %}\r\n                {\r\n                    \"type\": \"{{ namespace }}\",\r\n                    \"id\": \"{{ customerData }}\"\r\n                }{%- if not loop.last -%},{%- endif -%}\r\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n            {% endfor %}\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                {%- for segment in profile.segmentMembership.ups | added %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ],\r\n                \"remove\": [\r\n                {#- Alternative syntax for filtering segments by status: -#}\r\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ]\r\n            }\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ]\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947859Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-biCbJ"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-0Q3hp"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-mN1Hw"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-MVw4L"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-2OjnN"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        },
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948187Z",
                        "status": "realized"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-fxt2p"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-sboQe"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-MRelR"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-M46ze"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-40Vrf"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**응답**

응답은 템플릿 렌더링 결과 또는 발생한 모든 오류를 반환합니다.
성공적인 응답은 내보낸 데이터의 세부 정보와 함께 HTTP 상태 200을 반환합니다. 응답에서 세그먼트 멤버십 및 ID를 기반으로 프로필을 집계하는 방법을 확인합니다. 에서 내보낸 프로필을 찾습니다. `output` 매개 변수(이스케이프 처리된 문자열)입니다.
실패한 응답은 발생한 오류에 대한 설명과 함께 HTTP 상태 400을 반환합니다.

```json
{
    "results": [
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        }
    ]
}
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 메시지 변환 템플릿을 사용하여 대상의 예상 데이터 형식과 일치하는 내보낸 프로필을 생성하는 방법을 알 수 있습니다. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../../guides/configure-destination-instructions.md) 대상 구성 프로세스에 이 단계가 어떤 영향을 주는지 이해하기 위해 노력합니다.
