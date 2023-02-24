---
solution: Experience Platform
title: (베타) Flow Service API를 사용하여 데이터 세트를 내보냅니다
description: Flow Service API를 사용하여 데이터 세트를 내보내고 대상을 선택하는 방법을 알아봅니다.
type: Tutorial
source-git-commit: c16fbc89b7bc7a8f1ee4a0ca4fd9f7541df095ca
workflow-type: tm+mt
source-wordcount: '3326'
ht-degree: 4%

---

# (베타) [!DNL Flow Service API]

>[!IMPORTANT]
>
>* 데이터 세트를 내보내는 기능은 현재 베타에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.
>* 이 베타 기능은 Real-time Customer Data Platform에 정의된 대로 1세대 데이터의 내보내기를 지원합니다 [제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* 이 기능은 Real-Time CDP Prime 또는 Ultimate 패키지를 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.


이 문서에서는 [!DNL Flow Service API] 내보내기 [데이터 세트](/help/catalog/datasets/overview.md) Adobe Experience Platform에서 선호하는 클라우드 스토리지 위치(예: ) [!DNL Amazon S3], SFTP 위치 또는 [!DNL Google Cloud Storage].

>[!TIP]
>
>Experience Platform 사용자 인터페이스를 사용하여 데이터 세트를 내보낼 수도 있습니다. 다음 문서를 참조하십시오. [데이터 세트 UI 내보내기 자습서](/help/destinations/ui/export-datasets.md) 추가 정보.

## 시작하기 {#get-started}

![개요 - 대상 만들기 및 데이터 세트 내보내기 절차](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): Adobe Experience Platform에 성공적으로 수집된 모든 데이터는 [!DNL Data Lake] 을 데이터 세트로 사용합니다. 데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. 데이터 세트에는 저장하는 데이터의 다양한 측면을 설명하는 메타데이터도 포함됩니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 Platform의 클라우드 스토리지 대상으로 데이터 세트를 내보내기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요 권한 {#permissions}

데이터 세트를 내보내려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, 및 **[!UICONTROL 데이터 집합 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

데이터 세트를 내보내는 데 필요한 권한이 있고 대상이 데이터 세트 내보내기를 지원하는지 확인하려면 대상 카탈로그를 찾아보십시오. 대상에 **[!UICONTROL 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]** 그런 다음 적절한 권한이 있습니다.

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 및 선택적 헤더에 대한 값을 수집합니다 {#gather-values-headers}

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [Experience Platform 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 분리할 수 있습니다. 요청에서 [!DNL Platform] API를 사용하여 작업을 수행할 샌드박스의 이름과 ID를 지정할 수 있습니다. 선택적 매개 변수입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### API 참조 설명서 {#api-reference-documentation}

이 자습서에서는 모든 API 작업에 대한 추가 참조 설명서를 찾을 수 있습니다. 자세한 내용은 [[!DNL Flow Service] - Adobe Developer 웹 사이트의 대상 API 설명서](https://developer.adobe.com/experience-platform-apis/references/destinations/). 이 자습서와 API 참조 설명서를 동시에 사용하는 것이 좋습니다.

### 용어집 {#glossary}

이 API 자습서에서 보게 되는 용어에 대한 설명은 다음을 참조하십시오. [용어집 섹션](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 추가 정보.

### 원하는 대상에 대한 연결 사양 및 흐름 사양을 수집합니다 {#gather-connection-spec-flow-spec}

데이터 세트 내보내기 워크플로우를 시작하기 전에 데이터 세트를 내보내려는 대상의 연결 사양 및 흐름 사양 ID를 식별합니다. 참조용으로 아래 표를 사용하십시오.


| 대상 | 연결 사양 | 흐름 사양 |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style=&quot;table-layout:auto&quot;}

다양한 구성을 위해서는 이러한 ID가 필요합니다 [!DNL Flow Service] 엔티티. 또한 [!DNL Connection Spec] 특정 엔티티를 설정하여 검색할 수 있도록 [!DNL Connection Spec] 변환 전: [!DNL Flow Service APIs]. 테이블의 모든 대상에 대한 연결 사양 검색 예를 참조하십시오.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++Retrieve [!DNL connection spec] 대상 [!DNL Amazon S3]

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

+++Retrieve [!DNL connection spec] 대상 [!DNL Azure Blob Storage]

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

+++Retrieve [!DNL connection spec] 대상 [!DNL Azure Data Lake Gen 2(ADLS Gen2])

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

+++Retrieve [!DNL connection spec] 대상 [!DNL Data Landing Zone(DLZ)]

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

>[!TAB Google 클라우드 스토리지]

**요청**

+++Retrieve [!DNL connection spec] 대상 [!DNL Google Cloud Storage]

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

+++Retrieve [!DNL connection spec] SFTP용

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

데이터 집합을 클라우드 저장소 대상으로 설정하려면 아래 절차를 따르십시오. 일부 단계의 경우 요청 및 응답이 다양한 클라우드 스토리지 대상 간에 다릅니다. 이러한 경우 페이지의 탭을 사용하여 데이터 세트를 연결하고 내보낼 대상에 대한 요청과 응답을 검색합니다. 반드시 올바른 [!DNL connection spec] 및 [!DNL flow spec] 을 전달하는 것이 좋습니다.

## 데이터 세트 목록 검색 {#retrieve-list-of-available-datasets}

![데이터 세트 내보내기 워크플로우에서 1단계를 보여주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

활성화할 수 있는 데이터 세트 목록을 검색하려면 아래 엔드포인트에 API 호출을 수행하여 을 시작합니다.

>[!BEGINSHADEBOX]

**요청**

+++적합한 데이터 세트 검색 - 요청

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

적합한 데이터 세트를 검색하려면 [!DNL connection spec] 요청 URL에 사용되는 ID는 데이터 레이크 소스 연결 사양 ID여야 합니다. `23598e46-f560-407b-88d5-ea6207e49db0`, 및 두 쿼리 매개 변수 `outputField=datasets` 및 `outputType=activationDatasets` 을(를) 지정해야 합니다. 다른 모든 쿼리 매개 변수는 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/).

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

성공적인 응답에는 활성화할 수 있는 데이터 세트 목록이 포함되어 있습니다. 이러한 데이터 세트는 다음 단계에서 소스 연결을 구성할 때 사용할 수 있습니다.

반환된 각 데이터 세트에 대한 다양한 응답 매개 변수에 대한 자세한 내용은 [데이터 세트 API 개발자 설명서](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).

## 소스 연결 만들기 {#create-source-connection}

![데이터 세트 내보내기 워크플로우에서 2단계를 보여주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

내보낼 데이터 세트 목록을 검색한 후 이러한 데이터 세트 ID를 사용하여 소스 연결을 만들 수 있습니다.

>[!BEGINSHADEBOX]

**요청**

+++소스 연결 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

성공적인 응답은 ID(`id`) 내의 아무 곳에나 삽입할 수 있습니다 `etag`. 데이터 흐름을 만들 때 나중에 필요할 때 소스 연결 ID를 기록해 둡니다.

또한 다음 사항을 기억하십시오.

* 이 단계에서 만든 소스 연결을 데이터 세트에 데이터 세트를 대상으로 활성화하려면 데이터 로드에 연결해야 합니다. 자세한 내용은 [데이터 흐름 만들기](#create-dataflow) 데이터 플로우에 소스 연결을 연결하는 방법에 대한 섹션을 참조하십시오.
* 소스 연결의 데이터 세트 ID는 만든 후에 수정할 수 없습니다. 소스 연결에서 데이터 세트를 추가 또는 제거해야 하는 경우 새 소스 연결을 만들고 새 소스 연결의 ID를 데이터 흐름도에 연결해야 합니다.

## (target) 기본 연결 만들기 {#create-base-connection}

![데이터 세트 내보내기 워크플로우에서 3단계를 보여주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

기본 연결은 자격 증명을 대상에 안전하게 저장합니다. 대상 유형에 따라 해당 대상에 대해 인증하는 데 필요한 자격 증명이 달라질 수 있습니다. 이러한 인증 매개 변수를 찾으려면 먼저 [!DNL connection spec] 섹션에 설명된 대로 원하는 대상에 대해 [연결 사양 및 흐름 사양 수집](#gather-connection-spec-flow-spec) 그런 다음 `authSpec` 응답 중 하나를 선택합니다. 아래 탭에서 `authSpec` 지원되는 모든 대상의 속성.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 표시 [!DNL auth spec]

강조표시된 줄과 인라인 메모를 [!DNL connection spec] 아래 예에서는 에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] 표시 [!DNL auth spec]

강조표시된 줄과 인라인 메모를 [!DNL connection spec] 아래 예에서는 에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] 표시 [!DNL auth spec]

강조표시된 줄과 인라인 메모를 [!DNL connection spec] 아래 예에서는 에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] 표시 [!DNL auth spec]

>[!NOTE]
>
>데이터 랜딩 영역 대상에는 [!DNL auth spec].

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

>[!TAB Google 클라우드 스토리지]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] 표시 [!DNL auth spec]

강조표시된 줄과 인라인 메모를 [!DNL connection spec] 아래 예에서는 에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

+++SFTP - [!DNL Connection spec] 표시 [!DNL auth spec]

>[!NOTE]
>
>SFTP 대상에는 [!DNL auth spec], 암호와 SSH 키 인증을 모두 지원합니다.

강조표시된 줄과 인라인 메모를 [!DNL connection spec] 아래 예에서는 에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

인증 세부 항목에 지정된 속성 사용(예: `authSpec` 응답에서) 아래 예와 같이 각 대상 유형에 맞는 필수 자격 증명으로 기본 연결을 만들 수 있습니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++[!DNL Amazon S3] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 가져오는 방법에 대한 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) Amazon S3 대상 설명서 페이지의 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
>필요한 인증 자격 증명을 가져오는 방법에 대한 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) azure Blob 저장 공간 대상 설명서 페이지의 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
>필요한 인증 자격 증명을 가져오는 방법에 대한 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) Azure Data Lake Gen 2(ADLS Gen2) 대상 설명서 페이지의 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
>데이터 랜딩 영역 대상에 대한 인증 자격 증명이 필요하지 않습니다. 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) 섹션(데이터 랜딩 영역 대상 설명서)

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection",
  "auth": {
    "name": "Data Landing Zone(DLZ) Base Connection",
    "description": "Data Landing Zone(DLZ) Base Connection",
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
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

>[!TAB Google 클라우드 스토리지]

**요청**

+++[!DNL Google Cloud Storage] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 가져오는 방법에 대한 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) Google 클라우드 스토리지 대상 설명서 페이지의 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

+++SFTP(암호 포함) - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 가져오는 방법에 대한 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

+++SFTP(SSH 키 포함) - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 가져오는 방법에 대한 자세한 내용은 [대상 인증](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 섹션을 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

응답에서 연결 ID를 확인합니다. 이 ID는 Target 연결을 만들 때 다음 단계에서 필요합니다.

## 대상 연결 만들기 {#create-target-connection}

![데이터 세트 내보내기 워크플로우에서 4단계를 보여주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

그런 다음 데이터 세트에 대한 내보내기 매개 변수를 저장하는 타겟 연결을 만들어야 합니다. 내보내기 매개 변수에는 위치, 파일 형식, 압축 및 기타 세부 사항이 포함됩니다. 자세한 내용은 `targetSpec` 대상의 연결 사양에 제공된 등록 정보로서 각 대상 유형에 대해 지원되는 속성을 이해합니다. 아래 탭에서 `targetSpec` 지원되는 모든 대상의 속성.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] target 연결 매개 변수 표시

강조표시된 선과 인라인 메모를 [!DNL connection spec] 아래 예에서는 를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL target spec] 연결 사양의 매개변수. 아래 예에는 어떤 타겟 매개 변수가 있는지 나와 있습니다 *not* 데이터 집합 내보내기 대상에 적용할 수 있습니다.

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

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] target 연결 매개 변수 표시

강조표시된 선과 인라인 메모를 [!DNL connection spec] 아래 예에서는 를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL target spec] 연결 사양의 매개변수. 아래 예에는 어떤 타겟 매개 변수가 있는지 나와 있습니다 *not* 데이터 집합 내보내기 대상에 적용할 수 있습니다.

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

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] target 연결 매개 변수 표시

강조표시된 선과 인라인 메모를 [!DNL connection spec] 아래 예에서는 를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL target spec] 연결 사양의 매개변수. 아래 예에는 어떤 타겟 매개 변수가 있는지 나와 있습니다 *not* 데이터 집합 내보내기 대상에 적용할 수 있습니다.

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

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] target 연결 매개 변수 표시

강조표시된 선과 인라인 메모를 [!DNL connection spec] 아래 예에서는 를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL target spec] 연결 사양의 매개변수. 아래 예에는 어떤 타겟 매개 변수가 있는지 나와 있습니다 *not* 데이터 집합 내보내기 대상에 적용할 수 있습니다.

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

>[!TAB Google 클라우드 스토리지]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] target 연결 매개 변수 표시

강조표시된 선과 인라인 메모를 [!DNL connection spec] 아래 예에서는 를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL target spec] 연결 사양의 매개변수. 아래 예에는 어떤 타겟 매개 변수가 있는지 나와 있습니다 *not* 데이터 집합 내보내기 대상에 적용할 수 있습니다.

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

+++SFTP - [!DNL Connection spec] target 연결 매개 변수 표시

강조표시된 선과 인라인 메모를 [!DNL connection spec] 아래 예에서는 를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL target spec] 연결 사양의 매개변수. 아래 예에는 어떤 타겟 매개 변수가 있는지 나와 있습니다 *not* 데이터 집합 내보내기 대상에 적용할 수 있습니다.

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

+++[!DNL Amazon S3] - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 [대상 세부 사항 채우기](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 섹션 [!DNL Amazon S3] 대상 설명서 페이지.
>의 다른 지원되는 값에 대해 `datasetFileType`를 참조하려면 API 참조 설명서 를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Beta Target Connection",
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

+++[!DNL Azure Blob Storage] - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 [대상 세부 사항 채우기](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) 섹션 [!DNL Azure Blob Storage] 대상 설명서 페이지.
>의 다른 지원되는 값에 대해 `datasetFileType`를 참조하려면 API 참조 설명서 를 참조하십시오.


추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Beta Target Connection",
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

+++[!DNL Azure Blob Storage] - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 [대상 세부 사항 채우기](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) azure 섹션 [!DNL Data Lake Gen 2(ADLS Gen2)] 대상 설명서 페이지.
>의 다른 지원되는 값에 대해 `datasetFileType`를 참조하려면 API 참조 설명서 를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

+++[!DNL Data Landing Zone] - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 [대상 세부 사항 채우기](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) 섹션 [!DNL Data Landing Zone] 대상 설명서 페이지.
>의 다른 지원되는 값에 대해 `datasetFileType`를 참조하려면 API 참조 설명서 를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

>[!TAB Google 클라우드 스토리지]

**요청**

+++[!DNL Google Cloud Storage] - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 [대상 세부 사항 채우기](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 섹션 [!DNL Google Cloud Storage] 대상 설명서 페이지.
>의 다른 지원되는 값에 대해 `datasetFileType`를 참조하려면 API 참조 설명서 를 참조하십시오.


추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
>필요한 대상 매개 변수를 가져오는 방법에 대한 자세한 내용은 [대상 세부 사항 채우기](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 섹션을 참조하십시오.
>의 다른 지원되는 값에 대해 `datasetFileType`를 참조하려면 API 참조 설명서 를 참조하십시오.

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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

응답에서 Target 연결 ID를 확인합니다. 이 ID는 데이터 세트를 내보내기 위해 데이터 흐름을 만들 때 다음 단계에서 필요합니다.

## 데이터 흐름 만들기 {#create-dataflow}

![데이터 세트 내보내기 워크플로우에서 5단계를 보여주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

대상 구성의 마지막 단계는 데이터 흐름을 설정하는 것입니다. 데이터 흐름은 이전에 만든 엔티티를 함께 결합하고 데이터 집합 내보내기 일정을 구성하기 위한 옵션을 제공합니다. 데이터 흐름을 만들려면 원하는 클라우드 저장소 대상에 따라 아래 페이로드를 사용하고 이전 단계의 엔티티 ID를 바꾸십시오.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++데이터 흐름 만들기 [!DNL Amazon S3] 대상 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. Use "interval": 1 when you select "timeUnit": "day"
        "startTime": 1675901210 // UNIX timestamp start time (in seconds)
    }
}'
```

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

+++데이터 흐름 만들기 [!DNL Azure Blob Storage] 대상 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

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

+++데이터 흐름 만들기 [!DNL Azure Data Lake Gen 2(ADLS Gen2)] 대상 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

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

+++데이터 흐름 만들기 [!DNL Data Landing Zone] 대상 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

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

>[!TAB Google 클라우드 스토리지]

**요청**

+++데이터 흐름 만들기 [!DNL Google Cloud Storage] 대상 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

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

+++SFTP 대상에 데이터 흐름 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석을 사용하여 강조 표시된 줄을 확인합니다. 요청을 원하는 단말에 복사하여 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

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
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

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

응답에서 데이터 흐름 ID를 확인합니다. 이 ID는 성공적인 데이터 집합 내보내기의 유효성을 확인하기 위해 데이터 흐름 실행을 검색할 때 다음 단계에서 필요합니다.

## 데이터 흐름 실행 가져오기 {#get-dataflow-runs}

![데이터 세트 내보내기 워크플로우에서 6단계를 보여주는 다이어그램](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

데이터 흐름의 실행을 확인하려면 데이터 흐름 실행 API를 사용하십시오.

>[!BEGINSHADEBOX]

**요청**

+++Get 데이터 흐름 실행 - 요청

데이터 흐름 검색 요청에서 데이터 흐름을 만들 때 이전 단계에서 얻은 데이터 흐름 ID에 쿼리 매개 변수로 을 추가합니다.

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

+++Get 데이터 흐름 실행 - 응답

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

에 대한 정보를 찾을 수 있습니다 [데이터 흐름 실행 API에서 반환되는 다양한 매개 변수](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) 를 참조하십시오.

## API 오류 처리 {#api-error-handling}

이 자습서의 API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors) 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 가이드를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서를 따라 플랫폼을 기본 배치 클라우드 스토리지 대상 중 하나에 연결하고 데이터 세트를 내보내기 위해 각 대상에 데이터 흐름을 설정합니다. Flow Service API를 사용하여 기존 데이터 흐름을 편집하는 방법 등 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
* [Flow Service API를 사용하여 대상 데이터 흐름 업데이트](../api/update-destination-dataflows.md)