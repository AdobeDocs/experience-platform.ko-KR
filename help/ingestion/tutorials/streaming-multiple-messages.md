---
keywords: Experience Platform;홈;인기 항목;스트리밍 수집;수집;여러 메시지 스트리밍;여러 메시지
solution: Experience Platform
title: 단일 HTTP 요청으로 여러 메시지 보내기
type: Tutorial
description: 이 문서에서는 스트리밍 수집을 사용하여 단일 HTTP 요청 내에서 Adobe Experience Platform에 여러 메시지를 전송하는 자습서를 제공합니다.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---

# 단일 HTTP 요청으로 여러 메시지 보내기

데이터를 Adobe Experience Platform으로 스트리밍할 때 많은 HTTP 호출을 수행하는 것은 비용이 많이 들 수 있습니다. 예를 들어, 1KB 페이로드를 사용하여 200개의 HTTP 요청을 만드는 대신 1KB의 메시지 200개를 1KB로 설정하고 200KB의 단일 페이로드를 사용하여 1개의 HTTP 요청을 만드는 것이 훨씬 효율적입니다. 올바르게 사용하는 경우 단일 요청 내에 여러 메시지를 그룹화하는 것은 전송되는 데이터를 최적화하는 좋은 방법입니다 [!DNL Experience Platform].

이 문서에서는 [!DNL Experience Platform] 스트리밍 수집을 사용하여 단일 HTTP 요청 내에서 전송됩니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform에 대한 작업 이해를 필요로 합니다 [!DNL Data Ingestion]. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

- [데이터 수집 개요](../home.md): 의 핵심 개념을 다룹니다. [!DNL Experience Platform Data Ingestion]: 수집 방법 및 data connectors.
- [스트리밍 수집 개요](../streaming-ingestion/overview.md): 스트리밍 연결, 데이터 세트, [!DNL XDM Individual Profile], 및 [!DNL XDM ExperienceEvent].

또한 이 자습서에서는 다음을 완료해야 합니다 [Adobe Experience Platform에 대한 인증](https://www.adobe.com/go/platform-api-authentication-en) 에 대한 호출을 성공적으로 수행하기 위한 자습서입니다. [!DNL Platform] API. 인증 자습서를 완료하면 이 자습서의 모든 API 호출에 필요한 인증 헤더 값을 제공합니다. 헤더는 다음과 같이 샘플 호출에 표시됩니다.

- 권한 부여: 베어러 `{ACCESS_TOKEN}`

모든 POST 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 스트리밍 연결 만들기

스트리밍 데이터를 시작하려면 먼저 스트리밍 연결을 만들어야 합니다 [!DNL Experience Platform]. 다음 문서를 참조하십시오. [스트리밍 연결 만들기](./create-streaming-connection.md) 스트리밍 연결을 만드는 방법에 대한 학습 안내서입니다.

스트리밍 연결을 등록한 후 데이터 생성자는 데이터를 플랫폼으로 스트리밍하는 데 사용할 수 있는 고유한 URL을 보유합니다.

## 데이터 세트로 스트리밍

다음 예는 단일 HTTP 요청 내에서 특정 데이터 세트에 여러 메시지를 전송하는 방법을 보여줍니다. 메시지 헤더에 데이터 세트 ID를 삽입하여 해당 메시지를 직접 수신하게 합니다.

기존 데이터 세트에 대한 ID를 [!DNL Platform] UI 또는 API에서 목록 작업 사용. 데이터 세트 ID는 [Experience Platform](https://platform.adobe.com) 다음과 같이 **[!UICONTROL 데이터 세트]** 탭에서 ID를 사용할 데이터 세트를 클릭하고 의 데이터 세트 ID 필드에서 문자열을 복사합니다 **[!UICONTROL 정보]** 탭. 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md) api를 사용하여 데이터 세트를 검색하는 방법에 대한 자세한 내용을 참조하십시오.

기존 데이터 세트를 사용하는 대신 새 데이터 세트를 만들 수 있습니다. 자세한 내용은 [api를 사용하여 데이터 세트 만들기](../../catalog/api/create-dataset.md) api를 사용하여 데이터 세트를 만드는 방법에 대한 자세한 내용은 자습서를 참조하십시오.

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

성공적인 응답은 HTTP 상태 207(다중 상태)을 반환합니다. 응답 본문을 검토하면 요청에서 실행된 각 메서드의 성공 또는 실패에 대한 자세한 정보를 제공합니다. 요청 메시지 배열의 각 요소에 대해 응답이 반환됩니다. 다음은 메시지 오류가 없는 성공적인 응답의 예입니다.

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

상태 코드에 대한 자세한 내용은 [응답 코드](#response-codes) 표( 이 자습서 부록)에 나와 있습니다.

## 실패한 메시지 식별

단일 메시지로 요청을 보내는 것과 비교하여 여러 메시지가 있는 HTTP 요청을 보낼 때 고려해야 할 추가 요소가 있습니다. 예: 데이터를 보내지 못한 시기, 보내지 못한 특정 메시지 및 메시지 검색 방법을 식별하는 방법, 동일한 요청의 다른 메시지가 실패할 때 성공한 데이터에 어떻게 발생합니까?

이 자습서를 계속 진행하기 전에 먼저 [실패한 배치 검색](../quality/retrieve-failed-batches.md) 안내서.

### 유효한 잘못된 메시지와 함께 요청 페이로드 보내기

다음 예는 배치에 유효하고 잘못된 메시지가 포함되어 있을 때 발생하는 상황을 보여줍니다.

요청 페이로드는 XDM 스키마에서 이벤트를 나타내는 JSON 개체의 배열입니다. 메시지를 성공적으로 유효성 검사하려면 다음 조건을 충족해야 합니다.
- 다음 `imsOrgId` 메시지 헤더의 필드는 입력 정의와 일치해야 합니다. 요청 페이로드에 가 포함되지 않은 경우 `imsOrgId` 필드, [!DNL Data Collection Core Service] (DCCS)에서 필드를 자동으로 추가합니다.
- 메시지 헤더는 [!DNL Platform] UI.
- 다음 `datasetId` 필드의 기존 데이터 세트를 참조해야 함 [!DNL Platform]및 해당 스키마는 `header` 요청 본문에 포함된 각 메시지 내의 개체

**API 형식**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 생성된 데이터 입구의 ID입니다. |

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

응답 페이로드에는 각 메시지에 대한 상태와 `xactionId` 추적에 사용할 수 있습니다.

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

위의 예제 응답에는 이전 요청에 대한 오류 메시지가 표시됩니다. 이 응답을 이전 유효한 응답과 비교함으로써, 한 메시지를 성공적으로 수집하여 세 개의 메시지를 오류로 인해 요청이 부분 성공임을 확인할 수 있습니다. 두 응답 모두 &#39;207&#39; 상태 코드를 반환합니다. 상태 코드에 대한 자세한 내용은 [응답 코드](#response-codes) 표( 이 자습서 부록)에 나와 있습니다.

첫 번째 메시지를 [!DNL Platform] 및 은 다른 메시지의 결과에 영향을 받지 않습니다. 따라서 실패한 메시지를 다시 전송하려고 할 때 이 메시지를 다시 포함할 필요가 없습니다.

두 번째 메시지는 메시지 본문이 없어서 실패했습니다. 컬렉션 요청에는 메시지 요소에 유효한 헤더 및 본문 섹션이 있어야 합니다. 두 번째 메시지의 헤더 뒤에 다음 코드를 추가하면 요청이 수정되고, 두 번째 메시지가 유효성 검사를 전달할 수 있습니다.

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

헤더에서 사용 중인 잘못된 조직 ID로 인해 세 번째 메시지가 실패했습니다. 조직은 게시하려는 {CONNECTION_ID}와 일치해야 합니다. 사용 중인 스트리밍 연결과 일치하는 조직 ID를 확인하려면 다음을 수행할 수 있습니다 `GET inlet` 를 사용하여 요청 [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). 자세한 내용은 [스트리밍 연결 검색](./create-streaming-connection.md#get-data-collection-url) 앞에서 만든 스트리밍 연결을 검색하는 방법의 예입니다.

네 번째 메시지가 예상 XDM 스키마를 따르지 않았으므로 실패했습니다. 다음 `xdmSchema` 요청의 헤더 및 본문에 포함된 가 `{DATASET_ID}`. 메시지 헤더 및 본문에서 스키마를 수정하면 DCCS 유효성 검사를 통과하고 를 성공적으로 보낼 수 있습니다 [!DNL Platform]. 메시지 본문도 페이지의 XDM 스키마와 일치하도록 업데이트해야 합니다 `{DATASET_ID}` 스트리밍 유효성 검사를 [!DNL Platform]. Platform으로 성공적으로 스트리밍되는 메시지에 대한 자세한 내용은 [수집된 메시지 확인](#confirm-messages-ingested) 이 자습서의 섹션.

### 에서 실패한 메시지 검색 [!DNL Platform]

실패한 메시지는 응답 배열의 오류 상태 코드로 식별됩니다.
잘못된 메시지가 수집되어 지정된 데이터 세트 내의 &quot;오류&quot; 배치에 저장됩니다 `{DATASET_ID}`.

다음 문서를 참조하십시오. [실패한 배치 검색](../quality/retrieve-failed-batches.md) 실패한 배치 메시지 복구에 대한 자세한 내용은 안내서 를 참조하십시오.

## 수집된 메시지 확인

DCCS 유효성 검사를 전달하는 메시지는 [!DNL Platform]. 설정 [!DNL Platform]로 일괄 처리 메시지를 수집하기 전에 스트리밍 유효성 검사로 테스트됩니다 [!DNL Data Lake]. 성공 여부에 관계없이 배치의 상태는 로 지정된 데이터 세트에 나타납니다 `{DATASET_ID}`.

에 성공적으로 스트리밍된 배치 메시지의 상태를 볼 수 있습니다 [!DNL Platform] 사용 [Experience Platform UI](https://platform.adobe.com) 다음과 같이 **[!UICONTROL 데이터 세트]** 탭에서 스트리밍할 데이터 세트를 클릭하고 **[!UICONTROL 데이터 집합 활동]** 탭.

스트리밍 유효성 검사를 전달하는 메시지 일괄 처리 [!DNL Platform] 다음 항목에 [!DNL Data Lake]. 그런 다음 메시지를 분석하거나 내보낼 수 있습니다.

## 다음 단계

이제 단일 요청으로 여러 메시지를 보내고 메시지가 타겟 데이터 세트에 성공적으로 수집되는 시기를 확인하는 방법을 알므로 자신의 데이터 스트리밍을 시작할 수 있습니다 [!DNL Platform]. 수집된 데이터를 쿼리 및 검색하는 방법에 대한 개요입니다 [!DNL Platform]를 참조하고 [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) 안내서.

## 부록

이 섹션에는 자습서에 대한 보충 정보가 포함되어 있습니다.

### 응답 코드

다음 표는 성공 및 실패한 응답 메시지에 의해 반환된 상태 코드를 보여줍니다.

| 상태 코드 | 설명 |
| :---: | --- |
| 207 | &#39;207&#39;이 전체 응답 상태 코드로 사용되지만, 수신자는 메서드 실행의 성공 또는 실패에 대한 자세한 내용을 보려면 다중 상태 응답 본문의 콘텐츠를 참조해야 합니다. 응답 코드는 성공, 부분 성공 및 실패 상황에도 사용됩니다. |
| 400 | 요청에 문제가 있습니다. 보다 구체적인 오류 메시지에 대해서는 응답 본문을 참조하십시오(예: 메시지 페이로드에 필수 필드가 없거나 메시지가 알 수 없는 xdm 형식). |
| 401 | 권한 없음: 요청에 유효한 인증 헤더가 없습니다. 이 값은 인증이 활성화된 inlet에만 반환됩니다. |
| 403 | 권한 없음: 제공된 인증 토큰이 잘못되었거나 만료되었습니다. 이 값은 인증이 활성화된 inlet에만 반환됩니다. |
| 413 | 페이로드가 너무 큼 - 총 페이로드 요청이 1MB보다 클 때 발생합니다. |
| 429 | 지정된 기간 내에 요청이 너무 많습니다. |
| 500 | 페이로드를 처리하는 동안 오류가 발생했습니다. 보다 구체적인 오류 메시지에 대해서는 응답 본문을 참조하십시오(예: 메시지 페이로드 스키마가 지정되지 않았거나 의 XDM 정의와 일치하지 않음) [!DNL Platform]). |
| 503 | 현재 서비스를 사용할 수 없습니다. 클라이언트는 지수 백오프 전략을 사용하여 최소 3번 다시 시도해야 합니다. |
