---
title: 흐름 서비스 API를 사용하여 Streaming SDK에 대한 새 연결 사양 만들기
description: 다음 문서에서는 Flow Service API를 사용하여 연결 사양을 만들고 셀프 서비스 소스를 통해 새 소스를 통합하는 방법에 대한 단계를 제공합니다.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 새 연결 사양 만들기

>[!NOTE]
>
>Streaming SDK는 베타 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

연결 사양은 소스의 구조를 나타냅니다. 여기에는 소스의 인증 요구 사항에 대한 정보가 포함되어 있으며 소스 데이터를 탐색하고 검사하는 방법을 정의하고 주어진 소스의 속성에 대한 정보를 제공합니다. [!DNL Flow Service] API의 `/connectionSpecs` 끝점을 사용하면 조직 내에서 연결 사양을 프로그래밍 방식으로 관리할 수 있습니다.

다음 문서에서는 [!DNL Flow Service] API를 사용하여 연결 사양을 만들고 셀프 서비스 소스(Streaming SDK)를 통해 새 소스를 통합하는 방법에 대한 단계를 설명합니다.

## 시작하기

계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 아티팩트 수집

셀프서비스 소스를 사용하여 새 스트리밍 소스를 만들려면 먼저 Adobe과 조정하고, 개인 Git 저장소를 요청하고, 소스의 레이블, 설명, 카테고리 및 아이콘과 관련된 세부 정보에 대한 Adobe과 일치해야 합니다.

제공된 후에는 다음과 같이 개인 Git 저장소를 구성해야 합니다.

* 소스
   * {your_source}
      * 아티팩트
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 아티팩트(파일 이름) | 설명 | 예 |
| --- | --- | --- |
| {your_source} | 소스의 이름입니다. 이 폴더에는 개인 Git 저장소 내에 있는 소스와 관련된 모든 아티팩트가 포함되어야 합니다. | `medallia` |
| {your_source}-category.txt | 텍스트 파일 형식의 소스가 속한 범주입니다. **참고**: 원본이 위의 범주에 맞지 않는다고 생각되면 Adobe 담당자에게 문의하여 논의하십시오. | `medallia-category.txt` 파일 내에서 원본의 범주를 지정하십시오(예: `streaming`). |
| {your_source}-description.txt | 소스에 대한 간략한 설명. | [!DNL Medallia]은(는) [!DNL Medallia] 데이터를 Experience Platform 상태로 만드는 데 사용할 수 있는 마케팅 자동화 소스입니다. |
| {your_source}-icon.svg | Experience Platform 소스 카탈로그에서 소스를 나타내는 데 사용할 이미지입니다. 이 아이콘은 SVG 파일이어야 합니다. |
| {your_source}-label.txt | Experience Platform 소스 카탈로그에 표시되어야 하는 소스의 이름입니다. | 메달리아 |
| {your_source}-connectionSpec.json | 소스의 연결 사양이 포함된 JSON 파일. 이 안내서를 완료할 때 연결 사양을 채우므로 이 파일은 처음에 필요하지 않습니다. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>연결 사양의 테스트 기간 동안 키 값 대신 연결 사양의 `text`을(를) 사용할 수 있습니다.

필요한 파일을 개인 Git 저장소에 추가한 후에는 Adobe이 검토할 끌어오기 요청(PR)을 만들어야 합니다. PR이 승인되고 병합되면 소스의 레이블, 설명 및 아이콘을 참조하는 연결 사양에 사용할 수 있는 ID가 제공됩니다.

다음으로 아래에 설명된 단계에 따라 연결 사양을 구성합니다. 고급 예약, 사용자 지정 스키마 또는 다양한 페이지 매김 유형과 같이 소스에 추가할 수 있는 다양한 기능에 대한 추가 지침은 [소스 사양 구성](../config/sourcespec.md)의 안내서를 검토하십시오.

## 연결 사양 템플릿 복사

필요한 아티팩트를 수집했으면 아래의 연결 사양 템플릿을 복사하여 선택한 텍스트 편집기에 붙여 넣은 다음 대괄호 `{}`의 특성을 특정 소스와 관련된 정보로 업데이트합니다.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## 연결 사양 만들기 {#create}

연결 사양 템플리트를 확보하면 이제 출처에 해당하는 적절한 값을 입력하여 새 연결 사양 작성을 시작할 수 있습니다.

연결 사양은 소스 사양과 탐색 사양의 두 부분으로 나눌 수 있습니다.

연결 사양의 섹션에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [소스 사양 구성](../config/sourcespec.md)
* [탐색 사양 구성](../config/explorespec.md)

사양 정보를 업데이트하면 [!DNL Flow Service] API의 `/connectionSpecs` 끝점에 POST 요청을 하여 새 연결 사양을 제출할 수 있습니다.

**API 형식**

```http
POST /connectionSpecs
```

**요청**

다음 요청은 스트리밍 소스에 대한 전체 작성 연결 사양의 예입니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**응답**

응답이 성공하면 고유한 `id`을(를) 포함하여 새로 만든 연결 사양이 반환됩니다.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## 다음 단계

이제 새 연결 사양을 만들었으므로 해당 연결 사양 ID를 기존 흐름 사양에 추가해야 합니다. 자세한 내용은 [흐름 사양 업데이트](./update-flow-specs.md)에 대한 자습서를 참조하십시오.

만든 연결 사양을 수정하려면 [연결 사양 업데이트](./update-connection-specs.md)에 대한 자습서를 참조하십시오.
