---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 대상 서버를 만드는 데 사용되는 API 호출을 보여 줍니다.
title: 대상 서버 구성 만들기
source-git-commit: cadffd60093eef9fb2dcf4562b1fd7611e61da94
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 9%

---


# 대상 서버 구성 만들기

대상 서버를 만드는 것은 Destination SDK으로 고유한 대상을 만드는 첫 번째 단계입니다. 대상 서버에는 [server](../../functionality/destination-server/server-specs.md) 및 [템플릿](../../functionality/destination-server/templating-specs.md) 사양, [메시지 포맷](../../functionality/destination-server/message-format.md)및 [파일 서식](../../functionality/destination-server/file-formatting.md) 옵션(파일 기반 대상).

이 페이지는 를 사용하여 고유한 대상 서버를 만드는 데 사용할 수 있는 API 요청 및 페이로드를 예시합니다. `/authoring/destination-servers` API 엔드포인트.

이 끝점을 통해 구성할 수 있는 기능에 대한 자세한 설명은 다음 문서를 참조하십시오.

* [Destination SDK으로 생성된 대상의 서버 사양](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Destination SDK으로 만든 대상에 대한 템플릿 사양](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [메시지 포맷](../../../destination-sdk/functionality/destination-server/message-format.md)
* [파일 서식 구성](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 서버 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상 서버 구성 만들기 {#create}

다음을 수행하여 새 대상 서버 구성을 만들 수 있습니다. `POST` 에 대한 요청 `/authoring/destination-servers` 엔드포인트.

>[!TIP]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API 형식**

```http
POST /authoring/destination-servers
```

만드는 대상 유형에 따라 약간 다른 유형의 대상 서버를 구성해야 합니다.

### 정적 스키마 대상 서버 만들기 {#static-destination-servers}

을 사용하는 대상에 대한 대상 서버의 예는 아래 탭에서 을 참조하십시오. [정적 스키마](../../functionality/destination-configuration/schema-configuration.md#attributes-schema).

아래의 샘플 페이로드에는 각 대상 서버 유형에서 지원하는 모든 매개 변수가 포함되어 있습니다. 요청에 모든 매개 변수를 포함할 필요는 없습니다. 페이로드는 필요에 따라 사용자 정의할 수 있습니다.

아래의 각 탭을 선택하여 해당 API 요청을 확인합니다.

>[!BEGINTABS]

>[!TAB 실시간(스트리밍)]

**실시간(스트리밍) 대상 서버 만들기**

실시간(스트리밍) API 기반 통합을 구성할 때 아래에 표시된 것과 유사한 실시간(스트리밍) 대상 서버를 만들어야 합니다.

+++요청

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

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | *필수 여부.* Adobe 시에만 표시되는 서버의 친숙한 이름을 나타냅니다. 이 이름은 파트너나 고객에게 표시되지 않습니다. 예 `Moviestar destination server`. |
| `destinationServerType` | 문자열 | *필수 여부.* 다음으로 설정 `URL_BASED` 실시간(스트리밍) 대상의 경우. |
| `urlBasedDestination.url.templatingStrategy` | 문자열 | *필수 여부.* <ul><li>사용 `PEBBLE_V1` Adobe에서 URL을 `value` 아래 필드. 다음과 같은 엔드포인트가 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items`, 여기서 `region` 부품은 고객마다 다를 수 있습니다. 이 경우 를 구성해야 합니다. `region` as a [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 다음에서 [대상 구성](../destination-configuration/create-destination-configuration.md. </li><li> 사용 `NONE` Adobe 측에 변환이 필요하지 않은 경우, 예를 들어 다음과 같은 엔드포인트가 있는 경우: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 문자열 | *필수 여부.* Experience Platform이 연결해야 하는 API 끝점의 주소를 입력합니다. |
| `httpTemplate.httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 옵션은 다음과 같습니다 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `httpTemplate.requestBody.value` | 문자열 | *필수 여부.* 이 문자열은 Platform 고객의 데이터를 서비스가 기대하는 형식으로 변환하는 문자 이스케이프 처리된 버전입니다. <br> <ul><li> 템플릿 작성 방법에 대한 자세한 내용은 [템플릿 섹션 사용](../../functionality/destination-server/message-format.md#using-templating). </li><li> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 간단한 변환의 예를 보려면 [프로필 속성](../../functionality/destination-server/message-format.md#attributes) 변환. </li></ul> |
| `httpTemplate.contentType` | 문자열 | *필수 여부.* 서버가 허용하는 콘텐츠 유형입니다. 이 값은 다음과 같을 수 있습니다. `application/json`. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Amazon S3]

**Amazon S3 대상 서버 만들기**

다음을 만들어야 합니다. [!DNL Amazon S3] 대상 서버 파일 기반 구성 시 아래에 표시된 서버와 유사 [!DNL Amazon S3] 대상.

+++요청

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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Amazon S3], 다음으로 설정 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedS3Destination.bucket.value` | 문자열 | 의 이름입니다. [!DNL Amazon S3] 이 대상에서 사용할 버킷. |
| `fileBasedS3Destination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedS3Destination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | N/A | 다음을 참조하십시오 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 이러한 설정을 구성하는 방법에 대한 자세한 내용은 을 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB SFTP]

**만들기 [!DNL SFTP] 대상 서버**

다음을 만들어야 합니다. [!DNL SFTP] 대상 서버 파일 기반 구성 시 아래에 표시된 서버와 유사 [!DNL SFTP] 대상.

+++요청

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
   "fileBasedSFTPDestination":{
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
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL SFTP] 대상, 다음으로 설정 `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedSFTPDestination.rootDirectory.value` | 문자열 | 대상 스토리지의 루트 디렉토리입니다. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedSFTPDestination.hostName.value` | 문자열 | 대상 스토리지의 호스트 이름입니다. |
| `port` | 정수 | SFTP 파일 서버 포트입니다. |
| `encryptionMode` | 문자열 | 파일 암호화를 사용할지 여부를 나타냅니다. 지원되는 값: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | N/A | 다음을 참조하십시오 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 이러한 설정을 구성하는 방법에 대한 자세한 내용은 을 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure 데이터 레이크 스토리지]

**만들기 [!DNL Azure Data Lake Storage] 대상 서버**

다음을 만들어야 합니다. [!DNL Azure Data Lake Storage] 대상 서버 파일 기반 구성 시 아래에 표시된 서버와 유사 [!DNL Azure Data Lake Storage] 대상.

+++요청

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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Azure Data Lake Storage] 대상, 다음으로 설정 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAdlsGen2Destination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | N/A | 다음을 참조하십시오 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 이러한 설정을 구성하는 방법에 대한 자세한 내용은 을 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure Blob 저장소]

**만들기 [!DNL Azure Blob Storage] 대상 서버**

다음을 만들어야 합니다. [!DNL Azure Blob Storage] 대상 서버 파일 기반 구성 시 아래에 표시된 서버와 유사 [!DNL Azure Blob Storage] 대상.

+++요청

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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Azure Blob Storage] 대상, 다음으로 설정 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAzureBlobDestination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAzureBlobDestination.container.value` | 문자열 | 의 이름입니다. [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다. |
| `fileConfigurations` | N/A | 다음을 참조하십시오 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 이러한 설정을 구성하는 방법에 대한 자세한 내용은 을 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

**만들기 [!DNL Data Landing Zone (DLZ)] 대상 서버**

다음을 만들어야 합니다. [!DNL Data Landing Zone (DLZ)] 대상 서버 파일 기반 구성 시 아래에 표시된 서버와 유사 [!DNL Data Landing Zone (DLZ)] 대상.

+++요청

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

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Data Landing Zone] 대상, 다음으로 설정 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedDlzDestination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | N/A | 다음을 참조하십시오 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 이러한 설정을 구성하는 방법에 대한 자세한 내용은 을 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Google 클라우드 스토리지]

**만들기 [!DNL Google Cloud Storage] 대상 서버**

다음을 만들어야 합니다. [!DNL Google Cloud Storage] 대상 서버 파일 기반 구성 시 아래에 표시된 서버와 유사 [!DNL Google Cloud Storage] 대상.

+++요청

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Google Cloud Storage] 대상, 다음으로 설정 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 문자열 | 의 이름입니다. [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | N/A | 다음을 참조하십시오 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 이러한 설정을 구성하는 방법에 대한 자세한 내용은 을 참조하십시오. |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!ENDTABS]

### 동적 스키마 대상 서버 만들기 {#dynamic-schema-servers}

동적 스키마를 사용하면 지원되는 타겟 속성을 동적으로 검색하고 고유한 API를 기반으로 스키마를 생성할 수 있습니다. 스키마를 구성하려면 먼저 동적 스키마에 대한 대상 서버를 구성해야 합니다.

을 사용하는 대상에 대한 대상 서버의 예는 아래 탭에서 을 참조하십시오 [동적 스키마](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

아래 샘플 페이로드에는 동적 스키마 서버에 필요한 모든 매개 변수가 포함되어 있습니다.

>[!BEGINTABS]

>[!TAB 동적 스키마 서버]

**동적 스키마 서버 만들기**

고유한 API 끝점에서 프로필 스키마를 검색하는 대상을 구성할 때 아래에 표시된 것과 유사한 동적 스키마 서버를 만들어야 합니다. 정적 스키마와 달리 동적 스키마는 `profileFields` 배열입니다. 대신 동적 스키마는 스키마 구성을 검색하는 위치에서 자체 API에 연결되는 동적 스키마 서버를 사용합니다.

+++요청

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | *필수 여부.* Adobe 시에만 표시되는 동적 스키마 서버의 친숙한 이름을 나타냅니다. |
| `destinationServerType` | 문자열 | *필수 여부.* 다음으로 설정 `URL_BASED` 동적 스키마 서버용. |
| `urlBasedDestination.url.templatingStrategy` | 문자열 | *필수 여부.* <ul><li>사용 `PEBBLE_V1` Adobe에서 URL을 `value` 아래 필드. 다음과 같은 엔드포인트가 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 사용 `NONE` Adobe 측에 변환이 필요하지 않은 경우, 예를 들어 다음과 같은 엔드포인트가 있는 경우: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 문자열 | *필수 여부.* 활성화 워크플로의 매핑 단계에서 Experience Platform이 연결할 API 끝점의 주소를 입력하고 스키마 필드를 검색하여 대상 필드로 채웁니다. |
| `httpTemplate.httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 동적 스키마 서버의 경우 다음을 사용합니다. `GET`. |
| `responseFields.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `responseFields.value` | 문자열 | *필수 여부.* 이 문자열은 파트너 API에서 받은 응답을 Platform UI에 표시되는 파트너 스키마로 변환하는 문자 이스케이프 변환 템플릿입니다. <br> <ul><li> 템플릿 작성 방법에 대한 자세한 내용은 [템플릿 섹션 사용](../../functionality/destination-server/message-format.md#using-templating). </li><li> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 간단한 변환의 예를 보려면 [프로필 속성](../../functionality/destination-server/message-format.md#attributes) 변환. </li></ul> |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++


>[!ENDTABS]


### 동적 드롭다운 대상 서버 만들기 {#dynamic-dropdown-servers}

사용 [동적 드롭다운](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) 를 사용하여 고유한 API를 기반으로 드롭다운 고객 데이터 필드를 동적으로 검색하고 채울 수 있습니다. 예를 들어 대상 연결에 사용할 기존 사용자 계정 목록을 검색할 수 있습니다.

동적 드롭다운 고객 데이터 필드를 구성하려면 먼저 동적 드롭다운에 대한 대상 서버를 구성해야 합니다.

API에서 드롭다운 선택기에 표시할 값을 동적으로 검색하는 데 사용되는 대상 서버의 예 아래 탭에서 를 참조하십시오.

아래 샘플 페이로드에는 동적 스키마 서버에 필요한 모든 매개 변수가 포함되어 있습니다.

>[!BEGINTABS]

>[!TAB 동적 드롭다운 서버]

**동적 드롭다운 서버 만들기**

고유한 API 끝점에서 드롭다운 고객 데이터 필드의 값을 검색하는 대상을 구성할 때 아래에 표시된 것과 유사한 동적 드롭다운 서버를 만들어야 합니다.

+++요청

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `name` | 문자열 | *필수 여부.* 동적 드롭다운 서버의 친숙한 이름을 나타내며 Adobe에만 표시됩니다. |
| `destinationServerType` | 문자열 | *필수 여부.* 다음으로 설정 `URL_BASED` 동적 드롭다운 서버. |
| `urlBasedDestination.url.templatingStrategy` | 문자열 | *필수 여부.* <ul><li>사용 `PEBBLE_V1` Adobe에서 URL을 `value` 아래 필드. 다음과 같은 엔드포인트가 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 사용 `NONE` Adobe 측에 변환이 필요하지 않은 경우, 예를 들어 다음과 같은 엔드포인트가 있는 경우: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 문자열 | *필수 여부.* Experience Platform이 연결해야 하는 API 끝점의 주소를 입력하고 드롭다운 값을 검색합니다. |
| `httpTemplate.httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 동적 드롭다운 서버의 경우 다음을 사용합니다. `GET`. |
| `httpTemplate.headers` | 오브젝트 | *Optiona.l* 동적 드롭다운 서버에 연결하는 데 필요한 모든 헤더를 포함합니다. |
| `responseFields.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `responseFields.value` | 문자열 | *필수 여부.* 이 문자열은 API에서 받은 응답을 Platform UI에 표시될 값으로 변환하는 문자 이스케이프 변환 템플릿입니다. <br> <ul><li> 템플릿 작성 방법에 대한 자세한 내용은 [템플릿 섹션 사용](../../functionality/destination-server/message-format.md#using-templating). </li><li> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 새로 만든 대상 서버 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!ENDTABS]

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 Destination SDK을 통해 새 대상 서버를 만드는 방법을 알 수 있습니다 `/authoring/destination-servers` API 엔드포인트.

이 끝점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 서버 구성 검색](retrieve-destination-server.md)
* [대상 서버 구성 업데이트](update-destination-server.md)
* [대상 서버 구성 삭제](delete-destination-server.md)

이 끝점이 대상 작성 프로세스에 맞는 위치를 이해하려면 다음 문서를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)