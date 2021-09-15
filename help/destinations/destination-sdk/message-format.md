---
description: 이 페이지의 콘텐츠와 파트너 대상에 대한 나머지 구성 옵션을 함께 사용하십시오. 이 페이지에서는 Adobe Experience Platform에서 대상으로 내보낸 데이터의 메시징 형식을 다룹니다. 반면 다른 페이지에서는 대상에 연결 및 인증에 대한 세부 사항을 다룹니다.
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: 메시지 포맷
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: add6c7c4f3a60bd9ee2c2b77a8a242c4df03377b
workflow-type: tm+mt
source-wordcount: '2056'
ht-degree: 2%

---

# 메시지 포맷

## 사전 요구 사항 - Adobe Experience Platform 개념 {#prerequisites}

Adobe 측의 프로세스를 이해하려면 다음 Experience Platform 개념을 숙지하십시오.

* **XDM(경험 데이터 모델)**. [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko) 에서 XDM 스키마  [를 만드는 방법 및 XDM 개요](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **클래스**. [UI에서 클래스를 만들고 편집합니다](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **필드 그룹**. [필드 그룹 ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) 정의 및  [필드 그룹에 대한 자세한 정보입니다](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group).
* **IdentityMap**&#x200B;을 참조하십시오. ID 맵은 Adobe Experience Platform의 모든 최종 사용자 ID의 맵을 나타냅니다. [XDM 필드 사전](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en)에서 `xdm:identityMap` 을 참조하십시오.
* **세그먼트 멤버십**. [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM 속성은 프로필이 구성원으로 있는 세그먼트를 알려줍니다. `status` 필드의 세 가지 다른 값에 대해 [세그먼트 멤버십 세부 사항 스키마 필드 그룹](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)에 대한 설명서를 읽어 보십시오.

## 개요 {#overview}

이 페이지의 콘텐츠와 파트너 대상](./configuration-options.md)에 대한 나머지 [구성 옵션을 함께 사용하십시오. 이 페이지에서는 Adobe Experience Platform에서 대상으로 내보낸 데이터의 메시징 형식을 다룹니다. 반면 다른 페이지에서는 대상에 연결 및 인증에 대한 세부 사항을 다룹니다.

Adobe Experience Platform은 다양한 데이터 형식으로 데이터를 상당한 수의 대상으로 내보냅니다. 대상 유형의 예로는 광고 플랫폼(Google), 소셜 네트워크(Facebook), 클라우드 저장소 위치(Amazon S3, Azure 이벤트 허브)가 있습니다.

Experience Platform은 내보낸 메시지 형식을 측면에서 예상되는 형식과 일치하도록 조정할 수 있습니다. 이 사용자 지정을 이해하려면 다음 개념이 중요합니다.
* Adobe Experience Platform의 소스(1) 및 대상(2) XDM 스키마
* 파트너 측(3)에 있는 메시지 형식 및
* [메시지 변환 템플릿](./message-format.md#using-templating)을(를) 만들어 정의할 수 있는 둘 사이의 변환 계층.

![스키마를 JSON 변형으로 변환](./assets/transformations-3-steps.png)

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다.

대상에 데이터를 활성화하려는 사용자는 Experience Platform에서 데이터 세트에 사용하는 필드를 대상의 예상 형식으로 변환하는 스키마에 매핑해야 합니다. Adobe은 회사에 타겟 스키마에 추가할 사용자 지정 필드 그룹을 만듭니다. 필드 그룹의 필드는 수신할 수 있는 프로필 속성 필드에 따라 다릅니다.

**소스 XDM 스키마(1)**: 고객이 Experience Platform에서 사용하는 스키마를 나타냅니다. Experience Platform의 대상 활성화 워크플로우의 [매핑 단계에서 고객은 소스 스키마의 필드를 대상의 대상 스키마(2)에 매핑합니다.](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping)

**Target XDM 스키마(2)**: Adobe과 공유하는 JSON 표준 스키마(3)를 기반으로 Adobe 팀이 대상에 대한 사용자 지정 스키마를 만듭니다. 프로젝트의 [향후 단계에서는 사용자 대상에 대한 사용자 지정 스키마를 직접 만들 수 있습니다.](./overview.md#phased-approach)

**대상 프로필 속성의 JSON 표준 스키마(3)**: 플랫폼이 지원하는  [모든 ](https://json-schema.org/learn/miscellaneous-examples.html) 프로필 속성 및 해당 유형의 JSON 스키마를 공유하십시오(예: 개체, 문자열, 배열). 대상이 지원할 수 있는 예제 필드는 `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` 등입니다.

위에서 설명한 스키마 변형을 기반으로 소스 XDM 스키마와 파트너 측의 샘플 스키마 간에 메시지 구조가 변경되는 방법을 설명합니다.

![변형 메시지 예](./assets/transformations-with-examples.png)

<br> 


## 시작하기 - 세 가지 기본 속성 변형 {#getting-started}

변환 프로세스를 보여주기 위해 아래 예제는 Adobe Experience Platform에서 세 가지 공통 프로필 속성을 사용합니다. **이름**, **성** 및 **전자 메일 주소**

>[!NOTE]
>
>고객은 [대상 워크플로우 활성화](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping)의 **매핑** 단계에서 소스 XDM 스키마의 속성을 Adobe Experience Platform UI의 파트너 XDM 스키마에 매핑합니다.

플랫폼이 다음과 같은 메시지 형식을 수신할 수 있다고 가정합니다.

```curl
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

메시지 형식을 고려할 때 해당 변형은 다음과 같습니다.

| Adobe 측의 파트너 XDM 스키마의 속성 | 변환 | 사용자 측의 HTTP 메시지에 있는 속성 |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

## ID, 속성 및 세그먼트 멤버십 변환에 템플릿 언어 사용 {#using-templating}

Adobe은 [Jinja](https://jinja.palletsprojects.com/en/2.11.x/)와 유사한 템플릿 언어를 사용하여 XDM 스키마에서 해당 필드를 대상에서 지원하는 형식으로 변환합니다.

이 섹션에서는 입력 XDM 스키마에서 템플릿을 통해 이러한 변환이 수행되는 방식에 대한 몇 가지 예를 제공하고 대상에서 허용하는 페이로드 형식으로 출력합니다. 아래 예는 다음과 같이 복잡도를 증가시켜 정렬됩니다.

1. 단순 변형 예 [프로필 속성](./message-format.md#attributes), [세그먼트 멤버십](./message-format.md#segment-membership) 및 [ID](./message-format.md#identities) 필드에 대한 간단한 변형에서 템플릿 작업이 작동하는 방식을 알아봅니다.
2. 위의 필드를 결합하는 템플릿의 복잡성 증가 예: [세그먼트와 ID](./message-format.md#segments-and-identities) 및 [세그먼트, ID 및 프로필 속성을 보내는 템플릿을 만듭니다](./message-format.md#segments-identities-attributes).
3. 템플릿에는 집계 키가 포함됩니다. 대상 구성에서 [구성 가능한 집계](./destination-configuration.md#configurable-aggregation)를 사용하는 경우 Experience Platform은 세그먼트 ID, 세그먼트 상태 또는 ID 네임스페이스와 같은 기준에 따라 대상에 내보낸 프로필을 그룹화합니다.

### 프로필 속성 {#attributes}

대상으로 내보낸 프로필 속성을 변형하려면 아래의 JSON 및 코드 샘플을 참조하십시오.

>[!IMPORTANT]
>
>Adobe Experience Platform에서 사용 가능한 모든 프로필 속성 목록을 보려면 [XDM 필드 사전](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) 을 참조하십시오.


**입력**

프로필 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

프로필 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**템플릿**

>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**결과**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### 세그먼트 멤버십 {#segment-membership}

[segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM 속성은 프로필이 구성원으로 있는 세그먼트를 알려줍니다.
`status` 필드의 세 가지 다른 값에 대해 [세그먼트 멤버십 세부 사항 스키마 필드 그룹](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)에 대한 설명서를 읽어 보십시오.

**입력**

프로필 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "existing"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

프로필 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "existing"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**템플릿**


>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**결과**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### ID {#identities}

Experience Platform의 ID에 대한 자세한 내용은 [ID 네임스페이스 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)를 참조하십시오.

**입력**

프로필 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

프로필 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**템플릿**


>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**결과**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```


### 세그먼트 및 ID를 보내는 템플릿 만들기 {#segments-and-identities}

이 섹션에서는 Adobe XDM 스키마와 파트너 대상 스키마 간에 일반적으로 사용되는 변환의 예를 제공합니다.
아래 예는 세그먼트 멤버십 및 ID 형식을 변형하고 대상으로 출력하는 방법을 보여줍니다.

**입력**

프로필 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "existing"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

프로필 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**템플릿**

>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering segments by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**결과**

아래 `json`은 Adobe Experience Platform에서 내보낸 데이터를 나타냅니다.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### 세그먼트, ID 및 프로필 속성을 보내는 템플릿을 만듭니다 {#segments-identities-attributes}

이 섹션에서는 Adobe XDM 스키마와 파트너 대상 스키마 간에 일반적으로 사용되는 변환의 예를 제공합니다.

다른 일반적인 사용 사례는 세그먼트 멤버십, ID가 포함된 데이터를 내보내는 것입니다(예: 이메일 주소, 전화번호, 광고 ID) 및 프로필 속성. 이러한 방식으로 데이터를 내보내려면 아래 예를 참조하십시오.

**입력**

프로필 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "existing"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

프로필 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**템플릿**

>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**결과**

아래 `json`은 Adobe Experience Platform에서 내보낸 데이터를 나타냅니다.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### 템플릿에 집계 키를 포함하여 다양한 기준으로 그룹화된 내보낸 프로필에 액세스합니다 {#template-aggregation-key}

대상 구성에서 [구성 가능한 집계](./destination-configuration.md#configurable-aggregation)를 사용하는 경우 세그먼트 ID, 세그먼트 별칭, 세그먼트 멤버십 또는 ID 네임스페이스와 같은 기준에 따라 대상에 내보낸 프로필을 그룹화할 수 있습니다.

메시지 변환 템플릿에서 다음 섹션의 예제와 같이 위에 언급된 집계 키에 액세스할 수 있습니다. 이렇게 하면 Experience Platform에서 내보낸 HTTP 메시지의 형식을 대상에서 기대하는 형식과 일치하도록 만드는 데 도움이 됩니다.

#### 템플릿에서 세그먼트 ID 집계 키 사용 {#aggregation-key-segment-id}

[구성 가능한 집계](./destination-configuration.md#configurable-aggregation)를 사용하고 `includeSegmentId`를 true로 설정하면 대상에 내보낸 HTTP 메시지의 프로필이 세그먼트 ID로 그룹화됩니다. 템플릿에서 세그먼트 ID에 액세스할 수 있는 방법은 아래를 참조하십시오.

**입력**

아래의 네 가지 프로필을 고려해 보십시오. 여기서
* 첫 번째 두 항목은 세그먼트 ID가 `788d8874-8007-4253-92b7-ee6b6c20c6f3`인 세그먼트의 일부입니다
* 세 번째 프로필은 세그먼트 ID가 `8f812592-3f06-416b-bd50-e7831848a31a`인 세그먼트의 일부입니다
* 네 번째 프로필은 위의 두 세그먼트 중 일부입니다.

프로필 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      },
      "birthDate":{
         
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

프로필 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      },
      "birthDate":{
         "value":"1980/07/31"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

프로필 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      },
      "birthDate":{
         
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"existing"
         }
      }
   }
}
```

프로필 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      },
      "birthDate":{
         "value":"1940/01/01"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"existing"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

**템플릿**

>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

템플릿에서 `audienceId` 을 사용하여 세그먼트 ID에 액세스하는 방법은 아래에 나와 있습니다. 대상 분류에서 세그먼트 멤버십에 `audienceId`을 사용한다고 가정합니다. 고유한 분류에 따라 다른 모든 필드 이름을 대신 사용할 수 있습니다.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**결과**

대상으로 내보내면 프로필은 세그먼트 ID를 기반으로 두 그룹으로 분할됩니다.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione",
         "birthDate":null
      },
      {
         "firstName":"Harry",
         "birthDate":"1980/07/31"
      },
      {
         "firstName":"Jerry",
         "birthDate":"1940/01/01"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom",
         "birthDate":null
      },
      {
         "firstName":"Jerry",
         "birthDate":"1940/01/01"
      }
   ]
}
```

#### 템플릿에서 세그먼트 별칭 집계 키 사용 {#aggregation-key-segment-alias}

[구성 가능한 집계](./destination-configuration.md#configurable-aggregation)를 사용하고 `includeSegmentId`를 true로 설정하면 템플릿의 세그먼트 별칭에 액세스할 수도 있습니다.

아래 줄을 템플릿에 추가하여 세그먼트 별칭으로 그룹화된 내보낸 프로필에 액세스합니다.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### 템플릿에서 세그먼트 상태 집계 키 사용 {#aggregation-key-segment-status}

[구성 가능한 집계](./destination-configuration.md#configurable-aggregation) 를 사용하고 `includeSegmentId` 및 `includeSegmentStatus`를 true로 설정하는 경우, 세그먼트의 세그먼트 상태에 액세스하여 세그먼트에서 프로필을 추가 또는 제거할지 여부에 따라 대상에 내보낸 HTTP 메시지의 프로필을 그룹화할 수 있습니다.

가능한 값은 다음과 같습니다.

* 실현
* 기존
* 종료한

위의 값에 따라 템플릿에 아래 줄을 추가하여 세그먼트에서 프로필을 추가하거나 제거합니다.

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### 템플릿에서 ID 네임스페이스 집계 키 사용 {#aggregation-key-identity}

다음은 대상 구성에서 [구성 가능한 집계](./destination-configuration.md#configurable-aggregation)가 ID 네임스페이스로 내보낸 프로필을 `"identityNamespaces": ["email", "phone"]` 형식으로 집계하도록 설정된 예입니다

**입력**

프로필 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ]
   }
}
```

프로필 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ]
   }
}
```

**템플릿**

>[!IMPORTANT]
>
>사용하는 모든 템플릿의 경우 [대상 서버 구성](./server-and-template-configuration.md#template-specs)에 템플릿을 삽입하기 전에 큰따옴표 `""`와 같은 잘못된 문자를 이스케이프 처리해야 합니다. 큰따옴표 이스케이프에 대한 자세한 내용은 [JSON 표준](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)의 9장을 참조하십시오.

`input.aggregationKey.identityNamespaces`은 아래 템플릿에서 사용됩니다

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**결과**

아래 `json`은 Adobe Experience Platform에서 내보낸 데이터를 나타냅니다.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

#### URL 템플릿에서 집계 키 사용 {#aggregation-key-url-template}

사용 사례에 따라 아래 표시된 대로 URL에 여기에 설명된 집계 키를 사용할 수도 있습니다.

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### 참조: 변환 템플릿에 사용되는 컨텍스트 및 함수 {#reference}

템플릿에 제공된 컨텍스트에는 `input`(이 호출에서 내보낸 프로필/데이터) 및 `destination`(Adobe이 데이터를 보내는 대상에 대한 데이터, 모든 프로필에 유효)가 포함됩니다.

아래 표는 위의 예에서 함수에 대한 설명을 제공합니다.

| 함수 | 설명 |
|---------|----------|
| `input.profile` | [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html)로 표시되는 프로필입니다. 이 페이지에서 위에 언급된 파트너 XDM 스키마를 따릅니다. |
| `destination.segmentAliases` | Adobe Experience Platform 네임스페이스의 세그먼트 ID에서 파트너 시스템의 세그먼트 별칭에 매핑합니다. |
| `destination.segmentNames` | Adobe Experience Platform 네임스페이스의 세그먼트 이름에서 파트너 시스템의 세그먼트 이름에 매핑합니다. |
| `addedSegments(listOfSegments)` | 상태 `realized` 또는 `existing`가 있는 세그먼트만 반환합니다. |
| `removedSegments(listOfSegments)` | 상태가 `exited`인 세그먼트만 반환합니다. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
