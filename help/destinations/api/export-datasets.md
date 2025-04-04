---
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 데이터 세트 내보내기
description: 흐름 서비스 API를 사용하여 데이터 세트를 내보내기 하여 대상을 선택하는 방법을 알아봅니다.
type: Tutorial
exl-id: f23a4b22-da04-4b3c-9b0c-790890077eaa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '5149'
ht-degree: 3%

---

# [!DNL Flow Service API]을(를) 사용하여 데이터 세트 내보내기

>[!AVAILABILITY]
>
>* 이 기능은 Real-Time CDP Prime 및 Ultimate 패키지, Adobe Journey Optimizer 또는 Customer Journey Analytics을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

>[!IMPORTANT]
>
>**작업 항목**: Experience Platform의 [2024년 9월 릴리스](/help/release-notes/latest/latest.md#destinations)에서는 데이터 세트 데이터 흐름 내보내기에 대한 `endTime` 날짜를 설정하는 옵션이 도입되었습니다. Adobe은 또한 9월 릴리스 *전에*&#x200B;생성된 모든 데이터 세트 내보내기 데이터 흐름에 대한 기본 종료 날짜를 2025년 5월 1일로 도입합니다. 이러한 데이터 흐름의 경우 종료 날짜 이전에 데이터 흐름의 종료 날짜를 수동으로 업데이트해야 합니다. 그렇지 않으면 해당 날짜의 내보내기를 중지해야 합니다. Experience Platform UI를 사용하여 5월 1일에 중지되도록 설정되는 데이터 흐름을 확인하십시오.
>
>마찬가지로, `endTime` 날짜를 지정하지 않고 만든 데이터 흐름의 경우 이 값은 기본적으로 만든 시간으로부터 6개월 후의 종료 시간으로 설정됩니다.

<!--

>You can retrieve a list of such dataflows by performing the following API call: `https://platform.adobe.io/data/foundation/flowservice/flows?property=scheduleParams.endTime==UNIXTIMESTAMPTHATWEWILLUSE`
>

-->

이 문서에서는 [!DNL Flow Service API]을(를) 사용하여 [데이터 세트](/help/catalog/datasets/overview.md)를 Adobe Experience Platform에서 선호하는 클라우드 저장소 위치(예: [!DNL Amazon S3], SFTP 위치 또는 [!DNL Google Cloud Storage])로 내보내는 데 필요한 워크플로에 대해 설명합니다.

>[!TIP]
>
>Experience Platform 사용자 인터페이스를 사용하여 데이터 세트를 내보낼 수도 있습니다. 자세한 내용은 [데이터 세트 내보내기 UI 자습서](/help/destinations/ui/export-datasets.md)를 참조하십시오.

## 내보내기에 사용 가능한 데이터 세트 {#datasets-to-export}

내보낼 수 있는 데이터 세트는 Experience Platform 애플리케이션(Real-Time CDP, Adobe Journey Optimizer), 계층(Prime 또는 Ultimate) 및 구매한 모든 추가 기능에 따라 다릅니다(예: Data Distiller).

내보낼 수 있는 데이터 세트를 이해하려면 UI 자습서 페이지의 [표](/help/destinations/ui/export-datasets.md#datasets-to-export)를 참조하십시오.

## 지원되는 대상 {#supported-destinations}

현재, 스크린샷에 강조 표시되고 아래에 나열된 클라우드 스토리지 대상으로 데이터 세트를 내보낼 수 있습니다.

데이터 집합 내보내기를 지원하는 ![대상](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 시작하기 {#get-started}

![개요 - 대상을 만들고 데이터 세트를 내보내는 단계](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 [!DNL Data Lake] 내에서 데이터 세트로 유지됩니다. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.
   * [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 데이터 세트를 Experience Platform의 클라우드 스토리지 대상으로 내보내기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요한 권한 {#permissions}

데이터 세트를 내보내려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 데이터 세트 보기]** 및 **[!UICONTROL 데이터 세트 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

데이터 세트를 내보내는 데 필요한 권한이 있고 대상이 데이터 세트 내보내기를 지원하는지 확인하려면 대상 카탈로그를 확인하십시오. 대상에 **[!UICONTROL 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]** 컨트롤이 있는 경우 적절한 권한이 있습니다.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 및 선택적 헤더에 대한 값 수집 {#gather-values-headers}

[!DNL Experience Platform] API를 호출하려면 먼저 [Experience Platform 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 리소스는 특정 가상 샌드박스로 격리될 수 있습니다. [!DNL Experience Platform] API에 대한 요청에서 작업을 수행할 샌드박스의 이름과 ID를 지정할 수 있습니다. 이러한 매개 변수는 선택 사항입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### API 참조 설명서 {#api-reference-documentation}

이 자습서에서 모든 API 작업에 대한 참조 설명서를 함께 찾을 수 있습니다. Adobe Developer 웹 사이트](https://developer.adobe.com/experience-platform-apis/references/destinations/)에서 [[!DNL Flow Service] - 대상 API 설명서를 참조하십시오. 이 자습서와 API 참조 설명서를 동시에 사용하는 것이 좋습니다.

### 용어집 {#glossary}

이 API 자습서에서 보게 되는 용어에 대한 설명은 API 참조 설명서의 [용어집 섹션](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary)을 참조하십시오.

### 원하는 대상에 대한 연결 사양 및 흐름 사양 수집 {#gather-connection-spec-flow-spec}

데이터 세트를 내보내는 워크플로우를 시작하기 전에 데이터 세트를 내보내려는 대상의 연결 사양 및 흐름 사양 ID를 식별합니다. 아래 표를 참조하십시오.


| 대상 | 연결 사양 | 흐름 사양 |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

다양한 [!DNL Flow Service] 엔터티를 만들려면 이러한 ID가 필요합니다. [!DNL Flow Service APIs]에서 [!DNL Connection Spec]을(를) 검색할 수 있도록 특정 엔터티를 설정하려면 [!DNL Connection Spec] 자체의 일부를 참조해야 합니다. 표의 모든 대상에 대한 연결 사양을 검색하는 아래 예를 참조하십시오.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++1}에 대해 [!DNL connection spec] 검색[!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**응답**

+++[!DNL Amazon S3] - 연결 사양

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Blob 저장소]

**요청**

+++1}에 대해 [!DNL connection spec] 검색[!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**응답**

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**요청**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2]에 대해 [!DNL connection spec] 검색)

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**응답**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

**요청**

+++1}에 대해 [!DNL connection spec] 검색[!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**응답**

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Google 클라우드 저장소]

**요청**

+++1}에 대해 [!DNL connection spec] 검색[!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**응답**

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**요청**

+++SFTP에 대해 [!DNL connection spec] 검색

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**응답**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

클라우드 스토리지 대상에 대한 데이터 세트 데이터 흐름을 설정하려면 아래 단계를 따르십시오. 일부 단계의 경우 요청 및 응답은 다양한 클라우드 스토리지 대상 간에 다릅니다. 이러한 경우 페이지의 탭을 사용하여 데이터 세트를 연결 및 내보내려는 대상에 대한 요청 및 응답을 검색합니다. 구성 중인 대상에 올바른 [!DNL connection spec] 및 [!DNL flow spec]을(를) 사용하십시오.

## 데이터 세트 목록 검색 {#retrieve-list-of-available-datasets}

![데이터 세트 내보내기 워크플로의 1단계를 보여 주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

활성화하기에 적합한 데이터 세트 목록을 검색하려면 먼저 아래 끝점에 대한 API 호출을 만듭니다.

>[!BEGINSHADEBOX]

**요청**

+++적격 데이터 세트 검색 - 요청

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

적격 데이터 세트를 검색하려면 요청 URL에 사용된 [!DNL connection spec] ID는 데이터 레이크 소스 연결 사양 ID `23598e46-f560-407b-88d5-ea6207e49db0`이어야 하며 두 개의 쿼리 매개 변수 `outputField=datasets` 및 `outputType=activationDatasets`을(를) 지정해야 합니다. 다른 모든 쿼리 매개 변수는 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에서 지원하는 표준 매개 변수입니다.

+++

**응답**

+++데이터 세트 검색 - 응답

```json
{
    "items": [
        {
            "id": "5ef3e324052581191aa6a466",
            "name": "AAM Authenticated Profiles Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e3259ad2a1191ab7dd7d",
            "name": "AAM Devices Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e325582424191b1beb42",
            "name": "AAM Devices Profile Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328582424191b1beb44",
            "name": "AAM Realtime",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328fe742a191b2b3ea5",
            "name": "AAM Realtime Profile Updates",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        }
    ],
    "pageInfo": {
        "start": 0,
        "end": 4,
        "total": 149,
        "hasNext": true
    }
}
```

+++

>[!ENDSHADEBOX]

성공적인 응답에는 활성화 가능한 데이터 세트 목록이 포함되어 있습니다. 이러한 데이터 세트는 다음 단계에서 소스 연결을 구성할 때 사용할 수 있습니다.

반환된 각 데이터 세트에 대한 다양한 응답 매개 변수에 대한 자세한 내용은 [데이터 세트 API 개발자 설명서](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets)를 참조하십시오.

## 소스 연결 만들기 {#create-source-connection}

![데이터 세트 내보내기 워크플로의 2단계를 보여 주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

내보낼 데이터 세트 목록을 검색한 후 해당 데이터 세트 ID를 사용하여 소스 연결을 만들 수 있습니다.

>[!BEGINSHADEBOX]

**요청**

+++소스 연결 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
  "name": "Connecting to Data Lake",
  "description": "Data Lake source connection to export datasets",
  "connectionSpec": {
    "id": "23598e46-f560-407b-88d5-ea6207e49db0", // this connection spec ID is always the same for Source Connections
    "version": "1.0"
  },
  "params": {
    "datasets": [ // datasets to activate
      {
        "dataSetId": "5ef3e3259ad2a1191ab7dd7d",
        "name": "AAM Devices Data"
      }
    ]
  }
}'
```

+++



**응답**

+++소스 연결 만들기 - 응답

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

성공한 응답은 새로 만든 원본 연결의 ID(`id`)와 `etag`을(를) 반환합니다. 소스 연결 ID는 나중에 데이터 흐름을 만들 때 필요하므로 기록해 두십시오.

또한 다음 사항을 기억하십시오.

* 이 단계에서 생성된 소스 연결은 해당 데이터 세트를 대상으로 활성화하기 위해 데이터 흐름에 연결되어야 합니다. 데이터 흐름에 원본 연결을 연결하는 방법에 대한 자세한 내용은 [데이터 흐름 만들기](#create-dataflow) 섹션을 참조하십시오.
* 소스 연결의 데이터 세트 ID는 만든 후에 수정할 수 없습니다. 소스 연결에서 데이터 세트를 추가하거나 제거해야 하는 경우 새 소스 연결을 만들고 새 소스 연결의 ID를 데이터 흐름에 연결해야 합니다.

## (대상) 기본 연결 만들기 {#create-base-connection}

![데이터 세트 내보내기 워크플로의 3단계를 보여 주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

기본 연결은 대상에 자격 증명을 안전하게 저장합니다. 대상 유형에 따라 해당 대상에 대해 인증하는 데 필요한 자격 증명이 달라질 수 있습니다. 이러한 인증 매개 변수를 찾으려면 먼저 [연결 사양 및 흐름 사양 수집](#gather-connection-spec-flow-spec) 섹션에 설명된 대로 원하는 대상에 대해 [!DNL connection spec]을(를) 검색한 다음 응답의 `authSpec`을(를) 확인하십시오. 지원되는 모든 대상의 `authSpec` 속성을 보려면 아래 탭을 참조하십시오.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] - [!DNL auth spec] 표시

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 참고하십시오. 이 줄은 [!DNL connection spec]에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다.

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Access Key",
                    "type": "KeyBased",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines auth params required for connecting to amazon-s3",
                        "type": "object",
                        "properties": {
                            "s3AccessKey": {
                                "description": "Access key id",
                                "type": "string",
                                "pattern": "^[A-Z2-7]{20}$"
                            },
                            "s3SecretKey": {
                                "description": "Secret access key for the user account",
                                "type": "string",
                                "format": "password",
                                "pattern": "^[A-Za-z0-9\/\\+]{40}$"
                            }
                        },
                        "required": [
                            "s3SecretKey",
                            "s3AccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB Azure Blob 저장소]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] - [!DNL auth spec] 표시

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 참고하십시오. 이 줄은 [!DNL connection spec]에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다.

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] - [!DNL auth spec] 표시

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 참고하십시오. 이 줄은 [!DNL connection spec]에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다.

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB 데이터 랜딩 영역(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] - [!DNL auth spec] 표시

>[!NOTE]
>
>데이터 랜딩 영역 대상에 [!DNL auth spec]이(가) 필요하지 않습니다.

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Google 클라우드 저장소]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] - [!DNL auth spec] 표시

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 참고하십시오. 이 줄은 [!DNL connection spec]에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다.

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec], [!DNL auth spec] 표시

>[!NOTE]
>
>SFTP 대상은 암호와 SSH 키 인증을 모두 지원하므로 [!DNL auth spec]에 두 개의 개별 항목을 포함합니다.

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 참고하십시오. 이 줄은 [!DNL connection spec]에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다.

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

인증 사양(즉, 응답의 `authSpec`)에 지정된 속성을 사용하여 아래 예와 같이 각 대상 유형에 맞는 필수 자격 증명으로 기본 연결을 만들 수 있습니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++[!DNL Amazon S3] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 Amazon S3 대상 설명서 페이지의 [대상에 대한 인증](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**응답**

+++[!DNL Amazon S3] 기본 연결 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob 저장소]

**요청**

+++[!DNL Azure Blob Storage] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 Azure Blob 저장소 대상 설명서 페이지의 [대상에 인증](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**응답**

+++[!DNL Azure Blob Storage] - 기본 연결 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**요청**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 Azure Data Lake Gen 2(ADLS Gen2) 대상 설명서 페이지의 [대상에 인증](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**응답**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - 기본 연결 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

**요청**

+++[!DNL Data Landing Zone(DLZ)] - 기본 연결 요청

>[!TIP]
>
>데이터 랜딩 영역 대상에 인증 자격 증명이 필요하지 않습니다. 자세한 내용은 데이터 랜딩 영역 대상 설명서 페이지의 [대상에 대한 인증](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) 섹션을 참조하십시오.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone Base Connection",
  "connectionSpec": {
    "id": "3567r537-2a7b-4583-ac39-ed38d4b848e8",
    "version": "1.0"
  }
}'
```

+++

**응답**

+++[!DNL Data Landing Zone] - 기본 연결 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google 클라우드 저장소]

**요청**

+++[!DNL Google Cloud Storage] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 Google 클라우드 저장소 대상 설명서 페이지의 [대상에 대한 인증](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**응답**

+++[!DNL Google Cloud Storage] - 기본 연결 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**요청**

+++암호가 포함된 SFTP - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 SFTP 대상 설명서 페이지의 [대상에 인증](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

+++SSH 키가 있는 SFTP - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 SFTP 대상 설명서 페이지의 [대상에 인증](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**응답**

+++SFTP - 기본 연결 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

응답에서 연결 ID를 확인합니다. 이 ID는 대상 연결을 만들 때 다음 단계에서 필요합니다.

## 대상 연결 만들기 {#create-target-connection}

![데이터 세트 내보내기 워크플로의 4단계를 보여 주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

다음으로 데이터 세트에 대한 내보내기 매개 변수를 저장하는 타겟 연결을 만들어야 합니다. 내보내기 매개 변수에는 위치, 파일 형식, 압축 및 기타 세부 사항이 포함됩니다. 각 대상 유형에 대해 지원되는 속성을 이해하려면 대상의 연결 사양에 제공된 `targetSpec` 속성을 참조하십시오. 지원되는 모든 대상의 `targetSpec` 속성을 보려면 아래 탭을 참조하십시오.

>[!IMPORTANT]
>
>JSON 파일로 내보내기는 압축 모드에서만 지원됩니다. [!DNL Parquet] 파일로 내보내기는 압축 모드와 압축 해제 모드 모두에서 지원됩니다.
>
>내보낸 JSON 파일의 형식은 NDJSON이며, 이는 빅 데이터 생태계의 표준 교환 형식입니다. Adobe에서는 NDJSON 호환 클라이언트를 사용하여 내보낸 파일을 읽는 것을 권장합니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++대상 연결 매개 변수를 표시하는 [!DNL Amazon S3] - [!DNL Connection spec]

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 메모하십시오. 연결 사양에서 [!DNL target spec] 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. 아래 예제에서 데이터 집합 내보내기 대상에 적용할 수 있는 대상 매개 변수가 *not*&#x200B;인지 확인할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,41,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Azure Blob 저장소]

+++대상 연결 매개 변수를 표시하는 [!DNL Azure Blob Storage] - [!DNL Connection spec]

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 메모하십시오. 연결 사양에서 [!DNL target spec] 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. 아래 예제에서 데이터 집합 내보내기 대상에 적용할 수 있는 대상 매개 변수가 *not*&#x200B;인지 확인할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++대상 연결 매개 변수를 표시하는 [!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 메모하십시오. 연결 사양에서 [!DNL target spec] 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. 아래 예제에서 데이터 집합 내보내기 대상에 적용할 수 있는 대상 매개 변수가 *not*&#x200B;인지 확인할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions":{...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

+++대상 연결 매개 변수를 표시하는 [!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 메모하십시오. 연결 사양에서 [!DNL target spec] 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. 아래 예제에서 데이터 집합 내보내기 대상에 적용할 수 있는 대상 매개 변수가 *not*&#x200B;인지 확인할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="9,21,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
        "targetSpec": { // describes the target connection parameters
            "name": "User based target",
            "type": "UserNamespace",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "path": {
                        "title": "Folder path",
                        "description": "Enter the path to your Azure Data Lake Storage folder",
                        "type": "string"
                    },
                    "fileType": {...}, // not applicable to dataset destinations
                    "datasetFileType": {
                        "conditional": {
                            "field": "flowSpec.attributes._workflow",
                            "operator": "CONTAINS",
                            "value": "DATASETS"
                        },
                        "title": "File Type",
                        "description": "Select file format",
                        "type": "string",
                        "enum": [
                            "JSON",
                            "PARQUET"
                        ]
                    },
                    "csvOptions": {...}, // not applicable to dataset destinations
                    "compression": {
                        "title": "Compression format",
                        "description": "Select the desired file compression format.",
                        "type": "string",
                        "enum": [
                            "NONE",
                            "GZIP"
                        ]
                    }
                },
                "required": [
                    "path",
                    "datasetFileType",
                    "compression",
                    "fileType"
                ]
            }
//...
```

+++

>[!TAB Google 클라우드 저장소]

+++대상 연결 매개 변수를 표시하는 [!DNL Google Cloud Storage] - [!DNL Connection spec]

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 메모하십시오. 연결 사양에서 [!DNL target spec] 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. 아래 예제에서 데이터 집합 내보내기 대상에 적용할 수 있는 대상 매개 변수가 *not*&#x200B;인지 확인할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - 대상 연결 매개 변수를 표시하는 [!DNL Connection spec]

아래 [!DNL connection spec] 예제에서 인라인 메모가 있는 강조 표시된 줄을 메모하십시오. 연결 사양에서 [!DNL target spec] 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. 아래 예제에서 데이터 집합 내보내기 대상에 적용할 수 있는 대상 매개 변수가 *not*&#x200B;인지 확인할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]


위의 사양을 사용하여 아래 탭에 표시된 대로 원하는 클라우드 스토리지 대상에 해당하는 Target 연결 요청을 구성할 수 있습니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++[!DNL Amazon S3] - 대상 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [!DNL Amazon S3] 대상 설명서 페이지의 [대상 세부 정보 채우기](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 섹션을 참조하십시오.
>`datasetFileType`의 다른 지원되는 값은 API 참조 설명서를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

**응답**

+++Target 연결 - 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob 저장소]

**요청**

+++[!DNL Azure Blob Storage] - 대상 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [!DNL Azure Blob Storage] 대상 설명서 페이지의 [대상 세부 정보 채우기](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) 섹션을 참조하십시오.
>`datasetFileType`의 다른 지원되는 값은 API 참조 설명서를 참조하십시오.


추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**응답**

+++Target 연결 - 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**요청**

+++[!DNL Azure Blob Storage] - 대상 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 Azure [!DNL Data Lake Gen 2(ADLS Gen2)] 대상 설명서 페이지의 [대상 세부 정보를 채우기](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) 섹션을 참조하세요.
>`datasetFileType`의 다른 지원되는 값은 API 참조 설명서를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

**응답**

+++Target 연결 - 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

**요청**

+++[!DNL Data Landing Zone] - 대상 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [!DNL Data Landing Zone] 대상 설명서 페이지의 [대상 세부 정보 채우기](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) 섹션을 참조하십시오.
>`datasetFileType`의 다른 지원되는 값은 API 참조 설명서를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

**응답**

+++Target 연결 - 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google 클라우드 저장소]

**요청**

+++[!DNL Google Cloud Storage] - 대상 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [!DNL Google Cloud Storage] 대상 설명서 페이지의 [대상 세부 정보 채우기](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 섹션을 참조하십시오.
>`datasetFileType`의 다른 지원되는 값은 API 참조 설명서를 참조하십시오.


추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**응답**

+++Target 연결 - 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**요청**

+++SFTP - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 SFTP 대상 설명서 페이지의 [대상 세부 정보를 입력하십시오](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 섹션을 참조하십시오.
>`datasetFileType`의 다른 지원되는 값은 API 참조 설명서를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

**응답**

+++Target 연결 - 응답

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

응답에서 Target 연결 ID를 확인합니다. 이 ID는 데이터 세트를 내보내기 위한 데이터 흐름을 만들 때 다음 단계에서 필수입니다.

## 데이터 흐름 만들기 {#create-dataflow}

![데이터 세트 내보내기 워크플로의 5단계를 보여 주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

대상 구성의 마지막 단계는 데이터 흐름을 설정하는 것입니다. 데이터 흐름은 이전에 만든 엔터티를 결합하고 데이터 세트 내보내기 일정을 구성하는 옵션도 제공합니다. 데이터 흐름을 만들려면 원하는 클라우드 스토리지 대상에 따라 아래 페이로드를 사용하고 이전 단계의 엔티티 ID를 바꾸십시오.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++[!DNL Amazon S3] 대상에 대한 데이터 세트 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "269ba276-16fc-47db-92b0-c1049a3c131f", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

아래 표에는 데이터 집합 내보내기에 대한 내보내기 시간, 빈도, 위치 등을 사용자 지정할 수 있는 `scheduleParams` 섹션의 모든 매개 변수에 대한 설명이 나와 있습니다.

| 매개변수 | 설명 |
|---------|----------|
| `exportMode` | `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. 사용 가능한 세 가지 내보내기 옵션은 <br>입니다. **전체 파일 - 한 번**: `"DAILY_FULL_EXPORT"`은(는) 데이터 집합의 일회성 전체 내보내기를 위해서만 `timeUnit`:`day` 및 `interval`:`0`과(와) 함께 사용할 수 있습니다. 데이터 세트의 일일 전체 내보내기는 지원되지 않습니다. 일별 내보내기가 필요한 경우 증분 내보내기 옵션을 사용합니다. <br> **매일 증분 내보내기**: 매일 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, `interval`:`1`을(를) 선택하십시오. <br> **증분 시간별 내보내기**: 시간별 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, `interval` :`3`,`6`,`9` 또는 `12`을(를) 선택합니다. |
| `timeUnit` | 데이터 집합 파일을 내보내려는 빈도에 따라 `day` 또는 `hour`을(를) 선택하십시오. |
| `interval` | `timeUnit`이(가) 요일인 경우 `1`을(를) 선택하고 시간 단위가 `hour`인 경우 `3`,`6`,`9`,`12`을(를) 선택합니다. |
| `startTime` | 데이터 세트 내보내기가 시작되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `endTime` | 데이터 세트 내보내기가 종료되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `foldernameTemplate` | 내보낸 파일이 저장될 저장소 위치에 예상 폴더 이름 구조를 지정합니다. <ul><li><code>DATASET_ID</code> = <span>데이터 집합에 대한 고유 식별자입니다.</span></li><li><code>대상</code> = <span>대상 이름입니다.</span></li><li><code>날짜/시간</code> = <span>yyyyMMdd_HHmmss.</span> 형식의 날짜 및 시간입니다.</li><li><code>EXPORT_TIME</code> = <span>데이터 내보내기 예약 시간(형식: `exportTime=YYYYMMDDHHMM`.</span>)</li><li><code>대상_인스턴스_이름</code> = <span>대상의 특정 인스턴스 이름.</span></li><li><code>대상_인스턴스_ID</code> = <span>대상 인스턴스의 고유 식별자입니다.</span></li><li><code>샌드박스 이름</code> = <span>샌드박스 환경의 이름입니다.</span></li><li><code>조직 이름</code> = <span>조직 이름</span></li></ul> |

{style="table-layout:auto"}
+++

**응답**

+++데이터 흐름 만들기 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob 저장소]

**요청**

+++[!DNL Azure Blob Storage] 대상에 대한 데이터 세트 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "95bd8965-fc8a-4119-b9c3-944c2c2df6d2", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

아래 표에는 데이터 집합 내보내기에 대한 내보내기 시간, 빈도, 위치 등을 사용자 지정할 수 있는 `scheduleParams` 섹션의 모든 매개 변수에 대한 설명이 나와 있습니다.

| 매개변수 | 설명 |
|---------|----------|
| `exportMode` | `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. 사용 가능한 세 가지 내보내기 옵션은 <br>입니다. **전체 파일 - 한 번**: `"DAILY_FULL_EXPORT"`은(는) 데이터 집합의 일회성 전체 내보내기를 위해서만 `timeUnit`:`day` 및 `interval`:`0`과(와) 함께 사용할 수 있습니다. 데이터 세트의 일일 전체 내보내기는 지원되지 않습니다. 일별 내보내기가 필요한 경우 증분 내보내기 옵션을 사용합니다. <br> **매일 증분 내보내기**: 매일 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, `interval`:`1`을(를) 선택하십시오. <br> **증분 시간별 내보내기**: 시간별 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, `interval` :`3`,`6`,`9` 또는 `12`을(를) 선택합니다. |
| `timeUnit` | 데이터 집합 파일을 내보내려는 빈도에 따라 `day` 또는 `hour`을(를) 선택하십시오. |
| `interval` | `timeUnit`이(가) 요일인 경우 `1`을(를) 선택하고 시간 단위가 `hour`인 경우 `3`,`6`,`9`,`12`을(를) 선택합니다. |
| `startTime` | 데이터 세트 내보내기가 시작되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `endTime` | 데이터 세트 내보내기가 종료되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `foldernameTemplate` | 내보낸 파일이 저장될 저장소 위치에 예상 폴더 이름 구조를 지정합니다. <ul><li><code>DATASET_ID</code> = <span>데이터 집합에 대한 고유 식별자입니다.</span></li><li><code>대상</code> = <span>대상 이름입니다.</span></li><li><code>날짜/시간</code> = <span>yyyyMMdd_HHmmss.</span> 형식의 날짜 및 시간입니다.</li><li><code>EXPORT_TIME</code> = <span>데이터 내보내기 예약 시간(형식: `exportTime=YYYYMMDDHHMM`.</span>)</li><li><code>대상_인스턴스_이름</code> = <span>대상의 특정 인스턴스 이름.</span></li><li><code>대상_인스턴스_ID</code> = <span>대상 인스턴스의 고유 식별자입니다.</span></li><li><code>샌드박스 이름</code> = <span>샌드박스 환경의 이름입니다.</span></li><li><code>조직 이름</code> = <span>조직 이름</span></li></ul> |

{style="table-layout:auto"}

+++

**응답**

+++데이터 흐름 만들기 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**요청**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] 대상에 대한 데이터 세트 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

아래 표에는 데이터 집합 내보내기에 대한 내보내기 시간, 빈도, 위치 등을 사용자 지정할 수 있는 `scheduleParams` 섹션의 모든 매개 변수에 대한 설명이 나와 있습니다.

| 매개변수 | 설명 |
|---------|----------|
| `exportMode` | `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. 사용 가능한 세 가지 내보내기 옵션은 <br>입니다. **전체 파일 - 한 번**: `"DAILY_FULL_EXPORT"`은(는) 데이터 집합의 일회성 전체 내보내기를 위해서만 `timeUnit`:`day` 및 `interval`:`0`과(와) 함께 사용할 수 있습니다. 데이터 세트의 일일 전체 내보내기는 지원되지 않습니다. 일별 내보내기가 필요한 경우 증분 내보내기 옵션을 사용합니다. <br> **매일 증분 내보내기**: 매일 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, `interval`:`1`을(를) 선택하십시오. <br> **증분 시간별 내보내기**: 시간별 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, `interval` :`3`,`6`,`9` 또는 `12`을(를) 선택합니다. |
| `timeUnit` | 데이터 집합 파일을 내보내려는 빈도에 따라 `day` 또는 `hour`을(를) 선택하십시오. |
| `interval` | `timeUnit`이(가) 요일인 경우 `1`을(를) 선택하고 시간 단위가 `hour`인 경우 `3`,`6`,`9`,`12`을(를) 선택합니다. |
| `startTime` | 데이터 세트 내보내기가 시작되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `endTime` | 데이터 세트 내보내기가 종료되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `foldernameTemplate` | 내보낸 파일이 저장될 저장소 위치에 예상 폴더 이름 구조를 지정합니다. <ul><li><code>DATASET_ID</code> = <span>데이터 집합에 대한 고유 식별자입니다.</span></li><li><code>대상</code> = <span>대상 이름입니다.</span></li><li><code>날짜/시간</code> = <span>yyyyMMdd_HHmmss.</span> 형식의 날짜 및 시간입니다.</li><li><code>EXPORT_TIME</code> = <span>데이터 내보내기 예약 시간(형식: `exportTime=YYYYMMDDHHMM`.</span>)</li><li><code>대상_인스턴스_이름</code> = <span>대상의 특정 인스턴스 이름.</span></li><li><code>대상_인스턴스_ID</code> = <span>대상 인스턴스의 고유 식별자입니다.</span></li><li><code>샌드박스 이름</code> = <span>샌드박스 환경의 이름입니다.</span></li><li><code>조직 이름</code> = <span>조직 이름</span></li></ul> |

{style="table-layout:auto"}

+++

**응답**

+++데이터 흐름 만들기 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 데이터 랜딩 영역(DLZ)]

**요청**

+++[!DNL Data Landing Zone] 대상에 대한 데이터 세트 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

아래 표에는 데이터 집합 내보내기에 대한 내보내기 시간, 빈도, 위치 등을 사용자 지정할 수 있는 `scheduleParams` 섹션의 모든 매개 변수에 대한 설명이 나와 있습니다.

| 매개변수 | 설명 |
|---------|----------|
| `exportMode` | `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. 사용 가능한 세 가지 내보내기 옵션은 <br>입니다. **전체 파일 - 한 번**: `"DAILY_FULL_EXPORT"`은(는) 데이터 집합의 일회성 전체 내보내기를 위해서만 `timeUnit`:`day` 및 `interval`:`0`과(와) 함께 사용할 수 있습니다. 데이터 세트의 일일 전체 내보내기는 지원되지 않습니다. 일별 내보내기가 필요한 경우 증분 내보내기 옵션을 사용합니다. <br> **매일 증분 내보내기**: 매일 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, `interval`:`1`을(를) 선택하십시오. <br> **증분 시간별 내보내기**: 시간별 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, `interval` :`3`,`6`,`9` 또는 `12`을(를) 선택합니다. |
| `timeUnit` | 데이터 집합 파일을 내보내려는 빈도에 따라 `day` 또는 `hour`을(를) 선택하십시오. |
| `interval` | `timeUnit`이(가) 요일인 경우 `1`을(를) 선택하고 시간 단위가 `hour`인 경우 `3`,`6`,`9`,`12`을(를) 선택합니다. |
| `startTime` | 데이터 세트 내보내기가 시작되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `endTime` | 데이터 세트 내보내기가 종료되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `foldernameTemplate` | 내보낸 파일이 저장될 저장소 위치에 예상 폴더 이름 구조를 지정합니다. <ul><li><code>DATASET_ID</code> = <span>데이터 집합에 대한 고유 식별자입니다.</span></li><li><code>대상</code> = <span>대상 이름입니다.</span></li><li><code>날짜/시간</code> = <span>yyyyMMdd_HHmmss.</span> 형식의 날짜 및 시간입니다.</li><li><code>EXPORT_TIME</code> = <span>데이터 내보내기 예약 시간(형식: `exportTime=YYYYMMDDHHMM`.</span>)</li><li><code>대상_인스턴스_이름</code> = <span>대상의 특정 인스턴스 이름.</span></li><li><code>대상_인스턴스_ID</code> = <span>대상 인스턴스의 고유 식별자입니다.</span></li><li><code>샌드박스 이름</code> = <span>샌드박스 환경의 이름입니다.</span></li><li><code>조직 이름</code> = <span>조직 이름</span></li></ul> |

{style="table-layout:auto"}
+++

**응답**

+++데이터 흐름 만들기 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google 클라우드 저장소]

**요청**

+++[!DNL Google Cloud Storage] 대상에 대한 데이터 세트 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

아래 표에는 데이터 집합 내보내기에 대한 내보내기 시간, 빈도, 위치 등을 사용자 지정할 수 있는 `scheduleParams` 섹션의 모든 매개 변수에 대한 설명이 나와 있습니다.

| 매개변수 | 설명 |
|---------|----------|
| `exportMode` | `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. 사용 가능한 세 가지 내보내기 옵션은 <br>입니다. **전체 파일 - 한 번**: `"DAILY_FULL_EXPORT"`은(는) 데이터 집합의 일회성 전체 내보내기를 위해서만 `timeUnit`:`day` 및 `interval`:`0`과(와) 함께 사용할 수 있습니다. 데이터 세트의 일일 전체 내보내기는 지원되지 않습니다. 일별 내보내기가 필요한 경우 증분 내보내기 옵션을 사용합니다. <br> **매일 증분 내보내기**: 매일 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, `interval`:`1`을(를) 선택하십시오. <br> **증분 시간별 내보내기**: 시간별 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, `interval` :`3`,`6`,`9` 또는 `12`을(를) 선택합니다. |
| `timeUnit` | 데이터 집합 파일을 내보내려는 빈도에 따라 `day` 또는 `hour`을(를) 선택하십시오. |
| `interval` | `timeUnit`이(가) 요일인 경우 `1`을(를) 선택하고 시간 단위가 `hour`인 경우 `3`,`6`,`9`,`12`을(를) 선택합니다. |
| `startTime` | 데이터 세트 내보내기가 시작되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `endTime` | 데이터 세트 내보내기가 종료되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `foldernameTemplate` | 내보낸 파일이 저장될 저장소 위치에 예상 폴더 이름 구조를 지정합니다. <ul><li><code>DATASET_ID</code> = <span>데이터 집합에 대한 고유 식별자입니다.</span></li><li><code>대상</code> = <span>대상 이름입니다.</span></li><li><code>날짜/시간</code> = <span>yyyyMMdd_HHmmss.</span> 형식의 날짜 및 시간입니다.</li><li><code>EXPORT_TIME</code> = <span>데이터 내보내기 예약 시간(형식: `exportTime=YYYYMMDDHHMM`.</span>)</li><li><code>대상_인스턴스_이름</code> = <span>대상의 특정 인스턴스 이름.</span></li><li><code>대상_인스턴스_ID</code> = <span>대상 인스턴스의 고유 식별자입니다.</span></li><li><code>샌드박스 이름</code> = <span>샌드박스 환경의 이름입니다.</span></li><li><code>조직 이름</code> = <span>조직 이름</span></li></ul> |

{style="table-layout:auto"}

+++

**응답**

+++데이터 흐름 만들기 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**요청**

+++SFTP 대상에 대한 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "354d6aad-4754-46e4-a576-1b384561c440", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

아래 표에는 데이터 집합 내보내기에 대한 내보내기 시간, 빈도, 위치 등을 사용자 지정할 수 있는 `scheduleParams` 섹션의 모든 매개 변수에 대한 설명이 나와 있습니다.

| 매개변수 | 설명 |
|---------|----------|
| `exportMode` | `"DAILY_FULL_EXPORT"` 또는 `"FIRST_FULL_THEN_INCREMENTAL"`을(를) 선택하십시오. 두 옵션에 대한 자세한 내용은 일괄 처리 대상 활성화 자습서에서 [전체 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 및 [증분 파일 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)를 참조하십시오. 사용 가능한 세 가지 내보내기 옵션은 <br>입니다. **전체 파일 - 한 번**: `"DAILY_FULL_EXPORT"`은(는) 데이터 집합의 일회성 전체 내보내기를 위해서만 `timeUnit`:`day` 및 `interval`:`0`과(와) 함께 사용할 수 있습니다. 데이터 세트의 일일 전체 내보내기는 지원되지 않습니다. 일별 내보내기가 필요한 경우 증분 내보내기 옵션을 사용합니다. <br> **매일 증분 내보내기**: 매일 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, `interval`:`1`을(를) 선택하십시오. <br> **증분 시간별 내보내기**: 시간별 증분 내보내기를 사용하려면 `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, `interval` :`3`,`6`,`9` 또는 `12`을(를) 선택합니다. |
| `timeUnit` | 데이터 집합 파일을 내보내려는 빈도에 따라 `day` 또는 `hour`을(를) 선택하십시오. |
| `interval` | `timeUnit`이(가) 요일인 경우 `1`을(를) 선택하고 시간 단위가 `hour`인 경우 `3`,`6`,`9`,`12`을(를) 선택합니다. |
| `startTime` | 데이터 세트 내보내기가 시작되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `endTime` | 데이터 세트 내보내기가 종료되어야 하는 UNIX 단위 날짜 및 시간입니다. |
| `foldernameTemplate` | 내보낸 파일이 저장될 저장소 위치에 예상 폴더 이름 구조를 지정합니다. <ul><li><code>DATASET_ID</code> = <span>데이터 집합에 대한 고유 식별자입니다.</span></li><li><code>대상</code> = <span>대상 이름입니다.</span></li><li><code>날짜/시간</code> = <span>yyyyMMdd_HHmmss.</span> 형식의 날짜 및 시간입니다.</li><li><code>EXPORT_TIME</code> = <span>데이터 내보내기 예약 시간(형식: `exportTime=YYYYMMDDHHMM`.</span>)</li><li><code>대상_인스턴스_이름</code> = <span>대상의 특정 인스턴스 이름.</span></li><li><code>대상_인스턴스_ID</code> = <span>대상 인스턴스의 고유 식별자입니다.</span></li><li><code>샌드박스 이름</code> = <span>샌드박스 환경의 이름입니다.</span></li><li><code>조직 이름</code> = <span>조직 이름</span></li></ul> |

{style="table-layout:auto"}

+++

**응답**

+++데이터 흐름 만들기 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

응답에서 데이터 흐름 ID를 확인합니다. 이 ID는 성공적인 날짜 집합 내보내기의 유효성을 검사하기 위해 데이터 흐름 실행을 검색할 때 다음 단계에서 필요합니다.

## 데이터 흐름 실행 가져오기 {#get-dataflow-runs}

![데이터 세트 내보내기 워크플로의 6단계를 보여 주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

데이터 흐름 실행을 확인하려면 데이터 흐름 실행 API를 사용하십시오.

>[!BEGINSHADEBOX]

**요청**

+++데이터 흐름 실행 가져오기 - 요청

데이터 흐름 검색 요청에서 데이터 흐름을 만들 때 이전 단계에서 얻은 데이터 흐름 ID를 쿼리 매개 변수로 추가합니다.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**응답**

+++데이터 흐름 실행 가져오기 - 응답

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

API 참조 설명서에서 데이터 흐름에서 반환된 [다양한 매개 변수](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns)에 대한 정보를 찾을 수 있습니다.

## 데이터 세트 내보내기 성공 확인 {#verify}

데이터 세트를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 `.json` 또는 `.parquet` 파일을 만듭니다. [데이터 흐름을 만들 때](#create-dataflow)제공한 내보내기 일정에 따라 저장소 위치에 새 파일이 저장될 것으로 예상합니다.

Experience Platform은 사용자가 지정한 저장 위치에 폴더 구조를 만들며, 이 위치에 내보낸 데이터 세트 파일을 저장합니다. 내보내기 시간마다 아래 패턴을 따라 새 폴더가 만들어집니다.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

기본 파일 이름은 임의로 생성되며 내보낸 파일 이름이 고유한지 확인합니다.

### 샘플 데이터 세트 파일 {#sample-files}

스토리지 위치에 이러한 파일이 있으면 내보내기가 성공적으로 수행되었는지 확인할 수 있습니다. 내보낸 파일의 구조를 이해하기 위해 샘플 [.parquet 파일](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 또는 [.json 파일](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)을 다운로드할 수 있습니다.

#### 압축된 데이터 세트 파일 {#compressed-dataset-files}

[대상 연결을 만듭니다](#create-target-connection) 단계에서는 압축할 내보낸 데이터 세트 파일을 선택할 수 있습니다.

압축할 때 두 파일 유형 간의 파일 형식 차이를 확인합니다.

* 압축된 JSON 파일을 내보낼 때 내보낸 파일 형식은 `json.gz`입니다.
* 압축된 Parquet 파일을 내보낼 때 내보낸 파일 형식은 `gz.parquet`입니다.
* JSON 파일은 압축 모드에서만 내보낼 수 있습니다.

## API 오류 처리 {#api-error-handling}

이 자습서의 API 끝점은 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 오류 응답 해석에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 알려진 제한 사항 {#known-limitations}

데이터 집합 내보내기에 대한 [알려진 제한 사항](/help/destinations/ui/export-datasets.md#known-limitations)을 봅니다.

## 자주 묻는 질문 {#faq}

데이터 세트 내보내기에 대한 [자주 묻는 질문 목록](/help/destinations/ui/export-datasets.md#faq)을 봅니다.

## 다음 단계 {#next-steps}

이 자습서를 따라 기본 설정 일괄 처리 클라우드 스토리지 대상 중 하나에 Experience Platform을 연결하고 데이터 세트를 내보내기 위해 해당 대상에 데이터 흐름을 설정했습니다. 흐름 서비스 API를 사용하여 기존 데이터 흐름을 편집하는 방법과 같은 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
* [흐름 서비스 API를 사용하여 대상 데이터 흐름 업데이트](../api/update-destination-dataflows.md)