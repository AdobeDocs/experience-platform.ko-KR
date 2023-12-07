---
title: 데이터 랜딩 영역 대상
description: 데이터 랜딩 영역에 연결하여 대상자를 활성화하고 데이터 세트를 내보내는 방법을 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 8c08b3d62d58d061f62c3b0abb23de0d826e3985
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 3%

---

# 데이터 랜딩 영역 대상

>[!IMPORTANT]
>
>이 설명서 페이지는 다음을 참조합니다. [!DNL Data Landing Zone] *대상*. 다음 항목도 있습니다 [!DNL Data Landing Zone] *소스* 소스 카탈로그에서. 자세한 내용은 [[!DNL Data Landing Zone] 소스](/help/sources/connectors/cloud-storage/data-landing-zone.md) 설명서를 참조하십시오.


## 개요 {#overview}

[!DNL Data Landing Zone]은 Adobe Experience Platform에 의해 프로비저닝된 [!DNL Azure Blob] 스토리지 인터페이스로, 이를 통해 안전한 클라우드 기반 파일 스토리지 시설에 액세스하여 Platform에서 파일을 내보낼 수 있습니다. 액세스 권한이 있습니다. [!DNL Data Landing Zone] 샌드박스당 컨테이너 및 모든 컨테이너의 총 데이터 볼륨은 Platform 제품 및 서비스 라이선스와 함께 제공되는 총 데이터로 제한됩니다. Platform 및 해당 애플리케이션 서비스의 모든 고객: [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], 및 [!DNL Real-Time Customer Data Platform] 이(가) 하나로 프로비저닝됨 [!DNL Data Landing Zone] 샌드박스당 컨테이너. 다음을 통해 컨테이너에 파일을 읽고 쓸 수 있습니다. [!DNL Azure Storage Explorer] 또는 명령줄 인터페이스입니다.

[!DNL Data Landing Zone] 는 SAS 기반 인증을 지원하며 데이터는 표준으로 보호됩니다 [!DNL Azure Blob] 중단 및 전송 중인 스토리지 보안 메커니즘. SAS 기반 인증을 통해 [!DNL Data Landing Zone] 공용 인터넷 연결을 통한 컨테이너. 에 액세스하는 데 필요한 네트워크 변경 사항이 없습니다. [!DNL Data Landing Zone] 즉, 네트워크에 대한 허용 목록 또는 교차 영역 설정을 구성할 필요가 없습니다.

Platform은에 업로드된 모든 파일에 엄격한 7일 TTL(time-to-live)을 적용합니다. [!DNL Data Landing Zone] 컨테이너. 모든 파일은 7일 후에 삭제됩니다.

## 다음에 연결 [!UICONTROL 데이터 랜딩 영역] API 또는 UI를 통한 스토리지 {#connect-api-or-ui}

* 에 연결하려면 [!UICONTROL 데이터 랜딩 영역] 플랫폼 사용자 인터페이스를 사용한 저장소 위치에서 섹션을 읽습니다. [대상에 연결](#connect) 및 [이 대상에 대상자 활성화](#activate) 아래요.
* 에 연결하려면 [!UICONTROL 데이터 랜딩 영역] 저장소 위치를 프로그래밍 방식으로 읽고 [흐름 서비스 API 튜토리얼을 사용하여 파일 기반 대상에 대한 대상자 활성화](../../api/activate-segments-file-based-destinations.md).

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드(예: PPID)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

다음을 사용하려면 먼저 다음 전제 조건을 충족해야 합니다. [!DNL Data Landing Zone] 대상.

### 연결 [!DNL Data Landing Zone] 컨테이너 대상 [!DNL Azure Storage Explorer]

다음을 사용할 수 있습니다. [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) 의 콘텐츠를 관리하려면 [!DNL Data Landing Zone] 컨테이너. 을(를) 사용하려면 [!DNL Data Landing Zone], 먼저 자격 증명을 검색하여 입력해야 합니다. [!DNL Azure Storage Explorer]및 다음을 연결합니다. [!DNL Data Landing Zone] 컨테이너 대상 [!DNL Azure Storage Explorer].

다음에서 [!DNL Azure Storage Explorer] UI에서 왼쪽 탐색 막대에 있는 연결 아이콘을 선택합니다. 다음 **리소스 선택** 연결 옵션을 제공하는 창이 나타납니다. 선택 **[!DNL Blob container]** 을(를) 통해 [!DNL Data Landing Zone] 스토리지.

![Azure UI에서 강조 표시된 리소스를 선택합니다.](/help/sources/images/tutorials/create/dlz/select-resource.png)

그런 다음 을 선택합니다. **SAS(공유 액세스 서명 URL)** 을 연결 방법으로 선택한 다음 을 선택합니다. **다음**.

![Azure UI에서 강조 표시된 연결 방법을 선택하십시오.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

연결 방법을 선택한 후 다음을 제공해야 합니다 **표시 이름** 및 **[!DNL Blob]컨테이너 SAS URL** 에 해당하는 [!DNL Data Landing Zone] 컨테이너.

>[!BEGINSHADEBOX]

### 에 대한 자격 증명 검색 [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

플랫폼 API를 사용하여 을(를) 검색해야 합니다. [!DNL Data Landing Zone] 자격 증명. 자격 증명을 검색하기 위한 API 호출에 대해서는 아래에 설명되어 있습니다. 머리글에 필요한 값을 가져오는 방법에 대한 자세한 내용은 [Adobe Experience Platform API 시작하기](/help/landing/api-guide.md) 가이드.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `dlz_destination` | 다음 `dlz_destination` 유형 을 사용하면 API에서 랜딩 영역 대상 컨테이너를 사용 가능한 다른 유형의 컨테이너와 구별할 수 있습니다. |

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

다음 응답은 현재 위치를 포함하여 랜딩 영역에 대한 자격 증명 정보를 반환합니다 `SASToken` 및 `SASUri`및 `storageAccountName` 랜딩 영역 컨테이너에 해당합니다.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | 랜딩 영역의 이름입니다. |
| `SASToken` | 랜딩 영역에 대한 공유 액세스 서명 토큰입니다. 이 문자열에는 요청을 승인하는 데 필요한 모든 정보가 포함되어 있습니다. |
| `SASUri` | 랜딩 영역에 대한 공유 액세스 서명 URI입니다. 이 문자열은 인증 중인 랜딩 영역에 대한 URI와 해당 SAS 토큰의 조합입니다. |

{style="table-layout:auto"}

### 업데이트 [!DNL Data Landing Zone] 자격 증명 {#update-dlz-credentials}

원할 경우 자격 증명을 새로 고칠 수도 있습니다. 다음을 업데이트할 수 있습니다. `SASToken` 에 POST 요청을 하여 `/credentials` 의 엔드포인트 [!DNL Connectors] API.

**API 형식**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| 쿼리 매개 변수 | 설명 |
| --- | --- |
| `dlz_destination` | 다음 `dlz_destination` 유형 을 사용하면 API에서 랜딩 영역 대상 컨테이너를 사용 가능한 다른 유형의 컨테이너와 구별할 수 있습니다. |
| `refresh` | 다음 `refresh` 작업을 통해 랜딩 영역 자격 증명을 재설정하고 새 항목을 자동으로 생성할 수 있습니다. `SASToken`. |

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

다음 응답은 다음에 대한 업데이트된 값을 반환합니다. `SASToken` 및 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

디스플레이 이름(`containerName`) 및 [!DNL Data Landing Zone] 위에서 설명한 API 호출에서 반환된 SAS URL을 선택한 다음 **다음**.

![Azure UI에서 강조 표시된 연결 정보를 입력하십시오.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

다음 **요약** 창에 설정에 대한 정보를 포함하여 설정의 개요를 제공합니다. [!DNL Blob] 엔드포인트 및 권한. 준비가 되면 다음을 선택합니다. **연결**.

![Azure UI에 표시된 설정 요약입니다.](/help/sources/images/tutorials/create/dlz/summary.png)

연결에 성공하면 다음 항목이 업데이트됩니다. [!DNL Azure Storage Explorer] 을 통한 UI [!DNL Data Landing Zone] 컨테이너.

![Azure UI에서 강조 표시된 DLZ 사용자 컨테이너의 요약입니다.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

(으)로 [!DNL Data Landing Zone] 컨테이너 연결됨 [!DNL Azure Storage Explorer]이제 Experience Platform에서 로 파일 내보내기를 시작할 수 있습니다. [!DNL Data Landing Zone] 컨테이너. 파일을 내보내려면 [!DNL Data Landing Zone] 아래 섹션에 설명된 대로 Experience Platform UI의 대상

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

다음을 연결했는지 확인하십시오. [!DNL Data Landing Zone] 컨테이너 대상 [!DNL Azure Storage Explorer] 에 설명된대로 [전제 조건](#prerequisites) 섹션. 이유 [!DNL Data Landing Zone] 는 Adobe이 프로비저닝된 스토리지로, Experience Platform UI에서 대상을 인증하기 위해 더 이상 단계를 수행할 필요가 없습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 을(를) 선택할 때 [!UICONTROL CSV] 옵션을 사용하여 다음을 수행할 수도 있습니다. [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 대해 Experience Platform이 사용해야 하는 압축 유형을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜거나 끕니다. 매니페스트의 이름은 형식을 사용하여 지정합니다. `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 보기 [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 내보낸 파일을 생성했습니다.
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장되는 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 예약

다음에서 **[!UICONTROL 예약]** 단계, 다음을 수행할 수 있습니다. [내보내기 일정 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 에 대한 [!DNL Data Landing Zone] 대상 및 다음을 수행할 수도 있습니다. [내보낸 파일의 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 속성 및 ID 매핑 {#map}

다음에서 **[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 속성 및 id 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 배치 대상 활성화 UI 튜토리얼에서 다음을 수행합니다.

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* 방법 [platform 사용자 인터페이스를 사용하여 데이터 세트 내보내기](/help/destinations/ui/export-datasets.md).
* 방법 [흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트 내보내기](/help/destinations/api/export-datasets.md).

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Data Landing Zone] 저장소가 추가되고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.
