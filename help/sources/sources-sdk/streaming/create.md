---
title: Flow Service API를 사용하여 스트리밍 SDK에 대한 새로운 연결 사양을 만듭니다
description: 다음 문서에서는 Flow Service API를 사용하여 연결 사양을 만들고 Self-Serve Sources를 통해 새 소스를 통합하는 방법에 대해 설명합니다.
hide: true
hidefromtoc: true
source-git-commit: f91ebcf8e27fd7d9019c5bb6d270b89fd08785ef
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# 를 사용하여 새 연결 사양을 만듭니다 [!DNL Flow Service] API

연결 사양은 소스의 구조를 나타냅니다. 소스 인증 요구 사항에 대한 정보를 포함하고, 소스 데이터를 탐색하고 검사할 수 있는 방법을 정의하며, 지정된 소스의 특성에 대한 정보를 제공합니다. 다음 `/connectionSpecs` 의 엔드포인트 [!DNL Flow Service] API를 사용하면 조직 내에서 연결 사양을 프로그래밍 방식으로 관리할 수 있습니다.

다음 문서에서는 [!DNL Flow Service] API를 사용하고 셀프서비스 소스(스트리밍 SDK)를 통해 새 소스를 통합합니다.

## 시작하기

계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 객체 수집

셀프 서비스 소스를 사용하여 새 스트리밍 소스를 만들려면 먼저 Adobe과 조정하고, 비공개 Git 리포지토리를 요청하고, 소스의 레이블, 설명, 카테고리 및 아이콘에 대한 세부 사항을 Adobe과 정렬해야 합니다.

제공되면 다음과 같이 개인 Git 리포지토리를 구성해야 합니다.

* 소스
   * {your_source}
      * 가공물
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 객체(파일 이름) | 설명 | 예 |
| --- | --- | --- |
| {your_source} | 소스의 이름입니다. 이 폴더에는 개인 Git 리포지토리 내에서 소스와 관련된 모든 아티팩트가 포함되어야 합니다. | `medallia` |
| {your_source}-category.txt | 소스가 속한 범주로 텍스트 파일로 서식이 지정됩니다. **참고**: 소스가 위의 카테고리에 맞지 않는다고 생각되면 Adobe 담당자에게 연락하여 상의하십시오. | `medallia-category.txt` 파일 내에서 다음과 같이 소스의 카테고리를 지정하십시오. `streaming`. |
| {your_source}-description.txt | 출처에 대한 간략한 설명. | [!DNL Medallia] 가져올 수 있는 마케팅 자동화 소스입니다 [!DNL Medallia] Experience Platform 데이터. |
| {your_source}-icon.svg | Experience Platform 소스 카탈로그에서 소스를 나타내는 데 사용할 이미지입니다. 이 아이콘은 SVG 파일이어야 합니다. |
| {your_source}-label.txt | Experience Platform 소스 카탈로그에 표시되는 소스의 이름입니다. | 메달리아 |
| {your_source}-connectionSpec.json | 소스의 연결 사양을 포함하는 JSON 파일입니다. 이 안내서를 완료할 때 연결 사양을 채울 것이므로 이 파일이 처음에 필요하지 않습니다. | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>연결 사양의 테스트 기간 동안 키 값 대신 를 사용할 수 있습니다 `text` 연결 사양에서 참조할 수 있습니다.

개인 Git 리포지토리에 필요한 파일을 추가했으면 Adobe이 검토할 가져오기 요청(PR)을 만들어야 합니다. PR이 승인되고 병합되면 소스의 레이블, 설명 및 아이콘을 참조하기 위해 연결 사양에 사용할 수 있는 ID가 제공됩니다.

다음으로, 연결 사양을 구성하려면 아래 설명된 단계를 따릅니다. 고급 예약, 사용자 지정 스키마 또는 다양한 페이지 매김 유형과 같이 소스에 추가할 수 있는 다양한 기능에 대한 추가 지침은 [소스 사양 구성](../config/sourcespec.md).

## 연결 사양 템플릿 복사

필요한 가공물을 수집한 후에는 아래 연결 사양 템플릿을 복사하여 선택한 텍스트 편집기에 붙여넣은 다음 대괄호로 속성을 업데이트합니다 `{}` 을 참조하십시오.

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
  "authSpec": [

  ],
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
  }
}
```

## 연결 사양 만들기 {#create}

연결 사양 템플릿을 획득하면 이제 소스에 해당하는 적절한 값을 입력하여 새 연결 사양 작성을 시작할 수 있습니다.

연결 사양은 두 개의 개별 부분으로 나눌 수 있습니다. 소스 사양 및 탐색 사양입니다.

연결 사양의 섹션에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [소스 사양 구성](../config/sourcespec.md)
* [탐색 사양 구성](../config/explorespec.md)

사양명세 정보가 업데이트되면, POST 요청을 수행하여 새 연결 사양을 `/connectionSpecs` 의 끝점 [!DNL Flow Service] API.

**API 형식**

```http
POST /connectionSpecs
```

**요청**

다음 요청은 스트리밍 소스에 대한 완전히 작성된 연결 사양의 예입니다.

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

성공적인 응답은 해당 고유한 연결을 포함하여 새로 생성된 연결 사양을 반환합니다 `id`.

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

새 연결 사양을 만들었으므로 이제 해당 연결 사양 ID를 기존 흐름 사양에 추가해야 합니다. 다음에서 자습서를 참조하십시오. [흐름 사양 업데이트](./update-flow-specs.md) 추가 정보.

생성한 연결 사양을 수정하려면 다음을 참조하십시오. [연결 사양 업데이트](./update-connection-specs.md).
