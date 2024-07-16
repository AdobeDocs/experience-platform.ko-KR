---
keywords: Experience Platform;홈;인기 항목;스트리밍 수집;수집;여러 메시지 스트리밍;여러 메시지;
solution: Experience Platform
title: 단일 HTTP 요청으로 여러 메시지 보내기
type: Tutorial
description: 이 문서에서는 스트리밍 수집을 사용하여 단일 HTTP 요청 내에서 Adobe Experience Platform에 여러 메시지를 전송하는 자습서를 제공합니다.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 1%

---

# 단일 HTTP 요청으로 여러 메시지 보내기

Adobe Experience Platform으로 데이터를 스트리밍할 때 많은 HTTP 호출을 수행하면 많은 비용이 들 수 있습니다. 예를 들어 1KB 페이로드를 사용하여 200개의 HTTP 요청을 만드는 대신 200KB의 단일 페이로드를 사용하여 각각 1KB의 200개의 메시지로 1개의 HTTP 요청을 만드는 것이 훨씬 효율적입니다. 올바르게 사용하는 경우 단일 요청 내에서 여러 메시지를 그룹화하는 것이 [!DNL Experience Platform](으)로 전송되는 데이터를 최적화하는 좋은 방법입니다.

이 문서에서는 스트리밍 수집을 사용하여 단일 HTTP 요청 내에서 [!DNL Experience Platform]에게 여러 메시지를 보내는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform [!DNL Data Ingestion]을(를) 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

- [데이터 수집 개요](../home.md): 수집 방법 및 Data Connectors를 포함하여 [!DNL Experience Platform Data Ingestion]의 핵심 개념을 다룹니다.
- [스트리밍 수집 개요](../streaming-ingestion/overview.md): 스트리밍 연결, 데이터 세트, [!DNL XDM Individual Profile] 및 [!DNL XDM ExperienceEvent]과(와) 같은 스트리밍 수집의 워크플로 및 기본 구성 요소입니다.

또한 이 자습서에서는 [!DNL Platform]개의 API를 성공적으로 호출하려면 [Adobe Experience Platform에 대한 인증](https://www.adobe.com/go/platform-api-authentication-en) 자습서를 완료해야 합니다. 인증 자습서를 완료하면 이 자습서의 모든 API 호출에 필요한 인증 헤더 값이 제공됩니다. 헤더는 다음과 같이 샘플 호출에 표시됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`

모든 POST 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 스트리밍 연결 만들기

[!DNL Experience Platform](으)로 데이터 스트리밍을 시작하려면 먼저 스트리밍 연결을 만들어야 합니다. 스트리밍 연결을 만드는 방법에 대해 알아보려면 [스트리밍 연결 만들기](./create-streaming-connection.md) 안내서를 읽어 보십시오.

스트리밍 연결을 등록한 후 데이터 생성자는 데이터를 Platform에 스트리밍하는 데 사용할 수 있는 고유한 URL을 갖게 됩니다.

## 데이터 세트로 스트리밍

다음 예는 단일 HTTP 요청 내의 특정 데이터 세트에 여러 메시지를 보내는 방법을 보여줍니다. 데이터 세트 ID를 메시지 헤더에 삽입하여 해당 메시지를 직접 수집할 수 있습니다.

[!DNL Platform] UI를 사용하거나 API의 목록 작업을 사용하여 기존 데이터 세트의 ID를 가져올 수 있습니다. **[!UICONTROL 데이터 세트]** 탭으로 이동하여 ID를 사용할 데이터 세트를 클릭하고 **[!UICONTROL 정보]** 탭의 데이터 세트 ID 필드에서 문자열을 복사하여 [Experience Platform](https://platform.adobe.com)에서 데이터 세트 ID를 찾을 수 있습니다. API를 사용하여 데이터 세트를 검색하는 방법에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하세요.

기존 데이터 세트를 사용하는 대신 새 데이터 세트를 만들 수 있습니다. API를 사용하여 데이터 집합을 만드는 방법에 대한 자세한 내용은 [API를 사용하여 데이터 집합 만들기](../../catalog/api/create-dataset.md) 자습서를 참조하십시오.

**API 형식**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 만든 스트리밍 연결의 ID입니다. |

**요청**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**응답**

성공적인 응답은 HTTP 상태 207(Multi-status)을 반환합니다. 응답 본문 검토에서는 요청에서 실행된 각 메서드의 성공 또는 실패에 대해 자세히 설명합니다. 요청 메시지 배열의 각 요소에 대한 응답이 반환됩니다. 다음은 메시지 오류가 없는 성공적인 응답의 예입니다.

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

상태 코드에 대한 자세한 내용은 이 자습서의 부록에 있는 [응답 코드](#response-codes) 표를 참조하십시오.

## 실패한 메시지 식별

단일 메시지로 요청을 보내는 것과 비교하여 여러 메시지로 HTTP 요청을 보낼 때 고려해야 할 추가 요소는 다음과 같습니다. 데이터 전송 실패 시기, 전송 실패한 특정 메시지 및 검색 방법, 동일한 요청의 다른 메시지가 실패하면 성공하는 데이터에 발생하는 결과.

이 자습서를 진행하기 전에 먼저 [실패한 일괄 처리 검색](../quality/retrieve-failed-batches.md) 안내서를 검토하는 것이 좋습니다.

### 요청 페이로드에 유효하고 잘못된 메시지 보내기

다음 예에서는 배치에 유효한 메시지와 유효하지 않은 메시지가 포함된 경우 발생하는 결과를 보여 줍니다.

요청 페이로드는 XDM 스키마의 이벤트를 나타내는 JSON 개체의 배열입니다. 메시지를 성공적으로 확인하려면 다음 조건을 충족해야 합니다.
- 메시지 헤더의 `imsOrgId` 필드는 인렛 정의와 일치해야 합니다. 요청 페이로드에 `imsOrgId` 필드가 포함되지 않은 경우 [!DNL Data Collection Core Service](DCCS)이 필드를 자동으로 추가합니다.
- 메시지 헤더는 [!DNL Platform] UI에서 만든 기존 XDM 스키마를 참조해야 합니다.
- `datasetId` 필드는 [!DNL Platform]의 기존 데이터 집합을 참조해야 하며 해당 스키마는 요청 본문에 포함된 각 메시지 내의 `header` 개체에 제공된 스키마와 일치해야 합니다.

**API 형식**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 생성된 데이터 인렛의 ID입니다. |

**요청**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**응답**

응답 페이로드에는 각 메시지의 상태와 추적에 사용할 수 있는 `xactionId`의 GUID가 포함되어 있습니다.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

위의 예제 응답에는 이전 요청에 대한 오류 메시지가 표시됩니다. 이 응답을 이전의 유효한 응답과 비교하여 한 개의 메시지가 성공적으로 수집되고 세 개의 메시지가 실패하는 부분 성공으로 이어졌는지 확인할 수 있습니다. 두 응답 모두 &#39;207&#39; 상태 코드를 반환합니다. 상태 코드에 대한 자세한 내용은 이 자습서의 부록에 있는 [응답 코드](#response-codes) 표를 참조하십시오.

첫 번째 메시지가 [!DNL Platform](으)로 전송되었으며 다른 메시지의 결과에 영향을 받지 않습니다. 따라서 실패한 메시지를 다시 보내려고 할 때는 이 메시지를 다시 포함할 필요가 없습니다.

두 번째 메시지는 메시지 본문이 부족하여 실패했습니다. 컬렉션 요청에서는 메시지 요소에 유효한 머리글과 본문 섹션이 있을 것으로 예상합니다. 두 번째 메시지의 헤더 뒤에 다음 코드를 추가하면 요청이 수정되어 두 번째 메시지가 유효성 검사를 통과할 수 있습니다.

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

세 번째 메시지는 헤더에 잘못된 조직 ID가 사용되었기 때문에 실패했습니다. 조직은 게시하려는 {CONNECTION_ID}과(와) 일치해야 합니다. 사용 중인 스트리밍 연결과 일치하는 조직 ID를 확인하려면 [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)을(를) 사용하여 `GET inlet` 요청을 수행할 수 있습니다. 이전에 만든 스트리밍 연결을 검색하는 방법에 대한 예는 [스트리밍 연결 검색](./create-streaming-connection.md#get-data-collection-url)을 참조하십시오.

네 번째 메시지는 예상 XDM 스키마를 따르지 않아 실패했습니다. 요청의 헤더 및 본문에 포함된 `xdmSchema`이(가) `{DATASET_ID}`의 XDM 스키마와 일치하지 않습니다. 메시지 헤더와 본문에서 스키마를 수정하면 DCCS 유효성 검사를 통과하고 [!DNL Platform](으)로 성공적으로 전송될 수 있습니다. [!DNL Platform]에서 스트리밍 유효성 검사를 통과하려면 `{DATASET_ID}`의 XDM 스키마와 일치하도록 메시지 본문도 업데이트해야 합니다. Platform으로 성공적으로 스트리밍되는 메시지에 발생하는 사항에 대한 자세한 내용은 이 자습서의 [수집된 메시지 확인](#confirm-messages-ingested) 섹션을 참조하십시오.

### [!DNL Platform]에서 실패한 메시지 검색

실패한 메시지는 응답 배열의 오류 상태 코드로 식별됩니다.
잘못된 메시지는 `{DATASET_ID}`에서 지정한 데이터 집합 내의 &quot;오류&quot; 일괄 처리에 수집되어 저장됩니다.

실패한 일괄 처리 메시지 복구에 대한 자세한 내용은 [실패한 일괄 처리 검색](../quality/retrieve-failed-batches.md) 안내서를 참조하십시오.

## 수집된 메시지 확인

DCCS 유효성 검사를 통과한 메시지는 [!DNL Platform](으)로 스트리밍됩니다. [!DNL Platform]에서 일괄 처리 메시지는 [!DNL Data Lake](으)로 수집되기 전에 스트리밍 유효성 검사로 테스트됩니다. 성공 여부에 관계없이 일괄 처리의 상태가 `{DATASET_ID}`에서 지정한 데이터 집합 내에 나타납니다.

**[!UICONTROL 데이터 세트]** 탭으로 이동하여 스트리밍 중인 데이터 세트를 클릭하고 **[!UICONTROL 데이터 세트 활동]** 탭을 확인하여 [Experience Platform UI](https://platform.adobe.com)를 사용하여 [!DNL Platform]에 성공적으로 스트리밍된 일괄 처리 메시지의 상태를 볼 수 있습니다.

[!DNL Platform]에서 스트리밍 유효성 검사를 통과한 일괄 처리 메시지는 [!DNL Data Lake]에 수집됩니다. 그런 다음 메시지를 분석 또는 내보내기에 사용할 수 있습니다.

## 다음 단계

단일 요청으로 여러 메시지를 보내고 메시지가 대상 데이터 집합에 성공적으로 수집되는 시기를 확인하는 방법을 알았으므로 이제 [!DNL Platform](으)로 데이터 스트리밍을 시작할 수 있습니다. [!DNL Platform]에서 수집된 데이터를 쿼리하고 검색하는 방법에 대한 개요는 [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) 안내서를 참조하십시오.

## 부록

이 섹션에는 자습서에 대한 추가 정보가 포함되어 있습니다.

### 응답 코드

다음 표는 성공 및 실패 응답 메시지에서 반환된 상태 코드를 보여 줍니다.

| 상태 코드 | 설명 |
| :---: | --- |
| 207 | 전체 응답 상태 코드로 &#39;207&#39;이 사용되지만 수신자는 다중 상태 응답 본문의 내용을 참조하여 메서드 실행의 성공 또는 실패에 대한 자세한 내용을 확인해야 합니다. 응답 코드는 성공, 부분 성공 및 실패 상황에서도 사용됩니다. |
| 400 | 요청에 문제가 있습니다. 보다 구체적인 오류 메시지에 대해서는 응답 본문을 참조하십시오(예: 메시지 페이로드에 필수 필드가 누락되었거나 메시지에 알 수 없는 xdm 형식). |
| 401 | 승인되지 않음: 요청에 유효한 인증 헤더가 누락되었습니다. 인증이 활성화된 입력에만 반환됩니다. |
| 403 | 승인되지 않음: 입력한 인증 토큰이 잘못되었거나 만료되었습니다. 인증이 활성화된 입력에만 반환됩니다. |
| 413 | 페이로드가 너무 큼 - 총 페이로드 요청이 1MB보다 클 때 발생합니다. |
| 429 | 지정된 기간 내에 요청이 너무 많음. |
| 500 | 페이로드를 처리하는 중 오류가 발생했습니다. 보다 구체적인 오류 메시지에 대해서는 응답 본문을 참조하십시오(예: 메시지 페이로드 스키마가 지정되지 않았거나 [!DNL Platform]의 XDM 정의와 일치하지 않음). |
| 503 | 서비스를 현재 사용할 수 없습니다. 클라이언트는 지수 백오프 전략을 사용하여 최소 3번 다시 시도해야 합니다. |
