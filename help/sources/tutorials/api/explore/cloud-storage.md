---
keywords: Experience Platform;홈;인기 항목;클라우드 스토리지;클라우드 스토리지
solution: Experience Platform
title: Flow Service API를 사용하여 클라우드 스토리지 시스템 탐색
topic-legacy: overview
description: 이 자습서에서는 Flow Service API를 사용하여 타사 클라우드 스토리지 시스템을 탐색합니다.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 클라우드 스토리지 시스템 탐색

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 타사 클라우드 스토리지 시스템을 탐색합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../home.md):  [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../sandboxes/home.md):  [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 클라우드 스토리지 시스템에 성공적으로 접속하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 연결 ID 얻기

[!DNL Platform] API를 사용하여 타사 클라우드 저장소를 탐색하려면 유효한 연결 ID가 있어야 합니다. 작업할 스토리지에 대한 연결이 아직 없는 경우 다음 자습서를 통해 연결을 만들 수 있습니다.

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 클라우드 스토리지 살펴보기

클라우드 스토리지에 대한 연결 ID를 사용하면 GET 요청을 수행하여 파일 및 디렉토리를 탐색할 수 있습니다. 클라우드 스토리지를 탐색하기 위해 GET 요청을 수행할 때는 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `objectType` | 탐색할 객체 유형입니다. 다음 중 하나로 이 값을 설정합니다. <ul><li>`folder`: 특정 디렉토리 탐색</li><li>`root`: 루트 디렉토리를 탐색합니다.</li></ul> |
| `object` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 이 값은 탐색할 디렉토리의 경로를 나타냅니다. |

다음 호출을 사용하여 [!DNL Platform]에 가져올 파일의 경로를 찾습니다.

**API 형식**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONNECTION_ID}` | 클라우드 스토리지 소스 커넥터에 대한 연결 ID입니다. |
| `{PATH}` | 디렉토리의 경로입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 쿼리된 디렉터리 내에 있는 파일 및 폴더의 배열을 반환합니다. 다음 단계에서 해당 구조를 검사하기 위해 파일을 제공해야 하므로 업로드할 파일의 `path` 속성을 주목해야 합니다.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect 파일 구조

클라우드 저장소에서 데이터 파일의 구조를 검사하려면 파일의 경로 및 유형을 쿼리 매개 변수로 제공하면서 GET 요청을 수행합니다.

파일의 경로 및 유형을 제공하는 동안 GET 요청을 수행하여 클라우드 스토리지 소스에서 데이터 파일의 구조를 검사할 수 있습니다. 쿼리 매개 변수의 일부로 파일 유형을 지정하여 CSV, TSV 또는 압축된 JSON 및 구분된 파일과 같은 다양한 파일 유형을 검사할 수도 있습니다.

**API 형식**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 클라우드 스토리지 소스 커넥터의 연결 ID입니다. |
| `{FILE_PATH}` | 검사할 파일의 경로입니다. |
| `{FILE_TYPE}` | 파일의 유형입니다. 지원되는 파일 유형은 다음과 같습니다.<ul><li>구분된</code>: 구분 기호로 구분된 값입니다. DSV 파일은 쉼표로 구분해야 합니다.</li><li>JSON</code>: JavaScript 개체 표기법. JSON 파일은 XDM 호환이어야 합니다</li><li>PARQUET</code>: 아파치 쪽모이 세공. Parquet 파일은 XDM 규격 파일이어야 합니다.</li></ul> |
| `{QUERY_PARAMS}` | 결과를 필터링하는 데 사용할 수 있는 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](#query)의 섹션을 참조하십시오. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 테이블 이름 및 데이터 유형을 포함하여 쿼리된 파일의 구조를 반환합니다.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## 쿼리 매개 변수 사용 {#query}

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)에서는 쿼리 매개 변수를 사용하여 다른 파일 유형을 미리 보고 검사할 수 있습니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `columnDelimiter` | CSV 또는 TSV 파일을 검사할 열 구분 기호로 지정한 단일 문자 값입니다. 매개 변수를 제공하지 않으면 기본값은 쉼표 `(,)`입니다. |
| `compressionType` | 압축된 구분 또는 JSON 파일을 미리 보기 위한 필수 쿼리 매개 변수입니다. 지원되는 압축 파일은 다음과 같습니다. <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## 다음 단계

이 자습서를 통해 클라우드 스토리지 시스템을 살펴보고 [!DNL Platform]에 가져올 파일의 경로를 찾아서 해당 구조를 확인했습니다. 이 정보는 다음 자습서에서 [클라우드 저장소에서 데이터를 수집하고 Platform](../collect/cloud-storage.md)로 가져올 수 있습니다.
