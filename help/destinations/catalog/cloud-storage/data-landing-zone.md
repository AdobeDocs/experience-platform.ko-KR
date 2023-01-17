---
title: 데이터 랜딩 영역 대상
description: 데이터 랜딩 영역에 연결하여 세그먼트를 활성화하고 데이터 세트를 내보내는 방법을 알아봅니다.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 6fbf1b87becebee76f583c6e44b1c42956e561ab
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 1%

---

# (베타) 데이터 랜딩 영역 대상

>[!IMPORTANT]
>
>* 이 대상은 현재 베타에 있으며 제한된 수의 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 [!DNL Data Landing Zone] 연결되면 Adobe 담당자에게 연락하여 [!DNL Organization ID].
>* 이 설명서 페이지는 [!DNL Data Landing Zone] *대상*. 또한 [!DNL Data Landing Zone] *소스* 소스 카탈로그에 있습니다. 자세한 내용은 [[!DNL Data Landing Zone] 소스](/help/sources/connectors/cloud-storage/data-landing-zone.md) 설명서.



## 개요 {#overview}

[!DNL Data Landing Zone] is [!DNL Azure Blob] Adobe Experience Platform에서 프로비저닝한 스토리지 인터페이스로, Platform에서 파일을 내보낼 수 있는 안전한 클라우드 기반 파일 저장소 기능에 대한 액세스 권한을 부여합니다. 액세스 권한이 있습니다. [!DNL Data Landing Zone] 샌드박스당 컨테이너 및 모든 컨테이너의 총 데이터 볼륨은 Platform Products 및 Services 라이선스와 함께 제공된 총 데이터로 제한됩니다. Platform 및 Launch의 모든 애플리케이션 서비스(예: [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], 및 [!DNL Real-Time Customer Data Platform] 하나의 [!DNL Data Landing Zone] 샌드박스당 컨테이너. 을 통해 파일을 컨테이너에 읽고 쓸 수 있습니다 [!DNL Azure Storage Explorer] 또는 명령줄 인터페이스를 사용할 수 있습니다.

[!DNL Data Landing Zone] 는 SAS 기반 인증을 지원하고 데이터는 표준으로 보호됩니다 [!DNL Azure Blob] 저장 보안 메커니즘이 휴지 및 전송 중입니다. SAS 기반 인증을 통해 [!DNL Data Landing Zone] 공용 인터넷 연결을 통한 컨테이너 사용자의 [!DNL Data Landing Zone] 컨테이너. 즉, 네트워크에 대한 허용 목록 또는 지역 간 설정을 구성할 필요가 없습니다.

Platform에서는 [!DNL Data Landing Zone] 컨테이너. 7일 후 모든 파일이 삭제됩니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 세그먼트의 프로필 속성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드(예: PPID)와 함께 세그먼트의 모든 구성원을 내보냅니다 [대상 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 전제 조건 {#prerequisites}

을(를) 사용하기 전에 충족해야 하는 다음 전제 조건을 확인합니다. [!DNL Data Landing Zone] 대상.

### 연결 [!DNL Data Landing Zone] 컨테이너 [!DNL Azure Storage Explorer]

다음을 사용할 수 있습니다 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 의 컨텐츠를 관리하려면 [!DNL Data Landing Zone] 컨테이너. 사용을 시작하려면 [!DNL Data Landing Zone]를 채울 때는 먼저 자격 증명을 검색하고 입력해야 합니다. [!DNL Azure Storage Explorer], 및에 연결 [!DNL Data Landing Zone] 컨테이너 [!DNL Azure Storage Explorer].

에서 [!DNL Azure Storage Explorer] UI의 왼쪽 탐색 막대에서 연결 아이콘을 선택합니다. 다음 **리소스 선택** 연결할 옵션을 제공하는 창이 나타납니다. 선택 **[!DNL Blob container]** 에 연결 [!DNL Data Landing Zone] 저장.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

다음 을 선택합니다. **공유 액세스 서명 URL(SAS)** 을 연결 메서드로 사용하고 **다음**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

연결 방법을 선택한 후 **표시 이름** 그리고 **[!DNL Blob]컨테이너 SAS URL** 해당 [!DNL Data Landing Zone] 컨테이너.

>[!BEGINSHADEBOX]

### 에 대한 자격 증명을 검색합니다. [!DNL Data Landing Zone]

플랫폼 API를 사용하여 를 검색해야 합니다 [!DNL Data Landing Zone] 자격 증명. 자격 증명을 검색하기 위한 API 호출은 아래에 설명되어 있습니다. 헤더에 필요한 값을 가져오는 방법에 대한 자세한 내용은 [Adobe Experience Platform API 시작하기](/help/landing/api-guide.md) 안내서.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

**요청**

다음 요청 예는 기존 랜딩 영역에 대한 자격 증명을 검색합니다.

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

다음 응답에서는 현재 사용자를 포함하여 랜딩 영역에 대한 자격 증명 정보를 반환합니다 `SASToken` 및 `SASUri`뿐만 아니라 `storageAccountName` 랜딩 영역 컨테이너에 해당합니다.

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
| `SASToken` | 랜딩 영역에 대한 공유 액세스 서명 토큰. 이 문자열에는 요청을 승인하는 데 필요한 모든 정보가 들어 있습니다. |
| `SASUri` | 랜딩 영역에 대한 공유 액세스 서명 URI입니다. 이 문자열은 인증 대상 랜딩 영역에 대한 URI와 해당 SAS 토큰의 조합입니다. |

>[!ENDSHADEBOX]

표시 이름(`containerName`) 및 [!DNL Data Landing Zone] 위에 설명된 API 호출에서 반환되는 SAS URL을 선택한 다음 **다음**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

다음 **요약** 창이 나타나고 설정에 대한 정보를 포함하여 설정에 대한 개요를 제공합니다 [!DNL Blob] 엔드포인트 및 권한. 준비되면 을 선택합니다. **Connect**.

![요약](/help/sources/images/tutorials/create/dlz/summary.png)

연결에 성공하면 [!DNL Azure Storage Explorer] 사용 중인 UI [!DNL Data Landing Zone] 컨테이너.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

사용 [!DNL Data Landing Zone] 연결된 컨테이너 [!DNL Azure Storage Explorer]이제 Experience Platform에서 로 파일 내보내기를 시작할 수 있습니다. [!DNL Data Landing Zone] 컨테이너. 파일을 내보내려면 [!DNL Data Landing Zone] 아래 섹션에 설명된 대로 Experience Platform UI에 대상을 추가합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 입력합니다.

### 대상에 인증 {#authenticate}

에 연결되어 있는지 확인합니다. [!DNL Data Landing Zone] 컨테이너 [!DNL Azure Storage Explorer] 에 설명된 대로 [전제 조건](#prerequisites) 섹션을 참조하십시오. 왜냐면 [!DNL Data Landing Zone] 는 Adobe이 프로비저닝된 저장소이므로 대상을 인증하기 위해 Experience Platform UI에서 추가 단계를 수행할 필요가 없습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스트할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 을(를) 선택할 때 [!UICONTROL CSV] 선택 사항 [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 사용할 압축 유형을 Experience Platform에서 선택합니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 예약

에서 **[!UICONTROL 예약]** 단계를 수행하여 다음을 수행할 수 있습니다. [내보내기 스케줄 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 에 대해 [!DNL Data Landing Zone] 대상 및 [내보낸 파일의 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 특성 및 ID 매핑 {#map}

에서 **[!UICONTROL 매핑]** 단계: 프로파일에 대해 내보낼 속성 및 id 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 친숙한 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 배치 대상 활성화 UI 자습서에서 를 참조하십시오.

## (베타) 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 집합 내보내기를 지원합니다. 데이터 집합 내보내기를 설정하는 방법에 대한 자세한 내용은 [데이터 세트 내보내기 자습서](/help/destinations/ui/export-datasets.md).

## 성공적인 데이터 내보내기의 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Data Landing Zone] 저장하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.
