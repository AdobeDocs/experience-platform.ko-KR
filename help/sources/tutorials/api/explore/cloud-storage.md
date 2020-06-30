---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 클라우드 스토리지 시스템 살펴보기
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---


# API를 사용하여 클라우드 스토리지 시스템 [!DNL Flow Service] 살펴보기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 타사 클라우드 스토리지 시스템을 탐색합니다.

## 시작하기

이 가이드는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 클라우드 스토리지 시스템에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 기본 연결 받기

API를 사용하여 타사 클라우드 스토리지를 탐색하려면 [!DNL Platform] 유효한 기본 연결 ID를 보유해야 합니다. 작업할 저장소에 대한 기본 연결이 아직 없는 경우 다음 자습서를 통해 기본 연결을 만들 수 있습니다.

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../create/cloud-storage/adls-gen2.md)
* [Google 클라우드 스토어](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 클라우드 스토리지 살펴보기

클라우드 스토리지에 대한 기본 연결을 사용하면 GET 요청을 수행하여 파일 및 디렉토리를 탐색할 수 있습니다. 클라우드 스토리지를 탐색하기 위해 GET 요청을 수행할 때는 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `objectType` | 탐색하려는 개체의 유형입니다. 다음 중 하나로 이 값을 설정합니다. <ul><li>`folder`: 특정 디렉토리 살펴보기</li><li>`root`: 루트 디렉토리를 살펴보십시오.</li></ul> |
| `object` | 이 매개 변수는 특정 디렉토리를 볼 때만 필요합니다. 이 값은 탐색할 디렉토리의 경로를 나타냅니다. |

다음 호출을 사용하여 가져올 파일의 경로를 찾습니다 [!DNL Platform].

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 클라우드 스토리지 기반 연결의 ID입니다. |
| `{PATH}` | 디렉토리 경로입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 쿼리된 디렉터리 내에 있는 파일 및 폴더의 배열을 반환합니다. 다음 단계에서 제공해야 하는 경우 업로드할 파일의 `path` 속성을 기록해 두십시오.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## 파일 구조 검사

클라우드 저장소에서 데이터 파일의 구조를 검사하려면 파일의 경로를 쿼리 매개 변수로 제공하면서 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 클라우드 스토리지 기반 연결의 ID입니다. |
| `{FILE_PATH}` | 파일의 경로입니다. |
| `{FILE_TYPE}` | 파일의 유형입니다. 지원되는 파일 유형은 다음과 같습니다.<ul><li>구분 기호</code>: 구분 기호로 구분된 값. DSV 파일은 쉼표로 구분되어야 합니다.</li><li>JSON</code>: JavaScript 개체 표기법. JSON 파일은 XDM과 호환되어야 합니다.</li><li>쪽모이 세공</code>: 아파치 쪽모이 세공. Parentheet 파일은 XDM과 호환되어야 합니다.</li></ul> |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

## 다음 단계

이 튜토리얼을 통해 클라우드 스토리지 시스템을 살펴보고 가져올 파일의 경로를 발견했으며 해당 구조를 [!DNL Platform]살펴보았습니다. 다음 튜토리얼에서 이 정보를 사용하여 클라우드 저장소에서 데이터를 [수집하여 Platform으로 가져올 수 있습니다](../collect/cloud-storage.md).