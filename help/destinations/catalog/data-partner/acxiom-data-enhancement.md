---
title: Acxiom 데이터 개선 사항
description: 이 커넥터를 사용하여 데이터 강화를 위해 Real-Time CDP에서 Acxiom으로 자사 Adobe 프로필을 활성화하고 마케팅 채널 전반에서 사용할 수 있습니다. 그런 다음 Acxiom 소스를 사용하여 고급 데이터가 포함된 프로필을 가져오고 Real-Time CDP에서 작업할 수 있습니다.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 2%

---

# [!DNL Acxiom Data Enhancement] 대상 연결

>[!NOTE]
>
>다음 [!DNL Acxiom Data Enhancement] 대상이 Beta 버전입니다.  이 대상 커넥터 및 설명서 페이지는 Acxiom 팀이 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 acxiom-adobe-help@acxiom.com으로 직접 문의하시기 바랍니다.

## 개요 {#overview}

사용 [!DNL Acxiom Data Enhancement] analytics, 세그멘테이션 및 타깃팅 애플리케이션에서 사용하기 위해 고객 프로필에 추가 설명 데이터를 제공하는 커넥터입니다. 수백 개의 요소를 사용할 수 있으므로 데이터를 더 잘 세그먼트화하고 모델링할 수 있으므로 더 정확한 타겟팅 및 예측 모델링을 수행할 수 있습니다.

![자사 데이터를 Acxiom으로 내보낸 다음 보강된 데이터를 다시 Real-Time CDP으로 가져오는 마케팅 다이어그램](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

이 튜토리얼에서는 [!DNL Acxiom Data Enhancement] Adobe Experience Platform 사용자 인터페이스를 사용한 대상 연결 및 데이터 흐름. 이 커넥터는 Amazon S3를 드롭 포인트로 사용하여 Acxiom 개선 서비스에 데이터를 전달하는 데 사용됩니다.

![Acxiom 대상이 선택된 대상 카탈로그입니다.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Acxiom Data Enhancement] 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 고객 데이터 향상 {#enhance-customer-data}

이 커넥터는 선택된 설명 요소를 고객 프로필에 추가하여 도달 전략의 효과를 높이고 이를 사용하여 캠페인을 더 잘 공략하기 위한 목적으로 마케팅 전문가가 사용해야 합니다.

예를 들어 마케터는 추가 데이터로 프로필을 보강하여 기존 대상자에 대한 이해를 심화하고자 할 수 있습니다. 이렇게 하면 세그먼테이션 및 타기팅 전략이 개선되어 캠페인 개인화 및 전환이 향상됩니다.

사용 사례는 대상 및 소스 커넥터 조합을 통해 실행됩니다.

먼저 이 대상 커넥터를 사용하여 데이터 보강 목적으로 기존 고객 레코드를 내보냅니다. Acxiom의 서비스는 파일을 검색하고 검색하며 Acxiom의 데이터로 보강하고 파일을 생성합니다.

그런 다음 고객은 해당 [Acxiom 데이터 섭취](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) 소스 카드를 사용하여 하이드레이션된 고객 프로필을 다시 Adobe Real-Time CDP으로 수집합니다.

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>* 대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | x | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}


## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 데이터 세트 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

Experience Platform 시 버킷에 액세스하려면 다음 자격 증명에 대한 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3 액세스 키 | 버킷에 대한 액세스 키 ID입니다. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |
| S3 비밀 키 | 버킷의 비밀 키 ID. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |
| 버킷 이름 | 파일을 공유할 버킷입니다. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |

### 새 계정

새 Acxiom Managed S3 위치를 정의하려면

![새 계정](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### 기존 계정

다음을 사용하여 이미 정의된 계정 [!DNL Acxiom Data Enhancement] 대상이 목록 팝업에 나타납니다. 선택하면 오른쪽 레일에서 계정에 대한 세부 정보를 볼 수 있습니다. 로 이동하면 UI에서 예를 봅니다. **[!UICONTROL 대상]** > **[!UICONTROL 계정]**;

![기존 계정](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 세부 사항](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **이름(필수)** - 대상이 저장될 이름
* **설명** - 대상 목적에 대한 간략한 설명
* **버킷 이름(필수)** - S3에 설정된 Amazon S3 버킷의 이름
* **폴더 경로(필수)** - 버킷의 하위 디렉터리를 사용하는 경우 경로를 정의하거나 &#39;/&#39;를 사용하여 루트 경로를 참조해야 합니다.
* **파일 유형** - 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 현재 Acxiom 처리에 필요한 유일한 파일 유형은 CSV입니다

>[!IMPORTANT]
>
>CSV 옵션을 선택할 때, *구분 기호*, *인용 문자*, *문자 이스케이프 처리*, *빈 값*, *Null 값*, *압축 포맷*, 및 *매니페스트 파일 포함* 옵션이 표시됩니다. 다음 문서에서는 이러한 설정에 대해 자세히 설명합니다 [서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).

![CSV 옵션](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](/help/destinations/ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 매핑 제안

Acxiom 측에서 파일을 올바르게 처리하려면 이름 및 주소 요소가 필요합니다. 모든 요소가 필요한 것은 아니지만 가능한 한 많이 제공하면 성공적인 일치를 수행하는 데 도움이 됩니다.

매핑 제안은 고객이 프로필 속성을 매핑할 수 있는 Acxiom 처리에 사용되는 대상 측의 속성을 나열하는 아래 표에 제공됩니다. 모든 요소가 필요한 것은 아니며 소스 값은 계정의 요구 사항에 따라 달라지므로 이러한 요소를 제안으로 처리합니다.

| 대상 필드 | Source 설명 |
|--------------|-------------------------------------------------------------|
| 이름 | 다음 `person.name.fullName` Experience Platform의 값입니다. |
| 이름 | 다음 `person.name.firstName` Experience Platform의 값입니다. |
| 성 | 다음 `person.name.lastName` Experience Platform의 값입니다. |
| address1 | 다음 `mailingAddress.street1` Experience Platform의 값입니다. |
| address2 | 다음 `mailingAddress.street2` Experience Platform의 값입니다. |
| 도시 | 다음 `mailingAddress.city` Experience Platform의 값입니다. |
| state | 다음 `mailingAddress.state` Experience Platform의 값입니다. |
| zip | 다음 `mailingAddress.postalCode` Experience Platform의 값입니다. |

>[!NOTE]
>
>데이터 흐름에서 위에 나열되지 않은 추가 필드를 매핑하면 데이터 내보내기에 포함되지만 Acxiom 처리에서는 무시됩니다.

## 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Amazon S3 Storage] 버킷 을 만들고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.

## 다음 단계

이 자습서를 따라 Experience Platform에서 로 프로필 데이터를 내보내는 데이터 흐름을 만들었습니다. [!DNL Acxiom] 관리되는 S3 위치입니다. 다음으로, 처리를 설정할 수 있도록 계정 이름, 파일 이름 및 버킷 경로를 사용하여 Acxiom 담당자에게 문의해야 합니다.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
