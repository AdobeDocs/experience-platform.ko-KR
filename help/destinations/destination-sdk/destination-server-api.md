---
description: 이 페이지에서는 "/authoring/destination-servers" API 끝점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. 대상의 서버 및 템플릿 사양은 공통 끝점 "/authoring/destination-servers"를 통해 Adobe Experience Platform Destination SDK에서 구성할 수 있습니다.
title: 대상 서버 끝점 API 작업
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 3%

---

# 대상 서버 끝점 API 작업

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

이 페이지에서는 다음을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/destination-servers` API 엔드포인트. 대상의 서버 및 템플릿 사양은 공통 끝점을 통해 Adobe Experience Platform Destination SDK에서 구성할 수 있습니다 `/authoring/destination-servers`. 이 종단점에서 제공하는 기능에 대한 설명은 다음을 참조하십시오. [서버 및 템플릿 사양](./server-and-template-configuration.md).

## 대상 서버 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 스트리밍 대상 서버에 대한 구성 만들기 {#create}

에 POST 요청을 하여 스트리밍 대상에 대한 새 대상 서버 구성을 만들 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destination-servers` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 매개 변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | *필수 여부.* Adobe 시에만 표시되는 서버의 친숙한 이름을 나타냅니다. 이 이름은 파트너나 고객에게 표시되지 않습니다. 예 `Moviestar destination server`. |
| `destinationServerType` | 문자열 | *필수 여부.* 다음으로 설정 `URL_BASED` 스트리밍 대상용입니다. |
| `urlBasedDestination.url.templatingStrategy` | 문자열 | *필수 여부.* <ul><li>사용 `PEBBLE_V1` Adobe에서 URL을 `value` 아래 필드. 다음과 같은 엔드포인트가 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 사용 `NONE` Adobe 측에 변환이 필요하지 않은 경우, 예를 들어 다음과 같은 엔드포인트가 있는 경우: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 문자열 | *필수 여부.* Experience Platform이 연결해야 하는 API 끝점의 주소를 입력합니다. |
| `httpTemplate.httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 옵션은 다음과 같습니다 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `httpTemplate.requestBody.value` | 문자열 | *필수 여부.* 이 문자열은 Platform 고객의 데이터를 서비스가 기대하는 형식으로 변환하는 문자 이스케이프 처리된 버전입니다. <br> <ul><li> 템플릿 작성 방법에 대한 자세한 내용은 [템플릿 섹션 사용](./message-format.md#using-templating). </li><li> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 간단한 변환의 예를 보려면 [프로필 속성](./message-format.md#attributes) 변환. </li></ul> |
| `httpTemplate.contentType` | 문자열 | *필수 여부.* 서버가 허용하는 콘텐츠 유형입니다. 이 값은 다음과 같을 수 있습니다. `application/json`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 파일 기반 대상 서버에 대한 구성 만들기 {#create-file-based}

### SFTP 대상 서버 예제 구성 {#sftp-server-sample}

+++샘플 보기 [!DNL SFTP] 대상 서버 구성

에 POST 요청을 하여 새 SFTP 대상 서버 구성을 만들 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destination-servers` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.


```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**응답**

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.
+++

### [!DNL Amazon S3] 대상 서버 예제 구성 {#s3-server-sample}

+++샘플 보기 [!DNL Amazon S3] 대상 서버 구성

에 POST 요청을 하여 새 Amazon S3 대상 서버 구성을 만들 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destination-servers` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**응답**

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.
+++

### [!DNL Azure Blob] 대상 서버 예제 구성 {#blob-server-sample}

+++샘플 보기 [!DNL Azure Blob] 대상 서버 구성

에 POST 요청을 하여 새 Azure Blob 대상 서버 구성을 만들 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destination-servers` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**응답**

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.
+++

### [!DNL Azure Data Lake Storage] 대상 서버 예제 구성 {#adls-server-sample}

+++샘플 보기 [!DNL Azure Data Lake Storage (ADLS)] 대상 서버 구성

에 POST 요청을 하여 새 ADLS 대상 서버 구성을 만들 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destination-servers` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**응답**

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.
+++

### [!DNL Data Landing Zone] (DLZ) 대상 서버 예제 구성 {#dlz-server-sample}

+++샘플 보기 [!DNL Data Landing Zone (DLZ)] 대상 서버 구성

[!DNL Data Landing Zone] ([!DNL DLZ])은 입니다. [!DNL Azure Blob] Adobe Experience Platform에서 프로비저닝한 스토리지 인터페이스로, 파일을 플랫폼으로 가져올 수 있는 안전한 클라우드 기반 파일 스토리지 시설에 액세스할 수 있습니다.

에 POST 요청을 하여 새 DLZ 대상 서버 구성을 만들 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
POST /authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다. 아래 페이로드에는 이 허용하는 모든 매개 변수가 포함되어 있습니다. `/authoring/destination-servers` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**응답**

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.
+++

## 대상 서버 구성 나열 {#retrieve-list}

에 GET 요청을 하여 IMS 조직에 대한 모든 대상 서버 구성 목록을 검색할 수 있습니다. `/authoring/destination-servers` 엔드포인트.

**API 형식**

```http
GET /authoring/destination-servers
```

**요청**

다음 요청은 IMS 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 대상 서버 구성 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 IMS 조직 ID와 샌드박스 이름을 기반으로 액세스 권한이 있는 대상 서버 구성 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `instanceId` 는 하나의 대상 서버에 대한 템플릿에 해당합니다. 응답은 간결성을 위해 잘립니다.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## 기존 대상 서버 구성 업데이트 {#update}

에 PUT 요청을 하여 기존 대상 서버 구성을 업데이트할 수 있습니다. `/authoring/destination-servers` 업데이트하려는 대상 서버 구성의 인스턴스 ID를 제공하는 종단점입니다. 호출 본문에서 업데이트된 대상 서버 구성을 제공합니다.

**API 형식**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 대상 서버 구성의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 대상 서버 구성을 업데이트합니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## 특정 대상 서버 구성 검색 {#get}

에 GET 요청을 하여 특정 대상 서버 구성에 대한 자세한 정보를 검색할 수 있습니다. `/authoring/destination-servers` 업데이트하려는 대상 서버 구성의 인스턴스 ID를 제공하는 종단점입니다.

**API 형식**

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 대상 서버 구성의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 대상 서버 구성에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## 특정 대상 서버 구성 삭제 {#delete}

에 DELETE 요청을 하여 지정된 대상 서버 구성을 삭제할 수 있습니다. `/authoring/destination-servers` 엔드포인트 및 요청 경로에 삭제할 대상 서버 구성의 ID 제공

**API 형식**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `id` 삭제할 대상 서버 구성의 일부입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이 문서를 읽고 나면 이제 대상 서버를 구성하고 `/authoring/destination-servers` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](./configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.
