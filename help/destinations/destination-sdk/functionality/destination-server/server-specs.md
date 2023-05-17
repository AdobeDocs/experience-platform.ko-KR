---
description: '''/authoring/destination-servers'' 종단점을 통해 Adobe Experience Platform Destination SDK에서 대상 서버 사양을 구성하는 방법을 알아봅니다.'
title: Destination SDK으로 생성된 대상에 대한 서버 사양
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# Destination SDK으로 생성된 대상에 대한 서버 사양

대상 서버 사양은 Adobe Experience Platform에서 데이터를 받을 대상 플랫폼의 유형, 플랫폼과 대상 간의 통신 매개 변수를 정의합니다. 예:

* A [스트리밍](#streaming-example) 대상 서버 사양은 플랫폼에서 HTTP 메시지를 받을 HTTP 서버 끝점을 정의합니다. 엔드포인트에 대한 HTTP 호출 형식 지정 방법을 구성하려면 다음을 참조하십시오 [템플릿 사양](templating-specs.md) 페이지.
* An [Amazon S3](#s3-example) 대상 서버 사양은 [!DNL S3] Platform이 파일을 내보낼 버킷 이름 및 경로입니다.
* An [SFTP](#sftp-example) 대상 서버 사양은 Platform에서 파일을 내보내는 SFTP 서버의 호스트 이름, 루트 디렉토리, 통신 포트 및 암호화 유형을 정의합니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서나 다음 대상 구성 개요 페이지를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

를 통해 대상 서버 사양을 구성할 수 있습니다 `/authoring/destination-servers` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 서버 구성 만들기](../../authoring-api/destination-server/create-destination-server.md)
* [대상 서버 구성 업데이트](../../authoring-api/destination-server/update-destination-server.md)

이 페이지에는 모든 구성 매개 변수와 함께 Destination SDK이 지원하는 모든 대상 서버 유형이 표시됩니다. 대상을 만들 때 매개 변수 값을 직접 바꿉니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 예 |

When [만들기](../../authoring-api/destination-server/create-destination-server.md) 또는 [업데이트](../../authoring-api/destination-server/update-destination-server.md) 대상 서버에서 이 페이지에 설명된 서버 유형 구성 중 하나를 사용합니다. 통합 요구 사항에 따라 이러한 예제의 샘플 매개 변수 값을 고유한 값으로 바꿔야 합니다.

## 하드코딩과 템플릿 필드 {#templatized-fields}

Destination SDK을 통해 대상 서버를 생성할 때 구성 매개 변수 값을 구성에 하드 코딩하거나 템플릿 필드를 사용하여 정의할 수 있습니다. 템플릿 필드를 사용하면 플랫폼 UI에서 사용자가 제공한 값을 읽을 수 있습니다.

대상 서버 매개 변수에는 두 개의 구성 가능한 필드가 있습니다. 이러한 옵션은 하드 코딩된 값을 사용하는지 또는 템플릿 값을 사용하는지를 나타냅니다.

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `templatingStrategy` | 문자열 | *필수 여부.* 를 통해 하드 코딩된 값이 제공되는지 여부를 정의합니다 `value` 필드 또는 UI의 사용자 구성 가능한 값입니다. 지원되는 값: <ul><li>`NONE`: 를 통해 매개 변수 값을 하드 코딩할 때 이 값을 사용합니다 `value` 매개 변수(다음 행 참조). 예:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: 사용자가 UI에서 매개 변수 값을 제공하려면 이 값을 사용하십시오. 예: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | 문자열 | *필수 여부*. 매개 변수 값을 정의합니다. 지원되는 값 유형: <ul><li>**하드 코딩된 값**: 하드 코딩된 값(예: `"value": "my-storage-bucket"`) 사용자가 UI에 매개 변수 값을 입력할 필요가 없는 경우. 값을 하드 코딩할 때 `templatingStrategy` 는 항상 로 설정되어야 합니다. `NONE`.</li><li>**템플화된 가치**: 템플릿 값을 사용합니다(예: `"value": "{{customerData.bucket}}"`)을 사용하십시오. 템플릿 값을 사용할 때 `templatingStrategy` 는 항상 로 설정되어야 합니다. `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### 하드 코딩과 템플릿 필드를 사용해야 하는 경우

하드 코딩된 필드와 템플릿 필드는 모두 Destination SDK에서 자신이 생성하는 통합 유형에 따라 고유한 사용 방법이 있습니다.

**사용자 입력 없이 대상에 연결**

사용자가 [대상에 연결](../../../ui/connect-destination.md) platform UI에서 대상 연결 프로세스를 입력하지 않고 처리할 수 있습니다.

이렇게 하려면 서버 사양에서 대상 플랫폼 연결 매개 변수를 하드 코딩할 수 있습니다. 대상 서버 구성에서 하드 코딩된 매개 변수 값을 사용하는 경우 Adobe Experience Platform과 대상 플랫폼 간의 연결은 사용자의 입력 없이 처리됩니다.

아래 예에서는 파트너가 `path.value` 하드코딩되는 필드.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

따라서 사용자가 [대상 연결 자습서](../../../ui/connect-destination.md)로 설정되면 방문자에게 표시되지 않습니다 [인증 단계](../../../ui/connect-destination.md#authenticate). 대신, 인증은 아래 이미지와 같이 Platform에서 처리됩니다.

![플랫폼과 DLZ 대상 간의 인증 화면을 보여주는 UI 이미지입니다.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**사용자 입력을 사용하여 대상에 연결**

API 종단점 선택 또는 필드 값 제공과 같이 플랫폼 UI의 특정 사용자 입력에 따라 플랫폼과 대상 간의 연결을 설정해야 하는 경우 서버 사양의 템플릿 필드를 사용하여 사용자 입력을 읽고 대상 플랫폼에 연결할 수 있습니다.

아래 예에서는 파트너가 [실시간(스트리밍)](#streaming-example) 통합 및 `url.value` 필드는 템플릿 매개 변수를 사용합니다 `{{customerData.region}}` 사용자 입력에 따라 API 엔드포인트의 일부를 개인화합니다.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

사용자에게 플랫폼 UI에서 값을 선택하는 옵션을 제공하려면 `region` 매개 변수도 [대상 구성](../../authoring-api/destination-configuration/create-destination-configuration.md) 아래와 같이 고객 데이터 필드로 사용할 수 있습니다.

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

따라서 사용자가 [대상 연결 자습서](../../../ui/connect-destination.md)를 눌러 대상 플랫폼에 연결하려면 먼저 영역을 선택해야 합니다. 그들이 목적지에 연결할 때, 템플화된 필드 `{{customerData.region}}` 은 아래 이미지와 같이 UI에서 사용자가 선택한 값으로 대체됩니다.

![영역 선택기가 있는 대상 연결 화면을 표시하는 Ui 이미지입니다.](../../assets/functionality/destination-server/server-spec-template-region.png)

## 실시간(스트리밍) 대상 서버 {#streaming-example}

이 대상 서버 유형을 사용하면 HTTP 요청을 통해 Adobe Experience Platform의 데이터를 대상으로 내보낼 수 있습니다. 서버 구성에는 메시지를 받는 서버(사용자 측 서버)에 대한 정보가 포함되어 있습니다.

이 프로세스는 대상 플랫폼에 일련의 HTTP 메시지로 사용자 데이터를 전달합니다. 아래 매개 변수는 HTTP 서버 사양 템플릿에서 가져옵니다.

아래 샘플은 실시간(스트리밍) 대상에 대한 대상 서버 구성의 예를 보여줍니다.

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | *필수 여부.* Adobe에만 표시되는 서버의 친숙한 이름을 나타냅니다. 파트너 또는 고객은 이 이름을 볼 수 없습니다. 예: `Moviestar destination server`. |
| `destinationServerType` | 문자열 | *필수 여부.* 을(를) (으)로 설정합니다. `URL_BASED` 스트리밍 대상 |
| `templatingStrategy` | 문자열 | *필수 여부.* <ul><li>사용 `PEBBLE_V1` 에서 하드 코딩된 값 대신 템플릿을 사용하는 경우 `value` 필드. 다음과 같은 종단점이 있는 경우 이 옵션을 사용합니다. `https://api.moviestar.com/data/{{customerData.region}}/items`: 사용자가 Platform UI에서 끝점 영역을 선택해야 합니다. </li><li> 사용 `NONE` Adobe 측에 임시 변환이 필요하지 않으면(예: 다음과 같은 종단점이 있는 경우) `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 문자열 | *필수 여부.* Experience Platform이 연결해야 하는 API 엔드포인트의 주소를 입력합니다. |

{style="table-layout:auto"}

## [!DNL Amazon S3] 대상 서버 {#s3-example}

이 대상 서버를 사용하면 Adobe Experience Platform 데이터가 포함된 파일을 Amazon S3 저장소로 내보낼 수 있습니다.

아래 샘플은 Amazon S3 대상에 대한 대상 서버 구성의 예를 보여줍니다.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 서버의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 파일을 로 내보내려면 [!DNL Amazon S3] 버킷: `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `bucket.value` 필드.<ul><li>사용자가 Experience Platform UI에서 자신의 버킷 이름을 입력하도록 하려면 이 값을 로 설정하십시오 `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 대해 처럼 하드 코딩된 버킷 이름을 사용하는 경우 `"bucket.value":"MyBucket"`그런 다음 이 값을 로 설정합니다. `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | 문자열 | 의 이름 [!DNL Amazon S3] 이 대상에서 사용할 버킷입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `path.value` 필드.<ul><li>사용자가 Experience Platform UI에서 자신의 경로를 입력하도록 하려면 이 값을 로 설정하십시오 `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `path.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 처럼 하드 코딩된 경로를 사용하는 경우 `"bucket.value":"/path/to/MyBucket"`그런 다음 이 값을 로 설정합니다. `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | 문자열 | 경로 [!DNL Amazon S3] 이 대상에서 사용할 버킷입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] 대상 서버 {#sftp-example}

이 대상 서버를 사용하면 Adobe Experience Platform 데이터가 포함된 파일을 [!DNL SFTP] 저장소 서버.

아래 샘플은 SFTP 대상에 대한 대상 서버 구성의 예를 보여줍니다.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 서버의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 파일을 로 내보내려면 [!DNL SFTP] 대상, 다음 위치로 설정 `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `rootDirectory.value` 필드.<ul><li>사용자가 Experience Platform UI에서 고유한 루트 디렉토리 경로를 입력하도록 하려면 이 값을 로 설정합니다. `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `rootDirectory.value` 필드에서 사용자가 제공한 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 대해 하드 코딩된 루트 디렉토리 경로를 사용하는 경우(예: ) `"rootDirectory.value":"Storage/MyDirectory"`그런 다음 이 값을 로 설정합니다. `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | 문자열 | 내보낸 파일을 호스트할 디렉토리의 경로입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `hostName.value` 필드.<ul><li>사용자가 Experience Platform UI에서 고유한 호스트 이름을 입력하도록 하려면 이 값을 로 설정합니다 `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `hostName.value` 필드에서 사용자가 제공한 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 대해 처럼 하드 코딩된 호스트 이름을 사용하는 경우 `"hostName.value":"my.hostname.com"`그런 다음 이 값을 로 설정합니다. `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | 문자열 | SFTP 서버의 호스트 이름입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `"hostName.value":"my.hostname.com"`. |
| `port` | 정수 | SFTP 파일 서버 포트입니다. |
| `encryptionMode` | 문자열 | 파일 암호화를 사용할지 여부를 나타냅니다. 지원되는 값: <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) 대상 서버 {#adls-example}

이 대상 서버를 사용하면 Adobe Experience Platform 데이터가 포함된 파일을 [!DNL Azure Data Lake Storage] 계정이 필요합니다.

아래 샘플은 [!DNL Azure Data Lake Storage] 대상.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Azure Data Lake Storage] 대상, 다음 위치로 설정 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `path.value` 필드.<ul><li>사용자가 [!DNL ADLS] Experience Platform UI의 폴더 경로에서 이 값을 로 설정합니다. `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `path.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 처럼 하드 코딩된 경로를 사용하는 경우 `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`그런 다음 이 값을 로 설정합니다. `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | 문자열 | 경로 [!DNL ADLS] 저장소 폴더. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] 대상 서버 {#blob-example}

이 대상 서버를 사용하면 Adobe Experience Platform 데이터가 포함된 파일을 [!DNL Azure Blob Storage] 컨테이너.

아래 샘플은 [!DNL Azure Blob Storage] 대상.

```json
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
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Azure Blob Storage] 대상, 다음 위치로 설정 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `path.value` 필드.<ul><li>사용자가 직접 입력하도록 하려면 [!DNL Azure Blob] [저장소 계정 URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) Experience Platform UI에서 이 값을 로 설정합니다. `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `path.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 처럼 하드 코딩된 경로를 사용하는 경우 `"path.value": "https://myaccount.blob.core.windows.net/"`그런 다음 이 값을 로 설정합니다. `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | 문자열 | 경로 [!DNL Azure Blob] 저장. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `container.value` 필드.<ul><li>사용자가 직접 입력하도록 하려면 [!DNL Azure Blob] [컨테이너 이름](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) Experience Platform UI에서 이 값을 로 설정합니다. `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `container.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 대해 처럼 하드 코딩된 컨테이너 이름을 사용하는 경우 `"path.value: myContainer"`그런 다음 이 값을 로 설정합니다. `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | 문자열 | 이 대상에 사용할 Azure Blob 저장소 컨테이너의 이름입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) 대상 서버 {#dlz-example}

이 대상 서버를 사용하면 플랫폼 데이터가 포함된 파일을 [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) 저장.

아래 샘플은 [!DNL Data Landing Zone] ([!DNL DLZ]) 대상.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Data Landing Zone] 대상, 다음 위치로 설정 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `path.value` 필드.<ul><li>사용자가 직접 입력하도록 하려면 [!DNL Data Landing Zone] Experience Platform UI에서 이 값을 로 설정합니다. `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `path.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 처럼 하드 코딩된 경로를 사용하는 경우 `"path.value": "https://myaccount.blob.core.windows.net/"`그런 다음 이 값을 로 설정합니다. `NONE`. |
| `fileBasedDlzDestination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] 대상 서버 {#gcs-example}

이 대상 서버를 사용하면 플랫폼 데이터가 포함된 파일을 [!DNL Google Cloud Storage] 계정이 필요합니다.

아래 샘플은 [!DNL Google Cloud Storage] 대상.

```json
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
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Google Cloud Storage] 대상, 다음 위치로 설정 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `bucket.value` 필드.<ul><li>사용자가 직접 입력하도록 하려면 [!DNL Google Cloud Storage] Experience Platform UI의 버킷 이름, 이 값을 `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `bucket.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 대해 처럼 하드 코딩된 버킷 이름을 사용하는 경우 `"bucket.value": "my-bucket"`그런 다음 이 값을 로 설정합니다. `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 문자열 | 의 이름 [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 문자열 | *필수 여부*. 에서 사용되는 값의 유형에 따라 이 값을 설정합니다. `path.value` 필드.<ul><li>사용자가 직접 입력하도록 하려면 [!DNL Google Cloud Storage] Experience Platform UI의 버킷 경로에서 이 값을 로 설정합니다. `PEBBLE_V1`. 이 경우 다음을 템플릿을 설정해야 합니다 `path.value` 필드에서 값을 읽을 필드 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했습니다. 이 사용 사례는 위의 예에 나와 있습니다.</li><li>통합에 처럼 하드 코딩된 경로를 사용하는 경우 `"path.value": "/path/to/my-bucket"`그런 다음 이 값을 로 설정합니다. `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | 문자열 | 경로 [!DNL Google Cloud Storage] 이 대상에서 사용할 폴더입니다. 이것은 그 가치를 읽을 템플릿화된 필드일 수 있다 [고객 데이터 필드](../destination-configuration/customer-data-fields.md) 사용자가 입력했거나(위 예제 참조), `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상 서버 사양이 무엇이고 대상 서버 사양을 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 서버 구성 요소에 대해 자세히 알아보려면 다음 문서를 참조하십시오.

* [템플릿 사양](templating-specs.md)
* [메시지 포맷](message-format.md)
* [파일 형식 구성](file-formatting.md)
