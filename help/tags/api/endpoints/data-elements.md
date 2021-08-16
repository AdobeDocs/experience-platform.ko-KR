---
title: 데이터 요소 끝점
description: Reactor API에서 /data_elements 엔드포인트를 호출하는 방법을 알아봅니다.
source-git-commit: 53612919dc040a8a3ad35a3c5c0991554ffbea7c
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 6%

---

# 데이터 요소 끝점

데이터 요소는 애플리케이션 내의 중요한 데이터를 가리키는 변수 역할을 합니다. 데이터 요소는 [규칙](./rules.md) 및 [확장](./extensions.md) 구성 내에서 사용됩니다. 브라우저나 애플리케이션에서 런타임 시 규칙이 트리거되면 데이터 요소의 값이 확인되고 규칙 내에서 사용됩니다. 데이터 요소는 확장 구성에 대해 동일하게 작동합니다.

여러 데이터 요소를 함께 사용하면 데이터 사전 또는 데이터 맵이 생성됩니다. 이 사전은 Adobe Experience Platform이 알고 있으며 사용할 수 있는 데이터를 나타냅니다.

데이터 요소는 정확히 하나의 [속성](./properties.md)에 속합니다. 속성에는 많은 데이터 요소가 있을 수 있습니다.

데이터 요소 및 태그의 사용에 대한 일반적인 정보는 UI 설명서의 [데이터 요소 안내서](../../ui/managing-resources/data-elements.md)를 참조하십시오.

## 시작하기

이 안내서에 사용된 끝점은 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)의 일부입니다. 계속하기 전에 API 인증 방법에 대한 중요한 정보가 필요하면 [시작 안내서](../getting-started.md)를 검토하십시오.

## 데이터 요소 목록 검색 {#list}

GET 요청 경로에 속성의 ID를 포함하여 속성에 대한 데이터 요소 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /properties/{PROPERTY_ID}/data_elements
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 데이터 요소를 소유하는 속성의 `id` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 데이터 요소는 다음 속성을 기반으로 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>자세한 내용은 [응답 필터링](../guides/filtering.md)에 대한 안내서를 참조하십시오.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 속성에 대한 데이터 요소 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 데이터 요소 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 데이터 요소를 조회할 수 있습니다.

>[!NOTE]
>
>데이터 요소가 삭제되면 삭제된 것으로 표시되지만 실제로 시스템에서 제거되지 않습니다. 따라서 삭제된 데이터 요소를 조회할 수 있습니다. 삭제된 데이터 요소는 `data.meta.deleted_at` 특성이 있는 것으로 식별할 수 있습니다.

**API 형식**

```http
GET /data_elements/{DATA_ELEMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `DATA_ELEMENT_ID` | 조회할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 데이터 요소의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "DE8097636264104451ac3a18c95d5ff833",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:35:54.956Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:35:54 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:35:54.956Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/property"
        },
        "data": {
          "id": "PRa5621686159f44c880557e12af412a95",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/origin"
        },
        "data": {
          "id": "DE8097636264104451ac3a18c95d5ff833",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/extension"
        },
        "data": {
          "id": "EX085a465793b54be39b5408d13b50b46e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension"
        },
        "data": {
          "id": "EXf9a32699efde42e9b9410b43bd660848",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa5621686159f44c880557e12af412a95",
      "origin": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "self": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "extension": "https://reactor.adobe.io/extensions/EX085a465793b54be39b5408d13b50b46e"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 데이터 요소 만들기 {#create}

POST 요청을 만들어 새 데이터 요소를 만들 수 있습니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/data_elements
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 에서 데이터 요소를 정의하는 [속성](./properties.md)의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 지정된 속성에 대한 새 데이터 요소를 만듭니다. 또한 호출은 `relationships` 속성을 통해 데이터 요소를 기존 확장과 연결합니다. 자세한 내용은 [관계](../guides/relationships.md)의 안내서를 참조하십시오.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Data Element 2020-12-14 17:33:21 +0000",
            "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
            "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}",
            "default_value": "general_label",
            "enabled": true,
            "force_lower_case": true,
            "clean_text": true,
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
                "type": "extensions"
              }
            }
          },
          "type": "data_elements"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes.name` | **(필수)** 사용자가 읽을 수 있는 데이터 요소의 이름입니다. |
| `attributes.delegate_descriptor_id` | **(필수)** 데이터 요소를 확장 패키지와 연결하는 형식이 지정된 문자열입니다. 각 확장 패키지는 위임 데이터 요소에 대한 호환 유형과 의도한 동작을 정의하므로 모든 데이터 요소를 처음 만들 때 확장 패키지와 연결해야 합니다. 자세한 내용은 [위임 설명자 ID](../guides/delegate-descriptor-ids.md)의 안내서를 참조하십시오. |
| `attributes.settings` | 문자열로 표시되는 설정 JSON 개체. |
| `attributes.default_value` | 데이터 요소가 `undefined`으로 평가되는 경우 반환할 기본값입니다. |
| `attributes.enabled` | 데이터 요소가 활성화되어 있는지 여부를 나타내는 부울 값입니다. |
| `attributes.force_lower_case` | 저장하기 전에 데이터 요소 값을 소문자로 변환해야 하는지 여부를 나타내는 부울 값입니다. |
| `attributes.clean_text` | 저장하기 전에 데이터 요소 값에서 선행 및 후행 공백을 제거해야 하는지 여부를 나타내는 부울 값입니다. |
| `type` | 업데이트할 리소스 유형입니다. 이 끝점의 경우 값은 `data_elements`이어야 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 새로 만든 데이터 요소의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 데이터 요소 업데이트 {#update}

PATCH 요청 경로에 해당 ID를 포함하여 데이터 요소를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `DATA_ELEMENT_ID` | 업데이트할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 데이터 요소에 대한 `name`을 업데이트합니다.

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 속성이 데이터 요소에 대해 업데이트할 속성을 나타내는 객체입니다. 모든 데이터 요소 속성을 업데이트할 수 있습니다. 속성 목록 및 사용 사례에는 [데이터 요소 만들기](#create)에 대한 예제 호출을 참조하십시오. |
| `id` | 업데이트할 데이터 요소의 `id` 이 값은 요청 경로에 제공된 `{DATA_ELEMENT_ID}` 값과 일치해야 합니다. |
| `type` | 업데이트할 리소스 유형입니다. 이 끝점의 경우 값은 `data_elements`이어야 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 업데이트된 데이터 요소의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 데이터 요소 수정 {#revise}

데이터 요소를 개정할 때 현재(head) 개정으로 데이터 요소의 새 개정이 만들어집니다. 데이터 요소의 각 수정에는 자체 ID가 있습니다. 원본 데이터 요소는 원본 링크를 통해 검색될 수 있다.

PATCH 요청 본문에서 `revise` 값과 함께 `meta.action` 속성을 제공하여 데이터 요소를 수정할 수 있습니다.

**API 형식**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `DATA_ELEMENT_ID` | 수정할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "meta": {
            "action": "revise"
          },
          "id": "DE7d7284657ee540ee8f402277860e9f8a",
          "type": "data_elements"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 속성이 데이터 요소에 대해 업데이트할 속성을 나타내는 객체입니다. 모든 데이터 요소 속성을 업데이트할 수 있습니다. 속성 목록 및 사용 사례에는 [데이터 요소 만들기](#create)에 대한 예제 호출을 참조하십시오. |
| `meta.action` | `revise` 값에 를 포함하는 경우 이 속성은 데이터 요소에 대해 새 개정을 만들어야 함을 나타냅니다. |
| `id` | 수정할 데이터 요소의 `id` 이 값은 요청 경로에 제공된 `{DATA_ELEMENT_ID}` 값과 일치해야 합니다. |
| `type` | 수정할 리소스 유형입니다. 이 끝점의 경우 값은 `data_elements`이어야 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공한 응답은 증가된 `meta.latest_revision_number` 속성에 표시된 대로 데이터 요소에 대한 새 개정 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## 데이터 요소 삭제

DELETE 요청 경로에 해당 ID를 포함하여 데이터 요소를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /data_elements/{DATA_ELEMENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `DATA_ELEMENT_ID` | 삭제할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적으로 응답하면 데이터 요소가 삭제되었음을 나타내는 응답 본문이 없는 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

## 데이터 요소에 대한 참고 사항 관리 {#notes}

데이터 요소는 &quot;주목할 만한&quot; 리소스입니다. 즉, 각 개별 리소스에서 텍스트 기반 메모를 만들고 검색할 수 있습니다. 데이터 요소 및 기타 호환 리소스에 대한 메모를 관리하는 방법에 대한 자세한 내용은 [참고 엔드포인트 안내서](./notes.md)를 참조하십시오.

## 데이터 요소에 대한 관련 리소스 검색 {#related}

다음 호출에서는 데이터 요소에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. [데이터 요소를 찾을 때 ](#lookup) 속성 아래에 이러한 관계가 나열됩니다.`relationships`

Reactor API의 관계에 대한 자세한 내용은 [관계 안내서](../guides/relationships.md)를 참조하십시오.

### 데이터 요소에 대한 관련 라이브러리 나열 {#libraries}

조회 요청의 경로에 `/libraries`을 추가하여 데이터 요소를 활용하는 라이브러리를 나열할 수 있습니다.

**API 형식**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/libraries
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 라이브러리를 나열할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 데이터 요소를 사용하는 라이브러리 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 데이터 요소에 대한 관련 수정 버전 나열 {#revisions}

조회 요청의 경로에 `/revisions`을 추가하여 데이터 요소의 이전 수정 버전을 나열할 수 있습니다.

**API 형식**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/revisions
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 수정 내용을 나열할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 데이터 요소의 개정 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "DEaeceb5164d494c768c18e37ec6f3b091",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:06.488Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:37:06.488Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "DE5172417ff56e43d2a99ca149021bf65a",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:05.920Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:37:05.920Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

### 데이터 요소에 대한 관련 확장 조회 {#extension}

GET 요청의 경로에 `/extension`을 추가하여 데이터 요소를 활용하는 확장을 조회할 수 있습니다.

**API 형식**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/extension
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 확장을 조회할 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 데이터 요소를 사용하는 확장의 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "EX9c7f9f1e826149978f2dadaf4c639679",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:37:31.952Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:31.952Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/property"
        },
        "data": {
          "id": "PR5c15543ef7bb403abc79d65fee0bf1f9",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/origin"
        },
        "data": {
          "id": "EX9c7f9f1e826149978f2dadaf4c639679",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5c15543ef7bb403abc79d65fee0bf1f9",
      "origin": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "self": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 데이터 요소에 대한 관련 원본 조회 {#origin}

GET 요청의 경로에 `/origin`을 추가하여 데이터 요소의 출처를 조회할 수 있습니다. 데이터 요소의 원본은 현재 개정을 만들기 위해 업데이트된 이전 개정입니다.

**API 형식**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/origin
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 원본을 조회하려는 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 데이터 요소의 원본 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "DE790cb76f91594c2082a727b9f97024f6",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:37:19.891Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:37:19 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:19.891Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/property"
        },
        "data": {
          "id": "PRf1ac400fb1e04c689e28d5efcd675c94",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/origin"
        },
        "data": {
          "id": "DE790cb76f91594c2082a727b9f97024f6",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/extension"
        },
        "data": {
          "id": "EX2345dba2c8b34d1cbe2795e29c62bf27",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension"
        },
        "data": {
          "id": "EXad7ebb72d721478483b741eebfffda6a",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRf1ac400fb1e04c689e28d5efcd675c94",
      "origin": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "self": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "extension": "https://reactor.adobe.io/extensions/EX2345dba2c8b34d1cbe2795e29c62bf27"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 데이터 요소에 대한 관련 속성 조회 {#property}

GET 요청 경로에 `/property`을 추가하여 데이터 요소를 소유하는 속성을 찾을 수 있습니다.

**API 형식**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/property
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 속성을 조회하려는 데이터 요소의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 데이터 요소를 소유하는 속성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "PRae9440b0f3234c4286569485f2b7a6a2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:40.829Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:40.829Z",
      "platform": "web",
      "development": false,
      "token": "42daac072e1e",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments",
      "extensions": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions",
      "rules": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules",
      "self": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
