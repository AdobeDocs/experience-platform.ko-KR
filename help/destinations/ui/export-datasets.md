---
title: 클라우드 스토리지 대상으로 데이터 세트 내보내기
type: Tutorial
description: Adobe Experience Platform에서 선호하는 클라우드 스토리지 위치로 데이터 세트를 내보내는 방법을 알아봅니다.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 5624dab337bcd27e28b4153459bb4e85fab22d6f
workflow-type: tm+mt
source-wordcount: '2594'
ht-degree: 8%

---

# 클라우드 스토리지 대상으로 데이터 세트 내보내기

>[!AVAILABILITY]
>
>* 이 기능은 Real-Time CDP Prime 또는 Ultimate 패키지, Adobe Journey Optimizer 또는 Customer Journey Analytics을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

이 문서에서는 Experience Platform UI를 사용하여 [데이터 세트](/help/catalog/datasets/overview.md)을(를) Adobe Experience Platform에서 선호하는 클라우드 저장소 위치(예: [!DNL Amazon S3], SFTP 위치 또는 [!DNL Google Cloud Storage])로 내보내는 데 필요한 워크플로에 대해 설명합니다.

Experience Platform API를 사용하여 데이터 세트를 내보낼 수도 있습니다. 자세한 내용은 [데이터 세트 내보내기 API 자습서](/help/destinations/api/export-datasets.md)를 참조하십시오.

## 내보내기에 사용 가능한 데이터 세트 {#datasets-to-export}

내보낼 수 있는 데이터 세트는 Experience Platform 애플리케이션(Real-Time CDP, Adobe Journey Optimizer), 계층(Prime 또는 Ultimate) 및 구입한 모든 추가 기능(예: Data Distiller)에 따라 다릅니다.

애플리케이션, 제품 계층 및 구입한 추가 기능에 따라 내보낼 수 있는 데이터 세트 유형을 아래 표를 사용하여 이해합니다.

<table>
<thead>
  <tr>
    <th>애플리케이션/추가 기능</th>
    <th>계층</th>
    <th>내보내기에 사용 가능한 데이터 세트</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>소스, Web SDK, Mobile SDK, Analytics Data Connector 및 Audience Manager을 통해 데이터를 수집하거나 수집한 후 Experience Platform UI에서 만들어진 프로필 및 경험 이벤트 데이터 세트입니다.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>소스, Web SDK, Mobile SDK, Analytics Data Connector 및 Audience Manager을 통해 데이터를 수집하거나 수집한 후 Experience Platform UI에서 만들어진 프로필 및 경험 이벤트 데이터 세트입니다.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">시스템 생성 프로필 스냅숏 데이터 집합</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td><a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> 설명서를 참조하세요.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> 설명서를 참조하세요.</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>모두</td>
    <td> 소스, Web SDK, Mobile SDK, Analytics Data Connector 및 Audience Manager을 통해 데이터를 수집하거나 수집한 후 Experience Platform UI에서 만들어진 프로필 및 경험 이벤트 데이터 세트입니다.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Data Distiller (추가 기능)</td>
    <td>쿼리 서비스를 통해 만들어진 파생 데이터 세트입니다.</td>
  </tr>
</tbody>
</table>

## 비디오 튜토리얼 {#video-tutorial}

이 페이지에 설명된 워크플로에 대한 전체적인 설명, 데이터 세트 내보내기 기능을 사용할 때의 이점 및 몇 가지 제안된 사용 사례를 확인하려면 아래 비디오를 보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## 지원되는 대상 {#supported-destinations}

현재, 스크린샷에 강조 표시되고 아래에 나열된 클라우드 스토리지 대상으로 데이터 세트를 내보낼 수 있습니다.

![데이터 집합 내보내기를 지원하는 대상을 보여 주는 대상 카탈로그 페이지입니다.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 대상자를 활성화하거나 데이터 세트를 내보내는 시기 {#when-to-activate-audiences-or-activate-datasets}

Experience Platform 카탈로그의 일부 파일 기반 대상은 대상 활성화와 데이터 세트 내보내기를 모두 지원합니다.

* 데이터가 대상자 관심사나 자격별로 그룹화된 프로필로 구성되도록 하려면 대상자 활성화를 고려하십시오.
* 또는 대상자 관심사나 자격에 의해 그룹화되거나 구조화되지 않은 원시 데이터 세트를 내보내려는 경우 데이터 세트 내보내기를 고려하십시오. 이 데이터는 보고, 데이터 과학 워크플로우 및 기타 다양한 사용 사례에 사용할 수 있습니다. 예를 들어 관리자, 데이터 엔지니어 또는 분석가는 Experience Platform에서 데이터를 내보내어 데이터 웨어하우스와 동기화하거나, BI 분석 도구, 외부 클라우드 ML 도구에서 사용하거나, 장기 저장 요구 사항에 맞게 시스템에 저장할 수 있습니다.

이 문서에는 데이터 세트를 내보내는 데 필요한 모든 정보가 포함되어 있습니다. 클라우드 저장소 또는 이메일 마케팅 대상에 *대상*&#x200B;을(를) 활성화하려면 [프로필 내보내기 대상을 일괄 처리하는 대상 데이터 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 읽어 보십시오.

## 전제 조건 {#prerequisites}

데이터 세트를 클라우드 저장소 대상으로 내보내려면 대상에 성공적으로 [연결](./connect-destination.md)해야 합니다. 아직 수행하지 않았다면 [대상 카탈로그](../catalog/overview.md)(으)로 이동하여 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

### 필요한 권한 {#permissions}

데이터 세트를 내보내려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 데이터 세트 보기]** 및 **[!UICONTROL 데이터 세트 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

데이터 세트를 내보내는 데 필요한 권한이 있고 대상이 데이터 세트 내보내기를 지원하는지 확인하려면 대상 카탈로그를 확인하십시오. 대상에 **[!UICONTROL 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]** 컨트롤이 있는 경우 적절한 권한이 있습니다.

## 대상 선택 {#select-destination}

지침에 따라 데이터 세트를 내보낼 수 있는 대상을 선택합니다.

1. **[!UICONTROL 연결 > 대상]**(으)로 이동하여 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   ![카탈로그 컨트롤이 강조 표시된 대상 카탈로그 탭.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 데이터 세트를 내보내려는 대상에 해당하는 카드에서 **[!UICONTROL 데이터 세트 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]**&#x200B;를 선택합니다.

   ![활성화 컨트롤이 강조 표시된 대상 카탈로그 탭입니다.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. **[!UICONTROL 데이터 형식 데이터 세트]**&#x200B;를 선택하고 데이터 세트를 내보낼 대상 연결을 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

>[!TIP]
> 
>데이터 집합을 내보내도록 새 대상을 설정하려면 **[!UICONTROL 새 대상 구성]**&#x200B;을 선택하여 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우를 트리거하십시오.

![데이터 세트 컨트롤이 강조 표시된 대상 활성화 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. **[!UICONTROL 데이터 세트 선택]** 보기가 나타납니다. 내보내기를 위해 [데이터 세트를 선택](#select-datasets)하려면 다음 섹션으로 이동하십시오.

## 데이터 세트 선택 {#select-datasets}

데이터 세트 이름 왼쪽에 있는 확인란을 사용하여 대상으로 내보낼 데이터 세트를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![내보낼 데이터 세트를 선택할 수 있는 데이터 세트 선택 단계를 표시하는 데이터 세트 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 데이터 세트 내보내기 예약 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="데이터 세트의 파일 내보내기 옵션"
>abstract="**증분 파일 내보내기**&#x200B;를 선택하여 마지막 내보내기 이후 데이터 세트에 추가된 데이터만 내보냅니다. <br>첫 번째 증분 파일 내보내기에는 채우기 역할을 하는 데이터 세트의 모든 데이터가 포함됩니다. 향후 증분 파일에는 첫 번째 내보내기 이후 데이터 세트에 추가된 데이터만 포함됩니다. <br> 각 내보내기 작업에서 각 데이터 세트의 전체 멤버십을 내보내려면 **전체 파일 내보내기**&#x200B;를 선택합니다. "

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="이 데이터 흐름의 종료 일자 업데이트"
>abstract="이 데이터 흐름의 종료 일자 업데이트"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="이 데이터 흐름 본문의 종료 일자 업데이트"
>abstract="최근 이 대상에 대한 업데이트로 인해 이제 데이터 흐름에 종료 일자가 필요합니다. Adobe는 기본 종료 일자를 2025년 5월 1일로 설정했습니다. 원하는 종료 일자로 업데이트하지 않으면 기본 일자에 데이터 내보내기가 중단됩니다."

**[!UICONTROL 예약]** 단계를 사용하여 다음을 수행합니다.

* 데이터 세트 내보내기에 대한 내보내기 케이던스뿐만 아니라 시작 날짜 및 종료 날짜를 설정합니다.
* 내보낸 데이터 세트 파일이 데이터 세트의 전체 멤버십을 내보내야 하는지 또는 각 내보내기 발생 시 멤버십에 대한 증분 변경만 내보내야 하는지 여부를 구성합니다.
* 데이터 세트를 내보내야 하는 저장소 위치의 폴더 경로를 사용자 지정합니다. [내보내기 폴더 경로를 편집](#edit-folder-path)하는 방법에 대해 자세히 알아보세요.

페이지의 **[!UICONTROL 일정 편집]** 컨트롤을 사용하여 내보내기 케이던스를 편집하고 전체 파일을 내보내는지 증분 파일을 내보내는지 여부를 선택합니다.

![예약 단계에서 강조 표시된 예약 컨트롤을 편집합니다.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlight.png)

기본적으로 **[!UICONTROL 증분 파일 내보내기]** 옵션이 선택되어 있습니다. 그러면 데이터 세트의 전체 스냅샷을 나타내는 하나 이상의 파일 내보내기가 트리거됩니다. 후속 파일은 이전 내보내기 이후 데이터 세트에 대한 증분 추가입니다. **[!UICONTROL 전체 파일 내보내기]**&#x200B;를 선택할 수도 있습니다. 이 경우 데이터 집합의 일회성 전체 내보내기에 대한 빈도를 **[!UICONTROL Once]**&#x200B;로 선택합니다.

>[!IMPORTANT]
>
>첫 번째 증분 파일 내보내기에는 데이터 집합에 있는 모든 기존 데이터가 포함되어 채우기 역할을 합니다. 내보내기에는 하나 이상의 파일이 포함될 수 있습니다.

![일정 단계를 표시하는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. **[!UICONTROL 빈도]** 선택기를 사용하여 내보내기 빈도를 선택하십시오.

   * **[!UICONTROL 매일]**: 매일 지정한 시간에 매일 한 번씩 증분 파일 내보내기를 예약합니다.
   * **[!UICONTROL 시간별]**: 증분 파일 내보내기를 3, 6, 8 또는 12시간마다 예약합니다.

2. 내보내기를 수행할 시간을 **[!UICONTROL 시간]** 선택기에서 [!DNL UTC] 형식으로 선택합니다.

3. **[!UICONTROL 날짜]** 선택기를 사용하여 내보내기를 수행할 간격을 선택하십시오.

4. **[!UICONTROL 저장]**&#x200B;을 선택하여 일정을 저장하고 **[!UICONTROL 검토]** 단계로 진행합니다.

>[!NOTE]
> 
>데이터 세트 내보내기의 경우 파일 이름에 수정할 수 없는 사전 설정된 기본 형식이 있습니다. 내보낸 파일에 대한 자세한 내용과 예를 보려면 [데이터 집합 내보내기 성공 확인](#verify) 섹션을 참조하십시오.

## 폴더 경로 편집 {#edit-folder-path}

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="폴더 경로 편집"
>abstract="제공된 여러 매크로를 사용하여 데이터 세트를 내보내는 폴더 경로를 사용자 정의합니다."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="데이터 세트 폴더 경로 미리보기"
>abstract="이 창에 추가한 매크로를 기반으로 스토리지 위치에서 생성된 폴더 구조를 미리보기합니다."

내보낸 데이터 세트가 저장되는 저장소 위치의 폴더 구조를 사용자 지정하려면 **[!UICONTROL 폴더 경로 편집]**&#x200B;을 선택합니다.

![예약 단계에서 강조 표시된 폴더 경로 컨트롤을 편집합니다.](/help/destinations/assets/ui/export-datasets/edit-folder-path.png)

사용 가능한 여러 매크로를 사용하여 원하는 폴더 이름을 사용자 정의할 수 있습니다. 매크로를 두 번 클릭하여 폴더 경로에 추가하고 매크로 사이에 `/`을(를) 사용하여 폴더를 구분합니다.

![사용자 지정 폴더 모달 창에서 강조 표시된 매크로 선택.](/help/destinations/assets/ui/export-datasets/custom-folder-path-macros.png)

원하는 매크로를 선택하면 저장소 위치에 생성되는 폴더 구조의 미리보기가 표시됩니다. 폴더 구조의 첫 번째 수준은 데이터 집합을 내보내기 위해 [대상에 연결](/help/destinations/ui/connect-destination.md##set-up-connection-parameters)할 때 표시한 **[!UICONTROL 폴더 경로]**&#x200B;을(를) 나타냅니다.

![사용자 지정 폴더 모달 창에서 강조 표시된 폴더 경로를 미리 봅니다.](/help/destinations/assets/ui/export-datasets/custom-folder-path-preview.png)

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택한 항목에 대한 요약을 볼 수 있습니다. 흐름을 분할하려면 **[!UICONTROL 취소]**&#x200B;를 선택하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택을 확인하고 데이터 세트를 대상으로 내보내려면 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.

![검토 단계를 표시하는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/review.png)

## 데이터 세트 내보내기 성공 확인 {#verify}

데이터 세트를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 하나 이상의 `.json` 또는 `.parquet` 파일을 만듭니다. 제공된 내보내기 일정에 따라 새 파일이 저장소 위치에 보관될 것으로 예상합니다.

Experience Platform은 지정한 저장소 위치에 내보낸 데이터 세트 파일을 저장하는 폴더 구조를 만듭니다. 기본 폴더 내보내기 패턴은 아래에 표시되어 있지만 [기본 매크로로 폴더 구조를 사용자 지정](#edit-folder-path)할 수 있습니다.

>[!TIP]
> 
>이 폴더 구조의 첫 번째 수준인 `folder-name-you-provided`은(는) 데이터 집합을 내보내기 위해 [대상에 연결](/help/destinations/ui/connect-destination.md##set-up-connection-parameters)할 때 표시한 **[!UICONTROL 폴더 경로]**&#x200B;을(를) 나타냅니다.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

기본 파일 이름은 임의로 생성되며 내보낸 파일 이름이 고유한지 확인합니다.

### 샘플 데이터 세트 파일 {#sample-files}

스토리지 위치에 이러한 파일이 있으면 내보내기가 성공적으로 수행되었는지 확인할 수 있습니다. 내보낸 파일의 구조를 이해하기 위해 샘플 [.parquet 파일](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 또는 [.json 파일](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)을 다운로드할 수 있습니다.

#### 압축된 데이터 세트 파일 {#compressed-dataset-files}

[대상 워크플로우에 연결](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options)에서 아래와 같이 내보낼 데이터 세트 파일을 선택할 수 있습니다.

데이터 집합을 내보내기 위해 대상에 연결할 때 ![파일 형식 및 압축 선택.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

압축할 때 두 파일 유형 간의 파일 형식 차이를 확인합니다.

* 압축된 JSON 파일을 내보낼 때 내보낸 파일 형식은 `json.gz`입니다. 내보낸 JSON의 형식은 NDJSON이며, 이 형식은 빅 데이터 생태계의 표준 교환 형식입니다. Adobe은 NDJSON 호환 클라이언트를 사용하여 내보낸 파일을 읽는 것을 권장합니다.
* 압축된 Parquet 파일을 내보낼 때 내보낸 파일 형식은 `gz.parquet`입니다.

JSON 파일로 내보내기는 압축 모드에서 *지원됩니다*. Parquet 파일로 내보내기는 압축 및 압축되지 않은 모드에서 지원됩니다.

## 대상에서 데이터 세트 제거 {#remove-dataset}

기존 데이터 흐름에서 데이터 세트를 제거하려면 아래 단계를 따르십시오.

1. [Experience Platform UI](https://experience.adobe.com/platform/)에 로그인하고 왼쪽 탐색 모음에서 **[!UICONTROL 대상]**&#x200B;을 선택합니다. 기존 대상 데이터 흐름을 보려면 상단 헤더에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.

   ![대상 연결이 표시되고 나머지 내용이 흐리게 표시되는 대상 찾아보기 보기입니다.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >왼쪽 상단의 필터 아이콘 ![Filter-icon](/help/images/icons/filter.png)을(를) 선택하여 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상의 목록을 제공합니다. 목록에서 두 개 이상의 대상을 선택하여 선택한 대상과 연관된 데이터 흐름의 필터링된 선택을 확인할 수 있습니다.

2. **[!UICONTROL 활성화 데이터]** 열에서 데이터 세트 컨트롤을 선택하여 이 내보내기 데이터 흐름에 매핑된 모든 데이터 세트를 봅니다.

   ![활성화 데이터 열에서 사용 가능한 데이터 세트 탐색 옵션이 강조 표시되어 있습니다.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. 대상의 **[!UICONTROL 활성화 데이터]** 페이지가 나타납니다. 데이터 세트 목록 왼쪽의 확인란을 사용하여 제거할 데이터 세트를 선택한 다음 오른쪽 레일에서 **[!UICONTROL 데이터 세트 제거]**&#x200B;를 선택하여 데이터 세트 제거 확인 대화 상자를 트리거합니다.

   ![오른쪽 레일에서 데이터 집합 제거 컨트롤을 표시하는 데이터 집합 제거 대화 상자.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. 확인 대화 상자에서 **[!UICONTROL 제거]**&#x200B;를 선택하여 대상으로 내보내기에서 데이터 세트를 즉시 제거합니다.

   ![데이터 흐름에서 데이터 집합 제거 확인 옵션을 보여 주는 대화 상자.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 데이터 세트 내보내기 권한 {#licensing-entitlement}

각 Experience Platform 애플리케이션에 대해 연간 얼마나 많은 데이터를 내보낼 수 있는지 파악하려면 제품 설명 문서를 참조하십시오. 예를 들어 Real-Time CDP 제품 설명 [여기](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)를 볼 수 있습니다.

다른 애플리케이션에 대한 데이터 내보내기 권한은 가산되지 않습니다. 예를 들어 Real-Time CDP Ultimate 및 Adobe Journey Optimizer Ultimate을 구매하는 경우 제품 설명에 따라 프로필 내보내기 권한이 두 권한 중 더 커지게 됩니다. 볼륨 권한은 라이선스가 부여된 총 프로필 수를 계산하고 Real-Time CDP Prime의 경우 500KB 또는 Real-Time CDP Ultimate의 경우 700KB를 곱하여 권한이 부여된 데이터의 양을 결정합니다.

반면 Data Distiller과 같은 추가 기능을 구입한 경우 권한이 부여된 데이터 내보내기 제한은 제품 계층과 추가 기능의 합계를 나타냅니다.

[라이선스 사용 대시보드](/help/landing/license-usage-and-guardrails/license-usage-dashboard.md)에서 계약 제한에 대한 프로필 내보내기를 보고 추적할 수 있습니다.

## 알려진 제한 사항 {#known-limitations}

데이터 세트 내보내기의 일반 가용성 릴리스에 대한 다음 제한 사항을 염두에 두십시오.

* Experience Platform은 작은 데이터 세트의 경우에도 여러 파일을 내보낼 수 있습니다. 데이터 세트 내보내기는 시스템 간 통합을 위해 설계되었으며 성능에 최적화되었기 때문에 내보낸 파일 수를 사용자 지정할 수 없습니다.
* 내보낸 파일 이름은 현재 사용자 지정할 수 없습니다.
* API를 통해 생성된 데이터 세트는 현재 내보내기에 사용할 수 없습니다.
* 현재 UI가 대상으로 내보내는 데이터 세트를 삭제할 수 있도록 차단하지 않습니다. 대상으로 내보내는 데이터 세트는 삭제하지 마십시오. 데이터 집합을 삭제하기 전에 대상 데이터 흐름에서 [데이터 집합을 제거](#remove-dataset)합니다.
* 데이터 세트 내보내기에 대한 모니터링 지표는 현재 프로필 내보내기에 대한 숫자와 혼합되므로 실제 내보내기 숫자를 반영하지 않습니다.
* 타임스탬프가 365일보다 오래된 데이터는 데이터 세트 내보내기에서 제외됩니다. 자세한 내용은 예약된 데이터 세트 내보내기에 대한 [보호 기능](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)을 참조하십시오.

## 자주 묻는 질문 {#faq}

**폴더 경로로 `/`에 저장하면 폴더가 없는 파일을 생성할 수 있습니까? 또한 폴더 경로가 필요하지 않으면 폴더 또는 위치에 중복된 이름을 가진 파일이 어떻게 생성됩니까?**

+++답변
2024년 9월 릴리스부터 폴더 이름을 사용자 지정하고 `/`을(를) 사용하여 동일한 폴더의 모든 데이터 세트에 대한 파일을 내보낼 수 있습니다. Adobe 다른 데이터 세트에 속하는 시스템 생성 파일 이름이 동일한 폴더에 혼합되므로 여러 데이터 세트를 내보내는 대상에 대해서는 이 옵션을 사용하지 않는 것이 좋습니다.
+++

**매니페스트 파일을 한 폴더로 라우팅하고 데이터 파일을 다른 폴더로 라우팅할 수 있습니까?**

+++답변
아니요. 매니페스트 파일을 다른 위치에 복사할 수 없습니다.
+++

**파일 배달 순서 또는 타이밍을 제어할 수 있습니까?**

+++답변
내보내기 예약 옵션이 있습니다. 파일 복사를 지연하거나 순서를 지정하는 옵션은 없습니다. 이러한 파일은 생성되는 즉시 저장소 위치에 복사됩니다.
+++

**매니페스트 파일에 사용할 수 있는 형식은 무엇입니까?**

+++답변
매니페스트 파일은 .json 형식입니다.
+++

**매니페스트 파일에 API를 사용할 수 있습니까?**

+++답변
매니페스트 파일에 사용할 수 있는 API는 없지만 내보내기를 구성하는 파일 목록을 포함합니다.
+++

**매니페스트 파일에 추가 세부 정보(예: 레코드 수)를 추가할 수 있습니까? 그렇다면 어떻게?**

+++답변
매니페스트 파일에 정보를 추가할 수 없습니다. 레코드 수는 `flowRun` 엔터티(API를 통해 쿼리할 수 있음)를 통해 사용할 수 있습니다. 대상 모니터링에서 자세히 알아보십시오.
+++

**데이터 파일이 어떻게 분할됩니까? 파일당 레코드 수**

+++답변
데이터 파일은 Experience Platform 데이터 레이크의 기본 파티셔닝에 따라 분할됩니다. 데이터 세트가 클수록 파티션 수가 많습니다. 기본 분할은 읽기에 최적화되었기 때문에 사용자가 구성할 수 없습니다.
+++

**임계값(파일당 레코드 수)을 설정할 수 있습니까?**

+++답변
아니요, 불가능합니다.
+++

**초기 전송이 잘못된 경우 데이터 집합을 어떻게 다시 전송합니까?**

+++답변
대부분의 시스템 오류 유형에 대해 자동으로 다시 시도가 수행됩니다.
+++