---
title: 데이터 랜딩 영역 대상
description: 데이터 랜딩 영역에 연결하여 대상자를 활성화하고 데이터 세트를 내보내는 방법을 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: cc7c8c14fe5ee4bb9001cae84d28a385a3b4b448
workflow-type: tm+mt
source-wordcount: '1956'
ht-degree: 2%

---

# 데이터 랜딩 영역 대상

>[!IMPORTANT]
>
>이 설명서 페이지는 [!DNL Data Landing Zone] *대상*&#x200B;을(를) 참조합니다. 소스 카탈로그에 [!DNL Data Landing Zone] *source*&#x200B;도 있습니다. 자세한 내용은 [[!DNL Data Landing Zone] 소스](/help/sources/connectors/cloud-storage/data-landing-zone.md) 설명서를 참조하십시오.


## 개요 {#overview}

[!DNL Data Landing Zone]은(는) Adobe Experience Platform에서 프로비저닝한 클라우드 스토리지 인터페이스로, 플랫폼 밖으로 파일을 내보낼 수 있는 안전한 클라우드 기반 파일 스토리지 기능에 대한 액세스 권한을 부여합니다. 샌드박스당 하나의 [!DNL Data Landing Zone] 컨테이너에 액세스할 수 있으며 모든 컨테이너의 총 데이터 볼륨은 Platform 제품 및 서비스 라이선스와 함께 제공되는 총 데이터로 제한됩니다. [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] 및 [!DNL Real-Time Customer Data Platform]과(와) 같은 플랫폼과 해당 애플리케이션의 모든 고객에게 샌드박스당 하나의 [!DNL Data Landing Zone] 컨테이너가 제공됩니다.

플랫폼은 [!DNL Data Landing Zone] 컨테이너에 업로드된 모든 파일에 엄격한 7일 TTL(time-to-live)을 적용합니다. 모든 파일은 7일 후에 삭제됩니다.

[!DNL Data Landing Zone] 대상 커넥터는 Azure 또는 Amazon 웹 서비스 클라우드 지원을 사용하는 고객에게 제공됩니다. 인증 메커니즘은 대상이 프로비저닝된 클라우드에 따라 다르며, 대상 및 해당 사용 사례에 대한 다른 모든 것은 동일합니다. [Azure Blob에 제공된 데이터 랜딩 영역 인증] 및 [AWS에 제공된 데이터 랜딩 영역 인증](#authenticate-dlz-aws) 섹션에서 두 가지 다른 인증 메커니즘에 대해 자세히 알아보십시오.

![클라우드 지원에 따라 데이터 랜딩 영역 대상의 구현이 어떻게 다른지를 보여 주는 다이어그램입니다.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png)

## API 또는 UI를 통해 [!UICONTROL 데이터 랜딩 영역] 저장소에 연결합니다. {#connect-api-or-ui}

* 플랫폼 사용자 인터페이스를 사용하여 [!UICONTROL 데이터 랜딩 영역] 저장소 위치에 연결하려면 아래의 [대상에 연결](#connect) 및 [이 대상에 대상 활성화](#activate) 섹션을 읽어 보십시오.
* 프로그래밍 방식으로 [!UICONTROL 데이터 랜딩 영역] 저장소 위치에 연결하려면 흐름 서비스 API 자습서를 사용하여 [파일 기반 대상에 대상 활성화](../../api/activate-segments-file-based-destinations.md)를 읽어 보십시오.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ 덧신 | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드(예: PPID)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* [플랫폼 사용자 인터페이스를 사용하여 데이터 세트를 내보내는 방법](/help/destinations/ui/export-datasets.md).
* 흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트를 [내보내는 방법](/help/destinations/api/export-datasets.md).

## 내보낸 데이터의 파일 형식 {#file-format}

*대상 데이터*&#x200B;를 내보낼 때 Platform은 사용자가 제공한 저장소 위치에 `.csv`, `parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 대상 활성화 자습서에서 [내보내기에 지원되는 파일 형식](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) 섹션을 참조하십시오.

*데이터 세트*&#x200B;를 내보낼 때 Platform은 사용자가 제공한 저장소 위치에 `.parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 데이터 세트 내보내기 자습서에서 [데이터 세트 내보내기에 성공했는지 확인](../../ui/export-datasets.md#verify) 섹션을 참조하십시오.

## Azure Blob에 프로비저닝된 데이터 랜딩 영역 인증 {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>이 섹션은 Microsoft Azure에서 실행되는 Experience Platform 구현에 적용됩니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)를 참조하세요.

[!DNL Azure Storage Explorer] 또는 명령줄 인터페이스를 통해 컨테이너에 파일을 읽고 쓸 수 있습니다.

[!DNL Data Landing Zone]은(는) SAS 기반 인증을 지원하며, 전송 중이거나 사용하지 않는 표준 [!DNL Azure Blob] 저장소 보안 메커니즘을 통해 데이터를 보호합니다. SAS는 [공유 액세스 서명](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers)을 의미합니다.

SAS 기반 인증을 사용하면 공용 인터넷 연결을 통해 [!DNL Data Landing Zone] 컨테이너에 안전하게 액세스할 수 있습니다. [!DNL Data Landing Zone] 컨테이너에 액세스하는 데 필요한 네트워크 변경 내용이 없습니다. 따라서 네트워크에 대한 허용 목록 또는 교차 지역 설정을 구성할 필요가 없습니다.

### [!DNL Data Landing Zone] 컨테이너를 [!DNL Azure Storage Explorer]에 연결

[[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/)을(를) 사용하여 [!DNL Data Landing Zone] 컨테이너의 콘텐츠를 관리할 수 있습니다. [!DNL Data Landing Zone]을(를) 사용하려면 먼저 자격 증명을 검색하고 [!DNL Azure Storage Explorer]에 입력한 다음 [!DNL Data Landing Zone] 컨테이너를 [!DNL Azure Storage Explorer]에 연결해야 합니다.

[!DNL Azure Storage Explorer] UI의 왼쪽 탐색 막대에서 연결 아이콘을 선택합니다. 연결할 수 있는 옵션을 제공하는 **리소스 선택** 창이 나타납니다. [!DNL Data Landing Zone] 저장소에 연결하려면 **[!DNL Blob container]**&#x200B;을(를) 선택하십시오.

![Azure UI에서 강조 표시된 리소스를 선택하십시오.](/help/sources/images/tutorials/create/dlz/select-resource.png)

다음으로 연결 방법으로 **SAS(공유 액세스 서명 URL)**&#x200B;을(를) 선택한 후 **다음**&#x200B;을(를) 선택합니다.

![Azure UI에서 강조 표시된 연결 방법을 선택하십시오.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

연결 방법을 선택한 후 [!DNL Data Landing Zone] 컨테이너에 해당하는 **표시 이름** 및 **[!DNL Blob]컨테이너 SAS URL**&#x200B;을(를) 제공해야 합니다.

>[!BEGINSHADEBOX]

### [!DNL Data Landing Zone]에 대한 자격 증명을 검색합니다. {#retrieve-dlz-credentials}

[!DNL Data Landing Zone] 자격 증명을 검색하려면 플랫폼 API를 사용해야 합니다. 자격 증명을 검색하기 위한 API 호출에 대해서는 아래에 설명되어 있습니다. 헤더에 필요한 값을 가져오는 방법에 대한 자세한 내용은 [Adobe Experience Platform API 시작하기](/help/landing/api-guide.md) 안내서를 참조하십시오.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `dlz_destination` | `dlz_destination` 형식을 사용하면 API에서 랜딩 영역 대상 컨테이너와 사용 가능한 다른 형식의 컨테이너를 구별할 수 있습니다. |

{style="table-layout:auto"}

**요청**

다음 요청 예제는 기존 랜딩 영역에 대한 자격 증명을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**응답**

다음 응답은 랜딩 영역의 자격 증명 정보를 반환합니다. 여기에는 현재 `SASToken` 및 `SASUri`과(와) 랜딩 영역 컨테이너에 해당하는 `storageAccountName`이(가) 포함됩니다.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | 랜딩 영역의 이름입니다. |
| `SASToken` | 랜딩 영역에 대한 공유 액세스 서명 토큰입니다. 이 문자열에는 요청을 승인하는 데 필요한 모든 정보가 포함되어 있습니다. |
| `SASUri` | 랜딩 영역에 대한 공유 액세스 서명 URI입니다. 이 문자열은 인증 중인 랜딩 영역에 대한 URI와 해당 SAS 토큰의 조합입니다. |

{style="table-layout:auto"}

### [!DNL Data Landing Zone] 자격 증명 업데이트 {#update-dlz-credentials}

원할 경우 자격 증명을 새로 고칠 수도 있습니다. [!DNL Connectors] API의 `/credentials` 끝점에 POST 요청을 하여 `SASToken`을(를) 업데이트할 수 있습니다.

**API 형식**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `dlz_destination` | `dlz_destination` 형식을 사용하면 API에서 랜딩 영역 대상 컨테이너와 사용 가능한 다른 형식의 컨테이너를 구별할 수 있습니다. |
| `refresh` | `refresh` 동작을 사용하면 랜딩 영역 자격 증명을 재설정하고 새 `SASToken`을(를) 자동으로 생성할 수 있습니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 랜딩 영역 자격 증명을 업데이트합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**응답**

다음 응답은 `SASToken` 및 `SASUri`에 대해 업데이트된 값을 반환합니다.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

위에서 설명한 API 호출에서 반환된 대로 표시 이름(`containerName`)과 [!DNL Data Landing Zone] SAS URL을 입력한 다음 **다음**&#x200B;을 선택합니다.

![Azure UI에서 강조 표시된 연결 정보를 입력하세요.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

[!DNL Blob] 끝점 및 사용 권한에 대한 정보를 포함하여 설정에 대한 개요를 제공하는 **요약** 창이 나타납니다. 준비가 되면 **연결**&#x200B;을 선택합니다.

![Azure UI에 표시된 설정 요약입니다.](/help/sources/images/tutorials/create/dlz/summary.png)

연결에 성공하면 [!DNL Azure Storage Explorer] UI가 [!DNL Data Landing Zone] 컨테이너로 업데이트됩니다.

![Azure UI에서 강조 표시된 DLZ 사용자 컨테이너의 요약입니다.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

[!DNL Data Landing Zone] 컨테이너를 [!DNL Azure Storage Explorer]에 연결하면 이제 Experience Platform에서 [!DNL Data Landing Zone] 컨테이너로 파일을 내보낼 수 있습니다. 파일을 내보내려면 아래 섹션에 설명된 대로 Experience Platform UI에서 [!DNL Data Landing Zone] 대상에 대한 연결을 설정해야 합니다.

## AWS에서 프로비저닝한 데이터 랜딩 영역 인증 {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. 현재 AWS에서 실행 중인 Experience Platform은 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)를 참조하세요.

AWS에 프로비저닝된 데이터 랜딩 영역 인스턴스에 대한 자격 증명을 가져오려면 아래 작업을 수행하십시오. 그런 다음 원하는 클라이언트를 사용하여 데이터 랜딩 영역 인스턴스에 연결합니다.

>[!BEGINSHADEBOX]

### [!DNL Data Landing Zone]에 대한 자격 증명을 검색합니다. {#retrieve-dlz-credentials-aws}

[!DNL Data Landing Zone] 자격 증명을 검색하려면 플랫폼 API를 사용해야 합니다. 자격 증명을 검색하기 위한 API 호출에 대해서는 아래에 설명되어 있습니다. 헤더에 필요한 값을 가져오는 방법에 대한 자세한 내용은 [Adobe Experience Platform API 시작하기](/help/landing/api-guide.md) 안내서를 참조하십시오.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `dlz_destination` | `dlz_destination` 형식을 사용하면 API에서 랜딩 영역 대상 컨테이너와 사용 가능한 다른 형식의 컨테이너를 구별할 수 있습니다. |

{style="table-layout:auto"}

**요청**

다음 요청 예제는 기존 랜딩 영역에 대한 자격 증명을 검색합니다.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**응답**

다음 응답은 현재 `awsAccessKeyId`, `awsSecretAccessKey` 및 기타 정보를 포함하여 랜딩 영역에 대한 자격 증명 정보를 반환합니다.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| 속성 | 설명 |
| --- | --- |
| `credentials` | 이 개체에는 Experience Platform이 파일을 프로비전된 데이터 랜딩 영역 위치로 내보내는 데 사용하는 `awsAccessKeyId`, `awsSecretAccessKey` 및 `awsSessionToken`이(가) 포함됩니다. |
| `dlzPath` | 이 개체에는 내보낸 파일이 저장되는 Adobe 프로비저닝 AWS 위치의 경로가 포함됩니다. |
| `dlzProvider` | Amazon S3에서 프로비저닝한 데이터 랜딩 영역임을 나타냅니다. |
| `expiryTime` | 위의 개체에 있는 자격 증명이 만료되는 시기를 나타냅니다. 다시 호출하여 새로 고칠 수 있습니다. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

[필수 구성 요소](#prerequisites) 섹션에 설명된 대로 [!DNL Data Landing Zone] 컨테이너를 [!DNL Azure Storage Explorer]에 연결했는지 확인하십시오. [!DNL Data Landing Zone]은(는) Adobe이 프로비전된 저장소이므로 Experience Platform UI에서 대상을 인증하기 위해 더 이상 단계를 수행할 필요가 없습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력하십시오.
* **[!UICONTROL 파일 형식]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택하십시오. [!UICONTROL CSV] 옵션을 선택할 때 [파일 서식 옵션을 구성](../../ui/batch-destinations-file-formatting-options.md)할 수도 있습니다.
* Experience Platform **[!UICONTROL 압축 형식]**: 내보낸 파일에 사용할 압축 형식을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜십시오. 매니페스트의 이름은 `manifest-<<destinationId>>-<<dataflowRunId>>.json` 형식을 사용하여 지정합니다. [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)을(를) 봅니다. 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: 내보낸 파일을 생성한 [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장된 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 일정 조정

**[!UICONTROL 예약]** 단계에서 [!DNL Data Landing Zone] 대상에 대해 [내보내기 일정을 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)할 수 있으며 [내보낸 파일의 이름을 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)할 수도 있습니다.

### 속성 및 ID 매핑 {#map}

**[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 특성 및 ID 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 일괄 처리 대상 활성화 UI 자습서에서 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 참조하십시오.

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Data Landing Zone] 저장소를 확인하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인하십시오.
