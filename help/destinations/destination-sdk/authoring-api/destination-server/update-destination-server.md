---
description: 이 페이지에서는 Adobe Experience Platform Destination SDK을 통해 기존 대상 서버 구성을 업데이트하는 데 사용되는 API 호출을 보여줍니다.
title: 대상 서버 구성 업데이트
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 12%

---


# 대상 서버 구성 업데이트

이 페이지에서는 기존 대상 서버 구성을 업데이트하는 데 사용할 수 있는 API 요청 및 페이로드를 예로 들 수 있습니다. `/authoring/destination-servers` API 엔드포인트.

>[!TIP]
>
>제품/공개 대상에 대한 모든 업데이트 작업은 를 사용한 후에만 표시됩니다 [API 게시](../../publishing-api/create-publishing-request.md) Adobe 검토를 위해 업데이트를 제출합니다.

이 종단점을 통해 구성할 수 있는 기능에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [Destination SDK으로 생성된 대상에 대한 서버 사양](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Destination SDK으로 생성된 대상에 대한 템플릿 사양](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [메시지 포맷](../../../destination-sdk/functionality/destination-server/message-format.md)
* [파일 형식 구성](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 서버 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 대상 서버 구성 업데이트 {#update}

을(를) 업데이트할 수 있습니다 [기존](create-destination-server.md) 대상 서버 구성 만들기 `PUT` 에 요청 `/authoring/destination-servers` 업데이트된 페이로드가 있는 종단점입니다.

>[!TIP]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

기존 대상 서버 구성 및 해당 구성 가져오기 `{INSTANCE_ID}`에 대한 자세한 내용은 [대상 서버 구성 검색](retrieve-destination-server.md).

**API 형식**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 대상 서버 구성의 ID입니다. 기존 대상 서버 구성 및 해당 구성 가져오기 `{INSTANCE_ID}`를 참조하십시오. [대상 서버 구성 검색](retrieve-destination-server.md). |

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 대상 서버 구성을 업데이트합니다.

아래의 각 탭을 선택하여 해당 페이로드를 확인합니다.

>[!BEGINTABS]

>[!TAB 실시간(스트리밍)]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | *필수 여부.* Adobe에만 표시되는 서버의 친숙한 이름을 나타냅니다. 파트너 또는 고객은 이 이름을 볼 수 없습니다. 예 `Moviestar destination server`. |
| `destinationServerType` | 문자열 | *필수 여부.* 을 로 설정합니다. `URL_BASED` 실시간(스트리밍) 대상 |
| `urlBasedDestination.url.templatingStrategy` | 문자열 | *필수 여부.* <ul><li>사용 `PEBBLE_V1` Adobe이 `value` 아래의 필드. 다음과 같은 종단점이 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 사용 `NONE` Adobe 측에 변환이 필요하지 않으면(예: 다음과 같은 엔드포인트가 있는 경우) `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 문자열 | *필수 여부.* Experience Platform이 연결해야 하는 API 엔드포인트의 주소를 입력합니다. |
| `httpTemplate.httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 옵션은 다음과 같습니다 `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `httpTemplate.requestBody.value` | 문자열 | *필수 여부.* 이 문자열은 Platform 고객의 데이터를 서비스에 필요한 형식으로 변환하는 문자 이스케이프 처리 버전입니다. <br> <ul><li> 템플릿을 작성하는 방법에 대한 자세한 내용은 [템플릿 섹션 사용](../../functionality/destination-server/message-format.md#using-templating). </li><li> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 단순 변환의 예는 [프로필 속성](../../functionality/destination-server/message-format.md#attributes) 변환. </li></ul> |
| `httpTemplate.contentType` | 문자열 | *필수 여부.* 서버가 허용하는 컨텐츠 유형입니다. 이 값은 `application/json`. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Amazon S3]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Amazon S3]으로 설정합니다. `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedS3Destination.bucket.value` | 문자열 | 의 이름 [!DNL Amazon S3] 이 대상에서 사용할 버킷입니다. |
| `fileBasedS3Destination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedS3Destination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 해당 없음 | 자세한 내용은 [파일 형식 구성](../../functionality/destination-server/file-formatting.md) 를 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB SFTP]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL SFTP] 대상, 다음 위치로 설정 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedSftpDestination.rootDirectory.value` | 문자열 | 대상 저장소의 루트 디렉토리입니다. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedSftpDestination.hostName.value` | 문자열 | 대상 스토리지의 호스트 이름입니다. |
| `port` | 정수 | SFTP 파일 서버 포트입니다. |
| `encryptionMode` | 문자열 | 파일 암호화를 사용할지 여부를 나타냅니다. 지원되는 값: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 해당 없음 | 자세한 내용은 [파일 형식 구성](../../functionality/destination-server/file-formatting.md) 를 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure Data Lake 저장소]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Azure Data Lake Storage] 대상, 다음 위치로 설정 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAdlsGen2Destination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 해당 없음 | 자세한 내용은 [파일 형식 구성](../../functionality/destination-server/file-formatting.md) 를 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure Blob 저장소]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Azure Blob Storage] 대상, 다음 위치로 설정 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAzureBlobDestination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAzureBlobDestination.container.value` | 문자열 | 의 이름 [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다. |
| `fileConfigurations` | 해당 없음 | 자세한 내용은 [파일 형식 구성](../../functionality/destination-server/file-formatting.md) 를 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Data Landing Zone] 대상, 다음 위치로 설정 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedDlzDestination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 해당 없음 | 자세한 내용은 [파일 형식 구성](../../functionality/destination-server/file-formatting.md) 를 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Google 클라우드 스토리지]

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Google Cloud Storage] 대상, 다음 위치로 설정 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 문자열 | 의 이름 [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷입니다. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 해당 없음 | 자세한 내용은 [파일 형식 구성](../../functionality/destination-server/file-formatting.md) 를 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 업데이트된 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!ENDTABS]

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 Destination SDK을 통해 대상 서버 구성을 업데이트하는 방법을 알 수 있습니다 `/authoring/destination-servers` API 엔드포인트.

이 종단점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 서버 구성 만들기](create-destination-server.md)
* [대상 서버 구성 검색](retrieve-destination-server.md)
* [대상 서버 구성 업데이트](update-destination-server.md)