---
keywords: Experience Platform;홈;인기 항목;클라우드 스토리지;클라우드 스토리지
title: Flow Service API를 사용하여 클라우드 스토리지 폴더 탐색
description: 이 자습서에서는 Flow Service API를 사용하여 타사 클라우드 스토리지 시스템을 탐색합니다.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# 을 사용하여 클라우드 스토리지 폴더 탐색 [!DNL Flow Service] API

이 자습서에서는 을(를) 사용하여 클라우드 스토리지의 구조와 컨텐츠를 탐색하고 미리 보는 방법에 대해 설명합니다. [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>클라우드 스토리지를 탐색하려면 클라우드 스토리지 소스에 유효한 기본 연결 ID가 있어야 합니다. 이 ID가 없다면 다음을 참조하십시오. [소스 개요](../../../home.md#cloud-storage) 을 사용하여 기본 연결을 만들 수 있는 클라우드 스토리지 소스 목록입니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../landing/api-guide.md).

## 클라우드 스토리지 폴더 탐색

에 GET 요청을 수행하여 클라우드 스토리지 폴더의 구조에 대한 정보를 검색할 수 있습니다 [!DNL Flow Service] 소스의 기본 연결 ID를 제공하는 동안 API입니다.

클라우드 스토리지를 탐색하기 위해 GET 요청을 수행할 때는 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `objectType` | 탐색할 객체 유형입니다. 다음 중 하나로 이 값을 설정합니다. <ul><li>`folder`: 특정 디렉토리 탐색</li><li>`root`: 루트 디렉토리를 탐색합니다.</li></ul> |
| `object` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 이 값은 탐색할 디렉토리의 경로를 나타냅니다. |


**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 클라우드 스토리지 소스의 기본 연결 ID입니다. |
| `{PATH}` | 디렉토리의 경로입니다. |

**요청**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 쿼리된 디렉터리 내에 있는 파일 및 폴더의 배열을 반환합니다. 다음 사항을 주목하십시오. `path` 다음 단계에서 해당 구조를 검사해야 하므로 업로드할 파일의 속성입니다.

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
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 클라우드 스토리지 소스 커넥터의 연결 ID입니다. |
| `{FILE_PATH}` | 검사할 파일의 경로입니다. |
| `{FILE_TYPE}` | 파일의 유형입니다. 지원되는 파일 유형은 다음과 같습니다.<ul><li>구분 기호</code>: 구분 기호로 구분된 값입니다. DSV 파일은 쉼표로 구분해야 합니다.</li><li>JSON</code>: JavaScript 개체 표기법. JSON 파일은 XDM 호환이어야 합니다</li><li>쪽모이 세공</code>: 아파치 쪽모이 세공. Parquet 파일은 XDM 규격 파일이어야 합니다.</li></ul> |
| `{QUERY_PARAMS}` | 결과를 필터링하는 데 사용할 수 있는 선택적 쿼리 매개 변수입니다. 의 섹션을 참조하십시오. [쿼리 매개 변수](#query) 추가 정보. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

다음 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 에서는 쿼리 매개 변수를 사용하여 다른 파일 유형을 미리 보고 검사할 수 있습니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `columnDelimiter` | CSV 또는 TSV 파일을 검사할 열 구분 기호로 지정한 단일 문자 값입니다. 매개 변수를 제공하지 않으면 기본값은 쉼표로 설정됩니다 `(,)`. |
| `compressionType` | 압축된 구분 또는 JSON 파일을 미리 보기 위한 필수 쿼리 매개 변수입니다. 지원되는 압축 파일은 다음과 같습니다. <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | 미리 보기를 렌더링할 때 사용할 인코딩 유형을 정의합니다. 지원되는 인코딩 유형은 다음과 같습니다. `UTF-8` 및 `ISO-8859-1`. **참고**: 다음 `encoding` 매개 변수는 구분된 CSV 파일을 수집할 때만 사용할 수 있습니다. 다른 파일 유형은 기본 인코딩으로 수집됩니다. `UTF-8`. |

## 다음 단계

이 자습서를 통해 클라우드 스토리지 시스템을 살펴보고 가져올 파일의 경로를 찾았습니다 [!DNL Platform], 및에서 해당 구조를 확인했습니다. 이 정보는 다음 자습서에서 사용할 수 있습니다 [클라우드 스토리지에서 데이터를 수집하여 플랫폼으로 가져오기](../collect/cloud-storage.md).
