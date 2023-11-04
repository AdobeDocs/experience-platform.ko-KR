---
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 대상을 파일 기반 대상으로 활성화
description: 흐름 서비스 API를 사용하여 적격 프로필이 있는 파일을 클라우드 스토리지 대상으로 내보내는 방법을 알아봅니다.
type: Tutorial
exl-id: 62028c7a-3ea9-4004-adb7-5e27bbe904fc
source-git-commit: 9c07664873f649645db57a9a025277f515333b1e
workflow-type: tm+mt
source-wordcount: '4401'
ht-degree: 6%

---

# 흐름 서비스 API를 사용하여 대상을 파일 기반 대상으로 활성화

Experience Platform 외부에서 파일을 내보낼 때 향상된 사용자 정의 기능에 액세스하려면 향상된 파일 내보내기 기능을 사용하십시오.

* 추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* [향상된 매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능.
* 을(를) 선택하는 기능 [파일 유형](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 내보낸 파일.
* [사용자 정의 기능내보낸 CSV 데이터 파일의 서식](/help/destinations/ui/batch-destinations-file-formatting-options.md)을 사용자 정의하는 기능.

이 기능은 아래에 나열된 6개의 클라우드 스토리지 카드에서 지원됩니다.

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

이 문서에서는 을(를) 사용하는 데 필요한 워크플로에 대해 설명합니다 [플로우 서비스 API](https://developer.adobe.com/experience-platform-apis/references/destinations/) Adobe Experience Platform에서 위에 연결된 클라우드 스토리지 위치 중 하나로 적격한 프로필을 내보냅니다.

>[!TIP]
>
>Experience Platform 사용자 인터페이스를 사용하여 프로필을 클라우드 스토리지 대상으로 내보낼 수도 있습니다. 읽기 [파일 기반 대상 활성화 자습서](/help/destinations/ui/activate-batch-profile-destinations.md) 추가 정보.

<!--

## API users migration {#api-migration}

If you were already using the Flow Service API to export profiles to the Amazon S3, Azure Blob, or SFTP cloud storage destinations, read the [API migration guide](/help/destinations/api/api-migration-guide-cloud-storage-destinations.md) for necessary migration steps as Adobe transitions users from the legacy destinations to the new destinations. 

-->

## 시작하기 {#get-started}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/segment-export-overview.png)

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): [!DNL Experience Platform]이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] 에서 대상을 빌드하고 대상을 생성할 수 있습니다. [!DNL Adobe Experience Platform] (으)로부터 [!DNL Real-Time Customer Profile] 데이터.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 Platform에서 파일 기반 대상에 데이터를 활성화하기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요 권한 {#permissions}

프로필을 내보내려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 보기]**, 및 **[!UICONTROL 대상 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 문서에 사용된 규칙에 대한 자세한 내용은 [ 문제 해결 안내서의 ](../../landing/troubleshooting.md#how-do-i-format-an-api-request)예제 API 호출을 읽는 방법[!DNL Experience Platform] 섹션을 참조하세요.

### 필수 및 선택적 헤더에 대한 값 수집 {#gather-values-headers}

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [Experience Platform 인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스로 격리될 수 있습니다. 에 대한 요청에서 [!DNL Platform] API에서는 작업이 수행될 샌드박스의 이름과 ID를 지정할 수 있습니다. 이러한 매개 변수는 선택 사항입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Experience Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### API 참조 설명서 {#api-reference-documentation}

이 자습서에서 모든 API 작업에 대한 참조 설명서를 함께 찾을 수 있습니다. 다음을 참조하십시오. [Adobe Developer 웹 사이트의 흐름 서비스 - 대상 API 설명서](https://developer.adobe.com/experience-platform-apis/references/destinations/). 이 자습서와 API 참조 설명서를 동시에 사용하는 것이 좋습니다.

### 용어집 {#glossary}

이 API 자습서에서 보게 되는 용어에 대한 설명은 [용어집 섹션](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) API 참조 설명서의

## 대상자를 내보낼 대상 선택 {#select-destination}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step1.png)

프로필을 내보내는 워크플로우를 시작하기 전에 대상을 내보내려는 대상의 연결 사양 및 흐름 사양 ID를 식별합니다. 아래 표를 참조하십시오.

| 대상 | 연결 사양 | 흐름 사양 |
---------|----------|---------|
| Amazon S3 | `4fce964d-3f37-408f-9778-e597338a21ee` | `1a0514a6-33d4-4c7f-aff8-594799c47549` |
| Azure Blob 저장소 | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `752d422f-b16f-4f0d-b1c6-26e448e3b388` |
| Azure Data Lake Gen 2(ADLS Gen2) | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| 데이터 랜딩 영역(DLZ) | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| Google 클라우드 스토리지 | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `fd36aaa4-bf2b-43fb-9387-43785eeeb799` |

{style="table-layout:auto"}

이 자습서의 다음 단계에서 다양한 흐름 서비스 엔티티를 구성하려면 이러한 ID가 필요합니다. 흐름 서비스 API에서 연결 사양을 검색할 수 있도록 연결 사양 자체의 일부를 참조하여 특정 엔티티를 설정해야 합니다. 표의 모든 대상에 대한 연결 사양을 검색하는 아래 예를 참조하십시오.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++검색 [!DNL connection spec] 대상 [!DNL Amazon S3]

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

+++검색 [!DNL connection spec] 대상 [!DNL Azure Blob Storage]

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

+++검색 [!DNL connection spec] 대상 [!DNL Azure Data Lake Gen 2(ADLS Gen2])

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

+++검색 [!DNL connection spec] 대상 [!DNL Data Landing Zone(DLZ)]

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

+++검색 [!DNL connection spec] 대상 [!DNL Google Cloud Storage]

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

+++검색 [!DNL connection spec] SFTP용

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

아래 단계에 따라 클라우드 스토리지 대상으로 대상 내보내기 데이터 흐름을 설정하십시오. 일부 단계의 경우 요청 및 응답은 다양한 클라우드 스토리지 대상 간에 다릅니다. 이러한 경우 페이지의 탭을 사용하여 대상을 연결하고 내보내려는 대상에 대한 요청 및 응답을 검색합니다. 올바른 을(를) 사용하십시오 `connection spec` 및 `flow spec` 을(를) 구성하려는 대상에 대해 선택합니다.

## 소스 연결 만들기 {#create-source-connection}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step2.png)

대상을 내보낼 대상을 결정한 후 소스 연결을 만들어야 합니다. 다음 [소스 연결](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 내부로의 연결을 나타냅니다. [Experience Platform 프로필 저장소](/help/profile/home.md#profile-data-store).

>[!BEGINSHADEBOX]

**요청**

+++소스 연결 만들기 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 인라인 주석을 제거합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
   "name":"Connect to Profile Store",
   "description":"Optional",
   "connectionSpec":{
      "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1", // this connection spec ID is always the same for Source Connections
      "version":"1.0"
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

성공적인 응답은 ID( )를 반환합니다.`id`)을 참조하십시오. `etag`. 소스 연결 ID는 나중에 데이터 흐름을 만들 때 필요하므로 기록해 두십시오.

## 기본 연결을 만듭니다 {#create-base-connection}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step3.png)

A [기본 연결](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 대상에 자격 증명을 안전하게 저장합니다. 대상 유형에 따라 해당 대상에 대해 인증하는 데 필요한 자격 증명이 달라질 수 있습니다. 이러한 인증 매개 변수를 찾으려면 먼저 `connection spec` 섹션에 설명된 대로 원하는 대상에 대해 [대상자를 내보낼 대상 선택](#select-destination) 그리고 다음을 살펴보십시오. `authSpec` 응답. 다음 탭을 참조하십시오. `authSpec` 지원되는 모든 대상의 속성입니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 표시 [!DNL auth spec]

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 아래 예제 : 파일에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 아래 예제 : 파일에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 아래 예제 : 파일에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 아래 예제 : 파일에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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
>SFTP 대상에는 [!DNL auth spec]암호와 SSH 키 인증을 모두 지원합니다.

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 아래 예제 : 파일에서 인증 매개 변수를 찾을 위치에 대한 추가 정보를 제공합니다. [!DNL connection spec].

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

인증 사양에 지정된 속성(예: `authSpec` 응답에서 아래 예와 같이 각 대상 유형에 맞는 필수 자격 증명으로 기본 연결을 만들 수 있습니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++[!DNL Amazon S3] - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 섹션(Amazon S3 대상 설명서 페이지 참조)

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 섹션( Azure Blob 저장 공간 대상 설명서 페이지)에 표시됩니다.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="17"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) 섹션( Azure Data Lake Gen 2(ADLS Gen2) 대상 설명서 페이지).

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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
>데이터 랜딩 영역 대상에 인증 자격 증명이 필요하지 않습니다. 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) 섹션( 데이터 랜딩 영역 대상 설명서 페이지)을 참조하십시오.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
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
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) 섹션( Google 클라우드 스토리지 대상 설명서 페이지 )에 표시됩니다.

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 섹션( SFTP 대상 설명서 페이지)

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>",
      "port": "<Add port>"      
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

| 속성 | 설명 |
| --------- | ----------- |
| `specName` | `SFTP with Password` 사용. |
| `domain` | SFTP 저장소 위치의 IP 주소 또는 도메인 이름입니다. |
| `username` | SFTP 저장소 위치에 로그인할 사용자 이름입니다. |
| `password` | SFTP 저장소 위치에 로그인할 암호입니다. |
| `port` | SFTP 저장소 위치에서 사용하는 포트입니다. |

{style="table-layout:auto"}

+++

+++SSH 키가 있는 SFTP - 기본 연결 요청

>[!TIP]
>
>필요한 인증 자격 증명을 얻는 방법에 대한 자세한 내용은 [대상에 인증](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 섹션( SFTP 대상 설명서 페이지)

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 요청에서 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>",
      "port": "<Add port>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

| 속성 | 설명 |
| --------- | ----------- |
| `specName` | `SFTP with Password` 사용. |
| `domain` | SFTP 저장소 위치의 IP 주소 또는 도메인 이름입니다. |
| `username` | SFTP 저장소 위치에 로그인할 사용자 이름입니다. |
| `sshKey` | SFTP 저장소 위치에 로그인하는 데 사용되는 개인 SSH 키입니다. 비공개 키 형식은 Base64 인코딩된 문자열로 지정하며 암호로 보호해서는 안 됩니다. |
| `port` | SFTP 저장소 위치에서 사용하는 포트입니다. |

{style="table-layout:auto"}

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

### 내보낸 파일에 암호화 추가

선택적으로 내보낸 파일에 암호화를 추가할 수 있습니다. 이 작업을 수행하려면 `encryptionSpecs`. 필수 매개 변수가 강조 표시된 아래 요청 예를 참조하십시오.


>[!BEGINSHADEBOX]

+++ 클라우드 스토리지 대상에 대한 암호화 사양 보기

```json {line-numbers="true" start-line="1" highlight="26-27"}
           "encryptionSpecs": [
                {
                    "name": "File PGP/GPG Encryption",
                    "type": "FileAsymmetric",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines parameters required for capturing user's inputs for encryption",
                        "type": "object",
                        "properties": {
                            "publicKey": {
                                "description": "Base64 encoded RSA public key",
                                "type": "string",
                                "contentEncoding": "base64"
                            },
                            "encryptionAlgo": {
                                "description": "Algorithm for encryption.",
                                "type": "string",
                                "default": "PGPGPG",
                                "enum": [
                                    "PGPGPG",
                                    "NONE"
                                ]
                            }
                        },
                        "required": [
                            "encryptionAlgo",
                            "publicKey"
                        ]
                    }
                }
            ]
```

+++

**요청**

+++기본 연결에 암호화 추가 - 요청

추가 정보를 제공하는 요청 예제에서 인라인 주석이 있는 강조 표시된 줄을 확인합니다. 요청을 선택한 터미널에 복사 붙여넣을 때 인라인 주석을 제거합니다.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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
  "encryptionSpecs":{
     "specName": "Encryption spec",
     "params": {
         "encryptionAlgo":"PGPGPG",
         "publicKey":"<Add public key>"
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

+++기본 연결에 암호화 추가 - 응답

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

응답에서 연결 ID를 확인합니다. 이 ID는 대상 연결을 만들 때 다음 단계에서 필요합니다.

## 대상 연결 만들기 {#create-target-connection}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step4.png)

그런 다음 타겟 연결을 만들어야 합니다. [Target 연결](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 내보낸 대상에 대한 내보내기 매개 변수를 저장합니다. 내보내기 매개 변수에는 내보내기 위치, 파일 형식, 압축 및 기타 세부 사항이 포함됩니다. 예를 들어 CSV 파일의 경우 몇 가지 내보내기 옵션을 선택할 수 있습니다. 지원되는 모든 CSV 내보내기 옵션에 대한 광범위한 정보를 보려면 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md).

다음을 참조하십시오. `targetSpec` 대상에 제공된 속성 `connection spec` 각 대상 유형에 대해 지원되는 속성을 이해합니다. 다음 탭을 참조하십시오. `targetSpec` 지원되는 모든 대상의 속성입니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 대상 연결 매개 변수 표시

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 를 찾을 위치에 대한 추가 정보를 제공하는 아래 예 [!DNL target spec] 연결 사양의 매개변수. 아래 예제에서 대상 매개 변수를 확인할 수 있습니다. *아님* 대상 내보내기 대상에 적용할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { //describes the target connection parameters
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] 대상 연결 매개 변수 표시

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 를 찾을 위치에 대한 추가 정보를 제공하는 아래 예 [!DNL target spec] 연결 사양의 매개변수. 아래 예제에서 대상 매개 변수를 확인할 수 있습니다. *아님* 대상 내보내기 대상에 적용할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,44"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] 대상 연결 매개 변수 표시

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 를 찾을 위치에 대한 추가 정보를 제공하는 아래 예 [!DNL target spec] 연결 사양의 매개변수. 아래 예제에서 대상 매개 변수를 확인할 수 있습니다. *아님* 대상 내보내기 대상에 적용할 수 있습니다.

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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] 대상 연결 매개 변수 표시

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 를 찾을 위치에 대한 추가 정보를 제공하는 아래 예 [!DNL target spec] 연결 사양의 매개변수. 아래 예제에서 대상 매개 변수를 확인할 수 있습니다. *아님* 대상 내보내기 대상에 적용할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="9,36"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] 대상 연결 매개 변수 표시

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 를 찾을 위치에 대한 추가 정보를 제공하는 아래 예 [!DNL target spec] 연결 사양의 매개변수. 아래 예제에서 대상 매개 변수를 확인할 수 있습니다. *아님* 대상 내보내기 대상에 적용할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,44"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

+++SFTP - [!DNL Connection spec] 대상 연결 매개 변수 표시

인라인 메모가 있는 강조 표시된 줄을 [!DNL connection spec] 를 찾을 위치에 대한 추가 정보를 제공하는 아래 예 [!DNL target spec] 연결 사양의 매개변수. 아래 예제에서 대상 매개 변수를 확인할 수 있습니다. *아님* 대상 내보내기 대상에 적용할 수 있습니다.

```json {line-numbers="true" start-line="1" highlight="10,37"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [대상 세부 사항 입력](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 의 섹션 [!DNL Amazon S3] 대상 설명서 페이지.

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Amazon S3] - CSV 옵션을 사용하여 Target 연결 요청

>[!TIP]
>
>파일 내보내기에 사용할 수 있는 CSV 옵션에 대한 자세한 내용은 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Amazon S3 Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"4fce964d-3f37-408f-9778-e597338a21ee",
      "version":"1.0"
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
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [대상 세부 사항 입력](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) 의 섹션 [!DNL Azure Blob Storage] 대상 설명서 페이지.

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Blob Storage] - CSV 옵션을 사용하여 Target 연결 요청

>[!TIP]
>
>파일 내보내기에 사용할 수 있는 CSV 옵션에 대한 자세한 내용은 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Blob Storage Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
      "version":"1.0"
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

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Target 연결 요청

>[!TIP]
>
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [대상 세부 사항 입력](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) Azure의 섹션 [!DNL Data Lake Gen 2(ADLS Gen2)] 대상 설명서 페이지.

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - CSV 옵션을 사용하여 Target 연결 요청

>[!TIP]
>
>파일 내보내기에 사용할 수 있는 CSV 옵션에 대한 자세한 내용은 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Data Lake Gen 2(ADLS Gen2)",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"be2c3209-53bc-47e7-ab25-145db8b873e1",
      "version":"1.0"
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
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [대상 세부 사항 입력](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) 의 섹션 [!DNL Data Landing Zone] 대상 설명서 페이지.

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Data Landing Zone] - CSV 옵션을 사용하여 Target 연결 요청

>[!TIP]
>
>파일 내보내기에 사용할 수 있는 CSV 옵션에 대한 자세한 내용은 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Data Landing Zone Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"10440537-2a7b-4583-ac39-ed38d4b848e8",
      "version":"1.0"
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
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [대상 세부 사항 입력](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 의 섹션 [!DNL Google Cloud Storage] 대상 설명서 페이지.

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Google Cloud Storage] - CSV 옵션을 사용하여 Target 연결 요청

>[!TIP]
>
>파일 내보내기에 사용할 수 있는 CSV 옵션에 대한 자세한 내용은 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Google Cloud Storage Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"c5d93acb-ea8b-4b14-8f53-02138444ae99",
      "version":"1.0"
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
>필요한 대상 매개 변수를 얻는 방법에 대한 자세한 내용은 [대상 세부 사항 입력](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 섹션( SFTP 대상 설명서 페이지)

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

+++SFTP - CSV 옵션이 있는 Target 연결 요청

>[!TIP]
>
>파일 내보내기에 사용할 수 있는 CSV 옵션에 대한 자세한 내용은 [파일 형식 지정 구성 페이지](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"SFTP Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"36965a81-b1c6-401b-99f8-22508f1e6a26",
      "version":"1.0"
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

다음을 참고하십시오. `target connection ID` 응답. 이 ID는 대상자를 내보내기 위한 데이터 흐름을 만들 때 다음 단계에서 필수입니다.

성공적인 응답은 ID( )를 반환합니다.`id`)을 참조하십시오. `etag`. 대상 연결 ID는 나중에 데이터 흐름을 만들 때 필요하므로 기록해 두십시오.

## 데이터 흐름을 만듭니다 {#create-dataflow}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step5.png)

대상 구성의 다음 단계는 데이터 흐름을 만드는 것입니다. A [데이터 흐름](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 는 이전에 만든 엔티티를 결합하고 대상 내보내기 일정을 구성하는 옵션을 제공합니다. 데이터 흐름을 만들려면 원하는 클라우드 스토리지 대상에 따라 아래 페이로드를 사용하고 이전 단계의 흐름 엔티티 ID를 바꾸십시오. 이 단계에서는 속성 또는 ID 매핑과 관련된 정보를 데이터 흐름에 추가하지 않습니다. 이 작업은 다음 단계에서 수행합니다.

>[!BEGINTABS]

>[!TAB Amazon S3]

**요청**

+++대상 내보내기 데이터 흐름 만들기 [!DNL Amazon S3] 대상 - 요청

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
    "name": "Activate audiences to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "1a0514a6-33d4-4c7f-aff8-594799c47549", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
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

+++대상 내보내기 데이터 흐름 만들기 [!DNL Azure Blob Storage] 대상 - 요청

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
    "name": "Activate audiences to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "752d422f-b16f-4f0d-b1c6-26e448e3b388", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [
        {
        "name": "GeneralTransform",
        "params": {
            "mandatoryFields": [],
            "primaryFields": [],
            "profileMapping": {},
            "segmentSelectors": {
            "selectors": []
            }
        }
        }
    ]
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

+++대상 내보내기 데이터 흐름 만들기 [!DNL Azure Data Lake Gen 2(ADLS Gen2)] 대상 - 요청

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
    "name": "Activate audiences to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
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
    "transformations": []
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

+++대상 내보내기 데이터 흐름 만들기 [!DNL Data Landing Zone] 대상 - 요청

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
    "name": "Activate audiences to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to a Data Landing Zone cloud storage destination",
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
    "transformations": []
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

+++대상 내보내기 데이터 흐름 만들기 [!DNL Google Cloud Storage] 대상 - 요청

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
    "name": "Activate audiences to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to a Google Cloud Storage destination",
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
    "transformations": []
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

+++SFTP 대상으로 대상 내보내기 데이터 흐름 만들기 - 요청

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
    "name": "Activate audiences to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "fd36aaa4-bf2b-43fb-9387-43785eeeb799", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
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

응답에서 데이터 흐름 ID를 확인합니다. 이 ID는 이후 단계에서 필수입니다.

### 내보내기에 대상자 추가

이 단계에서는 대상으로 내보낼 대상을 선택할 수도 있습니다. 이 단계와 데이터 흐름에 대상을 추가하는 요청 형식에 대한 자세한 내용은 [대상 데이터 흐름 업데이트](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/patchFlowById) 섹션에 자세히 설명되어 있습니다.


## 속성 및 ID 매핑 설정 {#attribute-and-identity-mapping}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step6.png)

데이터 흐름을 만든 후 내보낼 속성 및 ID에 대한 매핑을 설정해야 합니다. 이 단계는 아래에 나열된 세 단계로 구성됩니다.

1. 입력 스키마 만들기
2. 출력 스키마 만들기
3. 생성된 스키마를 연결하도록 매핑 세트 설정

예를 들어 UI에 표시된 다음 매핑을 가져오려면 위에 나열되고 다음 제목에 자세히 설명된 세 단계를 거쳐야 합니다.

![매핑 단계의 예](/help/destinations/assets/api/file-based-segment-export/mapping-example.png)

### 입력 스키마 만들기

입력 스키마를 생성하려면 먼저 [유니온 스키마](/help/profile/ui/union-schema.md) 및 대상을 내보낼 수 있는 ID입니다. 소스 매핑으로 선택할 수 있는 속성 및 ID의 스키마입니다.

![소스 필드 선택 보기에서 속성 및 ID 옵션을 보여 주는 기록](/help/destinations/assets/api/file-based-segment-export/select-source-field.gif)

속성 및 ID를 검색하기 위한 요청 및 응답의 아래 예를 보십시오.

>[!BEGINSHADEBOX]

**속성 가져오기 요청**

+++공용 구조체 스키마에서 사용 가능한 속성 가져오기 - 요청

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/ups/config/entityTypes/_xdm.context.profile?property=fullSchema==true&property=includeRelationshipDescriptors==true' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**응답**

+++유니온 스키마에서 사용 가능한 속성 가져오기 - 응답

간결성을 위해 아래 응답이 짧아졌습니다.

```json
       "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:referencedFrom": [
                "https://ns.adobe.com/xdm/context/person"
            ],
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "meta:xdmType": "date",
                    "type": "string",
                    "format": "date",
                    "title": "Birth date(YYYY-MM-DD)",
                    "description": "The full date a person was born."
                },
                "birthDayAndMonth": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Birth date (MM-DD)",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year."
                },
                "birthYear": {
                    "meta:xdmType": "short",
                    "type": "integer",
                    "minimum": 1,
                    "maximum": 32767,
                    "title": "Birth year",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date."
                },
                "gender": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Gender",
                    "description": "Gender identity of the person.\n",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Non-specific"
                    },
                    "default": "not_specified"
                },
                "maritalStatus": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Marital Status",
                    "description": "Describes a person's relationship with a significant other.",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "divorced": "Divorced",
                        "not_specified": "Not Specified",
                        "married": "Married",
                        "single": "Single",
                        "widowed": "Widowed"
                    },
                    "default": "not_specified"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "meta:referencedFrom": [
                        "https://ns.adobe.com/xdm/context/person-name"
                    ],
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Courtesy title",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr."
                        },
                        "firstName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "First name",
                            "description": "The first audience of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "fullName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Full name",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name."
                        },
                        "lastName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Last name",
                            "description": "The last audience of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "middleName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Middle name",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name."
                        },
                        "suffix": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Suffix",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc."
                        }
                    }
                },
                "nationality": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Nationality",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code."
                },
                "taxId": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Tax ID",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated"
                },
                "type": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Type",
                    "description": "The type of individual in different business contexts like B2C."
                }
            }
        }
```

+++

>[!ENDSHADEBOX]



>[!BEGINSHADEBOX]

**ID 가져오기 요청**

+++매핑 단계에서 사용할 수 있는 사용 가능한 ID 가져오기

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/idnamespace/identities' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**응답**

+++ 입력 스키마에서 사용할 수 있는 ID 보기

이 응답은 입력 스키마를 만들 때 사용할 수 있는 ID를 반환합니다. 이 응답은 두 가지를 모두 반환합니다. [표준](/help/identity-service/namespaces.md#standard) 및 [사용자 정의](/help/identity-service/namespaces.md#manage-namespaces) Experience Platform에서 설정한 id 네임스페이스.

```json
[
    {
        "updateTime": 1551688425455,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "Adobe Audience Manger UUID",
        "id": 0,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "Adobe Experience Cloud ID",
        "id": 4,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "AdCloud",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email_LC_SHA256",
        "status": "ACTIVE",
        "description": "Email addresses need to be hashed using SHA256 and lowercased. Please also note that leading and trailing spaces need to be trimmed before an email address is normalized. You won't be able to change this setting later",
        "id": 11,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Emails (SHA256, lowercased)",
        "custom": false,
        "hashFunction": "SHA256",
        "transform": "lowercase"
    },
    {
        "updateTime": 1597996026101,
        "code": "Phone_E.164",
        "status": "ACTIVE",
        "description": "Namespace for raw phone numbers in E.164 format. + sign is required",
        "id": 17,
        "createTime": 1597996026101,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (E.164)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "GAID",
        "status": "ACTIVE",
        "description": "This datasource is associated to a Google Ad ID",
        "id": 20914,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Google Ad ID (GAID)",
        "custom": false
    },
    {
        "updateTime": 1476993749000,
        "code": "IDFA",
        "status": "ACTIVE",
        "description": "Apple ID for Advertisers. See: https://support.apple.com/en-us/HT202074 for more info.",
        "id": 20915,
        "createTime": 1476993749000,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Apple IDFA (ID for Advertisers)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AAID",
        "status": "ACTIVE",
        "description": "Adobe Analytics (Legacy ID)",
        "id": 10,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "Adobe Analytics (Legacy ID)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email",
        "status": "ACTIVE",
        "description": "Email",
        "id": 6,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Email",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "WAID",
        "status": "ACTIVE",
        "description": "Windows AID",
        "id": 8,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Windows AID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "TNTID",
        "status": "ACTIVE",
        "description": "Adobe Target (TNTID)",
        "id": 9,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "TNTID",
        "custom": false
    },
    {
        "updateTime": 1556676464714,
        "code": "Google",
        "status": "ACTIVE",
        "id": 771,
        "createTime": 1556676464714,
        "idType": "COOKIE",
        "namespaceType": "Integration",
        "name": "Google",
        "custom": false
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256_E.164",
        "status": "ACTIVE",
        "description": "Phone numbers need to be hashed using SHA256 without any dashes. Hash should be completed by customers on raw phone numbers in E.164 format. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 18,
        "createTime": 1604597776019,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256_E.164)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256",
        "status": "ACTIVE",
        "description": "Remove symbols, letters, and any leading zeroes before hashing. Prefix the country code before hashing. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 15,
        "createTime": 1597995542594,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1551688425455,
        "code": "Phone",
        "status": "ACTIVE",
        "description": "Phone",
        "id": 7,
        "createTime": 1551688425455,
        "idType": "PHONE_NUMBER",
        "namespaceType": "Standard",
        "name": "Phone",
        "custom": false
    }
]
```

+++

>[!ENDSHADEBOX]

다음으로, 위의 응답을 복사하여 입력 스키마를 만드는 데 사용해야 합니다. 위의 응답에서 전체 JSON 응답을 복사하여 `jsonSchema` 아래에 표시된 개체입니다.

>[!BEGINSHADEBOX]

**입력 스키마 만들기 요청**

+++입력 스키마 만들기 - 요청

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas/' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \ 
--header 'Content-Type: application/json' \ 
--data-raw '{
    "name":"Sample Schema for Flow Mapping",
    "jsonSchema":{...insert response from union schema response here}
    '
```

+++

**응답**

+++입력 스키마 만들기 - 응답

```json
{
   "id":"8db56468c2ab475dbf17c2621f92c0f8",
   "version":0,
   "jsonSchema":{
      "title":"XDM Individual Profile",
      "description":"An XDM Individual Profile forms a singular representation of the attributes and interests of both identified and partially-identified individuals. Less-identified profiles may contain only anonymous behavioral signals, such as browser cookies, while highly-identified profiles may contain detailed personal information such as name, date of birth, location, and email address. As a profile grows, it becomes a robust repository of personal information, identification information, contact details, and communication preferences for an individual.",
      "type":"object",
      "properties":{ // this section returns the contents that you have added to the jsonSchema object in the request
      }
   }
}
```

+++

>[!ENDSHADEBOX]

응답의 ID는 생성한 입력 스키마의 고유 식별자를 나타냅니다. 이후 단계에서 재사용할 예정이므로 응답에서 ID를 복사합니다.

### 출력 스키마 만들기

그런 다음 내보내기를 위해 출력 스키마를 설정해야 합니다. 먼저 기존 파트너 스키마를 찾아 검사해야 합니다.

>[!BEGINSHADEBOX]

**요청**

+++출력 스키마에 대한 파트너 스키마를 가져오도록 요청

아래 예제에서는 `connection spec ID` Amazon S3용 이 값을 대상에 대한 연결 사양 ID로 바꾸십시오.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**예제 스키마가 있는 응답**

Inspect 위의 호출을 수행할 때 받는 응답입니다. 응답을 드릴다운하여 객체를 찾아야 합니다 `targetSpec.attributes.partnerSchema.jsonSchema`

+++ 출력 스키마에 대한 파트너 스키마 가져오기 응답

```json
{
   "title":"defaultschema",
   "type":"object",
   "properties":{
      "attributes":{
         "type":"object",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "properties":{
               "value":{
                  "type":"string",
                  "title":"Value"
               }
            },
            "meta:xdmType":"object"
         }
      },
      "identityMap":{
         "type":"object",
         "meta:xdmField":"xdm:identityMap",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"array",
            "items":{
               "type":"object",
               "properties":{
                  "id":{
                     "type":"string",
                     "title":"Identifier",
                     "description":"Identity of the consumer in the related namespace.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:id"
                  },
                  "primary":{
                     "type":"boolean",
                     "title":"Primary",
                     "default":false,
                     "description":"Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                     "meta:xdmType":"boolean",
                     "meta:xdmField":"xdm:primary"
                  },
                  "authenticatedState":{
                     "enum":[
                        "ambiguous",
                        "authenticated",
                        "loggedOut"
                     ],
                     "type":"string",
                     "default":"ambiguous",
                     "meta:enum":{
                        "ambiguous":"Ambiguous",
                        "loggedOut":"User was identified by a login action at some point of time previously, but is not currently logged in.",
                        "authenticated":"User identified by a login or similar action that was valid at the time of the event observation."
                     },
                     "description":"The state this identity is authenticated as for this observed ExperienceEvent.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:authenticatedState"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/identityitem"
            },
            "meta:xdmType":"array"
         }
      },
      "segmentMembership":{
         "title":"Segment membership map",
         "type":"object",
         "meta:xdmField":"xdm:segmentMembership",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "title":"Segment membership per namespace",
            "meta:xdmType":"map",
            "additionalProperties":{
               "type":"object",
               "properties":{
                  "status":{
                     "enum":[
                        "realized",
                        "exited"
                     ],
                     "type":"string",
                     "title":"Status",
                     "default":"realized",
                     "meta:enum":{
                        "exited":"Entity is exiting the segment.",
                        "realized":"Entity is entering the segment."
                     },
                     "description":"Is the audience participation realized as part of the current request.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:status"
                  },
                  "payload":{
                     "type":"object",
                     "title":"Payload",
                     "required":[
                        "payloadType"
                     ],
                     "properties":{
                        "payloadType":{
                           "enum":[
                              "boolean",
                              "number",
                              "propensity",
                              "string"
                           ],
                           "type":"string",
                           "title":"Payload Type",
                           "meta:enum":{
                              "number":"Number",
                              "string":"String",
                              "boolean":"Boolean",
                              "propensity":"Propensity"
                           },
                           "description":"The type of payload.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadType"
                        },
                        "payloadNumberValue":{
                           "type":"number",
                           "title":"Value",
                           "description":"The number.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadNumberValue"
                        },
                        "payloadStringValue":{
                           "type":"string",
                           "title":"Value",
                           "description":"The string value.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadStringValue"
                        },
                        "payloadBooleanValue":{
                           "type":"boolean",
                           "title":"Value",
                           "description":"The boolean value.",
                           "meta:xdmType":"boolean",
                           "meta:xdmField":"xdm:payloadBooleanValue"
                        },
                        "payloadPropensityValue":{
                           "type":"number",
                           "title":"Value",
                           "maximum":1,
                           "description":"The propensity.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadPropensityValue",
                           "exclusiveMinimum":0
                        }
                     },
                     "description":"Values that are directly related with the audience realization. This payload exists with the same 'validUntil' as the audience realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:payload"
                  },
                  "version":{
                     "type":"string",
                     "title":"Version",
                     "description":"The version of the audience definition used in this audience assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:version"
                  },
                  "segmentID":{
                     "type":"object",
                     "title":"Segment ID",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the audience in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "description":"The identity of the audience or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                     "meta:status":"deprecated",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:segmentID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentidentity"
                  },
                  "validUntil":{
                     "type":"string",
                     "title":"Valid until",
                     "format":"date-time",
                     "description":"The timestamp for when the audienceassertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:validUntil"
                  },
                  "profileStitchID":{
                     "type":"object",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the profile stitch in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:profileStitchID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/profileStitchIdentity"
                  },
                  "lastQualificationTime":{
                     "type":"string",
                     "title":"Last qualification time",
                     "format":"date-time",
                     "description":"The timestamp when the assertion of audience membership was made.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:lastQualificationTime"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentmembership"
            }
         }
      }
   }
}
```

+++

>[!ENDSHADEBOX]

그런 다음 출력 스키마를 만들어야 합니다. 위에 표시된 JSON 응답을 복사하여 `jsonSchema` 아래에 있는 개체입니다.

>[!BEGINSHADEBOX]

**요청**

+++출력 스키마 만들기 - 요청

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Sample Schema for Flow Mapping",
"jsonSchema":{...insert JSON from the response above here}
}
'
```

+++

**응답**

+++출력 스키마 만들기 - 응답

```json
{
    "id": "2f4fd51934c1409fb1d8207dd9f43dc9",
    "version": 0,
    "jsonSchema": {
        "title": "defaultschema",
        "type": "object",
        "properties": {
            "identityMap": {
                "type": "object",
                "meta:xdmField": "xdm:identityMap",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "meta:xdmType": "array",
                    "items": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                        "properties": {
                            "primary": {
                                "meta:xdmField": "xdm:primary",
                                "meta:xdmType": "boolean",
                                "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                                "default": false,
                                "type": "boolean",
                                "title": "Primary"
                            },
                            "id": {
                                "meta:xdmField": "xdm:id",
                                "meta:xdmType": "string",
                                "description": "Identity of the consumer in the related namespace.",
                                "type": "string",
                                "title": "Identifier"
                            },
                            "authenticatedState": {
                                "meta:xdmField": "xdm:authenticatedState",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in.",
                                    "authenticated": "User identified by a login or similar action that was valid at the time of the event observation.",
                                    "ambiguous": "Ambiguous"
                                },
                                "enum": [
                                    "ambiguous",
                                    "authenticated",
                                    "loggedOut"
                                ],
                                "default": "ambiguous",
                                "type": "string",
                                "description": "The state this identity is authenticated as for this observed ExperienceEvent."
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "type": "array"
                }
            },
            "segmentMembership": {
                "title": "Segment membership map",
                "type": "object",
                "meta:xdmField": "xdm:segmentMembership",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "additionalProperties": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentmembership",
                        "properties": {
                            "version": {
                                "meta:xdmField": "xdm:version",
                                "meta:xdmType": "string",
                                "description": "The version of the audience definition used in this audience assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                                "type": "string",
                                "title": "Version"
                            },
                            "validUntil": {
                                "meta:xdmField": "xdm:validUntil",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp for when the audienceassertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Valid until"
                            },
                            "status": {
                                "meta:xdmField": "xdm:status",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "exited": "Entity is exiting the segment.",
                                    "realized": "Entity is entering the segment."
                                },
                                "enum": [
                                    "realized",
                                    "exited"
                                ],
                                "default": "realized",
                                "description": "Is the audience participation realized as part of the current request.",
                                "type": "string",
                                "title": "Status"
                            },
                            "segmentID": {
                                "meta:xdmField": "xdm:segmentID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentidentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the audience in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object",
                                "description": "The identity of the audience or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                                "meta:status": "deprecated",
                                "title": "Segment ID"
                            },
                            "profileStitchID": {
                                "meta:xdmField": "xdm:profileStitchID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/profileStitchIdentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the profile stitch in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object"
                            },
                            "payload": {
                                "meta:xdmField": "xdm:payload",
                                "meta:xdmType": "object",
                                "required": [
                                    "payloadType"
                                ],
                                "properties": {
                                    "payloadType": {
                                        "meta:xdmField": "xdm:payloadType",
                                        "meta:xdmType": "string",
                                        "description": "The type of payload.",
                                        "meta:enum": {
                                            "string": "String",
                                            "propensity": "Propensity",
                                            "number": "Number",
                                            "boolean": "Boolean"
                                        },
                                        "enum": [
                                            "boolean",
                                            "number",
                                            "propensity",
                                            "string"
                                        ],
                                        "type": "string",
                                        "title": "Payload Type"
                                    },
                                    "payloadStringValue": {
                                        "meta:xdmField": "xdm:payloadStringValue",
                                        "meta:xdmType": "string",
                                        "description": "The string value.",
                                        "type": "string",
                                        "title": "Value"
                                    },
                                    "payloadPropensityValue": {
                                        "meta:xdmField": "xdm:payloadPropensityValue",
                                        "meta:xdmType": "number",
                                        "maximum": 1,
                                        "exclusiveMinimum": 0,
                                        "description": "The propensity.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadNumberValue": {
                                        "meta:xdmField": "xdm:payloadNumberValue",
                                        "meta:xdmType": "number",
                                        "description": "The number.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadBooleanValue": {
                                        "meta:xdmField": "xdm:payloadBooleanValue",
                                        "meta:xdmType": "boolean",
                                        "description": "The boolean value.",
                                        "type": "boolean",
                                        "title": "Value"
                                    }
                                },
                                "type": "object",
                                "description": "Values that are directly related with the audience realization. This payload exists with the same 'validUntil' as the audience realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                                "title": "Payload"
                            },
                            "lastQualificationTime": {
                                "meta:xdmField": "xdm:lastQualificationTime",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp when the assertion of audience membership was made.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Last qualification time"
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "meta:xdmType": "map",
                    "type": "object",
                    "title": "Segment membership per namespace"
                }
            },
            "attributes": {
                "type": "object",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "properties": {
                        "value": {
                            "type": "string",
                            "title": "Value"
                        }
                    },
                    "meta:xdmType": "object",
                    "type": "object"
                }
            },
            "firstName": {
                "title": "firstName",
                "type": "string"
            },
            "Email": {
                "title": "Email",
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "id",
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                },
                "meta:xdmType": "array"
            }
        }
    }
}
```

응답의 ID는 생성한 입력 스키마의 고유 식별자를 나타냅니다. 이후 단계에서 재사용할 예정이므로 응답에서 ID를 복사합니다.

>[!ENDSHADEBOX]

### 매핑 세트 만들기 {#create-mapping-set}

그런 다음 를 사용합니다. [데이터 준비 API](https://developer.adobe.com/experience-platform-apis/references/data-prep/#tag/Mapping-sets/operation/createMappingSet) 입력 스키마 ID, 출력 스키마 ID 및 원하는 필드 매핑을 사용하여 매핑 세트를 만듭니다.

>[!BEGINSHADEBOX]

**요청**

+++매핑 세트 만들기 - 요청

>[!IMPORTANT]
>
>* 아래 표시된 매핑 개체에서 `destination` 매개 변수에서 점을 허용하지 않음 `"."`. 예를 들어 구성 예제에서 강조 표시된 대로 personalEmail_address 또는 segmentMembership_status를 사용해야 합니다.
>* 소스 속성이 ID 속성이고 점을 포함하는 특별한 경우가 있습니다. 이 경우 속성은 로 이스케이프해야 합니다. `//`아래에 강조 표시된 대로.
>* 또한 아래 예제 구성에는 `Email` 및 `Phone_E.164`, 데이터 흐름당 하나의 id 속성만 내보낼 수 있습니다.

```shell {line-numbers="true" start-line="1" highlight="16-38"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputSchema": {
        "id": "81d7fc5376e54eb58d5186fd30d5a8c9"
    },  
    "outputSchema": {
        "id": "2f4fd51934c1409fb1d8207dd9f43dc9"
    },
    "mappings": [
        {
            "destination": "firstName",
            "source": "person.name.firstName",
            "sourceType": "ATTRIBUTE"
        }, 
        {
            "destination": "Email",
            "source": "identityMap.Email",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "Phone_E_164",
            "source": "identityMap.Phone_E//.164",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "personalEmail_address",
            "source": "personalEmail.address",
            "sourceType": "ATTRIBUTE"
        },        
        {
            "destination": "segmentMembership_status",
            "source": "segmentMembership.ups.seg_id.status",
            "sourceType": "ATTRIBUTE"
        }        
    ],
    "xdmVersion": "1.0"
}'
```

+++

**응답**

+++ 매핑 세트 만들기 - 응답

```json
{
    "id": "5f0031f8ccd4444dac9c5c391389e9e8",
    "version": 0,
    "createdDate": 1678999005197,
    "modifiedDate": 1678999005197,
    "createdBy": "example@AdobeID",
    "modifiedBy": "example@AdobeID"
}
```

+++

>[!ENDSHADEBOX]

매핑 세트 ID로 기존 데이터 흐름을 업데이트하려면 다음 단계에서 필요하므로 매핑 세트의 ID를 참고하십시오.

그런 다음 업데이트할 데이터 흐름의 ID를 가져옵니다.

>[!BEGINSHADEBOX]

다음을 참조하십시오 [대상 데이터 흐름의 세부 정보 검색](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/getFlowById) 데이터 흐름의 ID 검색에 대한 정보입니다.

>[!ENDSHADEBOX]

마지막으로 방금 만든 매핑 세트 정보로 데이터 흐름을 PATCH 해야 합니다.

>[!BEGINSHADEBOX]

**요청**

+++ 매핑 세트 정보로 데이터 흐름 업데이트 - 요청

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/df8245a8-dd8f-42da-a04a-2d3a92654d9e' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: ETAG_HERE' \
--data-raw '[
   {
      "op":"ADD",
      "path":"/transformations/0/params/profileMapping",
      "value":{
         "mappingId":"304ca6a2fff244949c956cad1cd9eae6",
         "mappingVersion":0
      }
   }
]'
```

+++

**응답**

+++ 매핑 세트 정보로 데이터 흐름 업데이트 - 응답

흐름 서비스 API의 응답은 업데이트된 데이터 흐름의 ID를 반환합니다.

```json
{
    "id": "1c246ae4-ba0d-43cd-a0ec-f16fe0a56b55",
    "etag": "\"1500c67f-0000-0200-0000-64137ee00000\""
}
```

+++

>[!ENDSHADEBOX]

## 다른 데이터 흐름 업데이트 {#other-dataflow-updates}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step7.png)

데이터 흐름을 업데이트하려면 `PATCH` 예를들어 데이터 흐름을 업데이트하여 필드를 필수 키 또는 중복 제거 키로 선택할 수 있습니다.

### 필수 키 추가 {#add-mandatory-key}

을(를) 추가하려면 [필수 키](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes), 아래의 요청 및 응답 예 를 참조하십시오

>[!BEGINSHADEBOX]

**요청**

+++필수 필드로 ID 추가 - 요청

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

+++XDM 속성을 필수 필드로 추가 - 요청

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

**응답**

+++필수 필드 추가 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### 중복 제거 키 추가 {#add-deduplication-key}

을(를) 추가하려면 [중복 제거 키](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys), 아래의 요청 및 응답 예 를 참조하십시오

>[!BEGINSHADEBOX]

**요청**

+++ID를 중복 제거 키로 추가 - 요청

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

+++XDM 속성을 중복 제거 키로 추가 - 요청

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

**응답**

+++필수 필드 추가 - 응답

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

## 데이터 흐름 유효성 검사(데이터 흐름 실행 가져오기) {#get-dataflow-runs}

![사용자가 진행 중인 현재 단계를 강조 표시하는 대상을 활성화하는 단계](/help/destinations/assets/api/file-based-segment-export/step8.png)

데이터 흐름 실행을 확인하려면 데이터 흐름 실행 API를 사용하십시오.

>[!BEGINSHADEBOX]

**요청**

+++데이터 흐름 실행 가져오기 - 요청

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw ''
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

다음에 대한 정보를 찾을 수 있습니다. [데이터 흐름에서 반환된 다양한 매개 변수는 API를 실행합니다.](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) API 참조 설명서에서 참조하십시오.

## API 오류 처리 {#api-error-handling}

이 자습서의 API 끝점은 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](/help/landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](/help/landing/troubleshooting.md#request-header-errors) 오류 응답 해석에 대한 자세한 내용은 플랫폼 문제 해결 안내서를 참조하십시오.

## 다음 단계 {#next-steps}

이 자습서에 따라 선호하는 클라우드 스토리지 대상 중 하나에 플랫폼을 연결하고 대상을 내보내도록 각 대상에 데이터 흐름을 설정했습니다. 흐름 서비스 API를 사용하여 기존 데이터 흐름을 편집하는 방법과 같은 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
* [흐름 서비스 API를 사용하여 대상 데이터 흐름 업데이트](../api/update-destination-dataflows.md)
