---
title: 클라우드 스토리지 대상으로 데이터 세트 내보내기
type: Tutorial
description: Adobe Experience Platform에서 선호하는 클라우드 스토리지 위치로 데이터 세트를 내보내는 방법을 알아봅니다.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: e95c0e509931f141ff72c1defacebe5a29756157
workflow-type: tm+mt
source-wordcount: '1845'
ht-degree: 4%

---

# 클라우드 스토리지 대상으로 데이터 세트 내보내기

>[!AVAILABILITY]
>
>* 이 기능은 Real-Time CDP Prime 또는 Ultimate 패키지, Adobe Journey Optimizer 또는 Customer Journey Analytics을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

이 문서에서는 Experience Platform UI를 사용하여 [데이터 세트](/help/catalog/datasets/overview.md)을(를) Adobe Experience Platform에서 선호하는 클라우드 저장소 위치(예: [!DNL Amazon S3], SFTP 위치 또는 [!DNL Google Cloud Storage])로 내보내는 데 필요한 워크플로에 대해 설명합니다.

Experience Platform API를 사용하여 데이터 세트를 내보낼 수도 있습니다. 자세한 내용은 [데이터 세트 내보내기 API 자습서](/help/destinations/api/export-datasets.md)를 참조하십시오.

## 내보내기에 사용 가능한 데이터 세트 {#datasets-to-export}

내보낼 수 있는 데이터 세트는 Experience Platform 애플리케이션(Real-Time CDP, Adobe Journey Optimizer), 계층(Prime 또는 Ultimate) 및 구입한 모든 추가 기능(예: Data Distiller)에 따라 다릅니다.

아래 표에서 애플리케이션, 제품 계층 및 구입한 추가 기능에 따라 내보낼 수 있는 데이터 세트 유형을 파악합니다.

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
    <td>소스, Web SDK, Mobile SDK, Analytics Data Connector 및 Audience Manager을 통해 데이터를 수집하거나 수집한 후 Experience Platform UI에서 생성된 프로필 및 경험 이벤트 데이터 세트입니다.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>소스, Web SDK, Mobile SDK, Analytics Data Connector 및 Audience Manager을 통해 데이터를 수집하거나 수집한 후 Experience Platform UI에서 생성된 프로필 및 경험 이벤트 데이터 세트입니다.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">시스템 생성 프로필 스냅숏 데이터 집합</a>.</li></td>
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
    <td> 소스, Web SDK, Mobile SDK, Analytics Data Connector 및 Audience Manager을 통해 데이터를 수집하거나 수집한 후 Experience Platform UI에서 생성된 프로필 및 경험 이벤트 데이터 세트입니다.</td>
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
>abstract="**증분 파일 내보내기**&#x200B;를 선택하여 마지막 내보내기 이후 데이터 세트에 추가된 데이터만 내보냅니다. <br>첫 번째 증분 파일 내보내기에는 채우기 역할을 하는 데이터 세트의 모든 데이터가 포함됩니다. 향후 증분 파일에는 첫 번째 내보내기 이후 데이터 세트에 추가된 데이터만 포함됩니다."

**[!UICONTROL 예약]** 단계에서는 데이터 세트 내보내기의 시작 날짜와 내보내기 케이던스를 설정할 수 있습니다.

**[!UICONTROL 증분 파일 내보내기]** 옵션이 자동으로 선택됩니다. 그러면 데이터 세트의 전체 스냅샷을 나타내는 하나 이상의 파일 내보내기가 트리거됩니다. 후속 파일은 이전 내보내기 이후 데이터 세트에 대한 증분 추가입니다.

>[!IMPORTANT]
>
>첫 번째 증분 파일 내보내기에는 데이터 집합에 있는 모든 기존 데이터가 포함되어 채우기 역할을 합니다. 내보내기에는 하나 이상의 파일이 포함될 수 있습니다.

![일정 단계를 표시하는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. **[!UICONTROL 빈도]** 선택기를 사용하여 내보내기 빈도를 선택하십시오.

   * **[!UICONTROL 매일]**: 매일 지정한 시간에 매일 한 번씩 증분 파일 내보내기를 예약합니다.
   * **[!UICONTROL 시간별]**: 증분 파일 내보내기를 3, 6, 8 또는 12시간마다 예약합니다.

2. 내보내기를 수행할 시간을 **[!UICONTROL 시간]** 선택기에서 [!DNL UTC] 형식으로 선택합니다.

3. **[!UICONTROL 날짜]** 선택기를 사용하여 내보내기를 수행할 간격을 선택하십시오. 내보내기에 대한 종료 날짜는 현재 설정할 수 없습니다. 자세한 내용은 [알려진 제한 사항](#known-limitations) 섹션을 참조하십시오.

4. **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 일정을 저장하고 **[!UICONTROL 검토]** 단계로 진행합니다.

>[!NOTE]
> 
>데이터 세트 내보내기의 경우 파일 이름에 수정할 수 없는 사전 설정된 기본 형식이 있습니다. 내보낸 파일에 대한 자세한 내용과 예를 보려면 [데이터 집합 내보내기 성공 확인](#verify) 섹션을 참조하십시오.

## 검토 {#review}

**[!UICONTROL 검토]** 페이지에서 선택한 항목에 대한 요약을 볼 수 있습니다. 흐름을 분할하려면 **[!UICONTROL 취소]**&#x200B;를 선택하고, 설정을 수정하려면 **[!UICONTROL 뒤로]**&#x200B;를 선택하고, 선택을 확인하고 데이터 세트를 대상으로 내보내려면 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.

![검토 단계를 표시하는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/review.png)

## 데이터 세트 내보내기 성공 확인 {#verify}

데이터 세트를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 하나 이상의 `.json` 또는 `.parquet` 파일을 만듭니다. 제공된 내보내기 일정에 따라 새 파일이 저장소 위치에 보관될 것으로 예상합니다.

Experience Platform은 지정한 저장소 위치에 내보낸 데이터 세트 파일을 저장하는 폴더 구조를 만듭니다. 내보내기 시간마다 아래 패턴을 따라 새 폴더가 만들어집니다.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

기본 파일 이름은 임의로 생성되며 내보낸 파일 이름이 고유한지 확인합니다.

### 샘플 데이터 세트 파일 {#sample-files}

스토리지 위치에 이러한 파일이 있으면 내보내기가 성공적으로 수행되었는지 확인할 수 있습니다. 내보낸 파일의 구조를 이해하기 위해 샘플 [.parquet 파일](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 또는 [.json 파일](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)을 다운로드할 수 있습니다.

#### 압축된 데이터 세트 파일 {#compressed-dataset-files}

[대상 워크플로우에 연결](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options)에서 아래와 같이 내보낼 데이터 세트 파일을 선택할 수 있습니다.

데이터 집합을 내보내기 위해 대상에 연결할 때 ![파일 형식 및 압축 선택.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

압축할 때 두 파일 유형 간의 파일 형식 차이를 확인합니다.

* 압축된 JSON 파일을 내보낼 때 내보낸 파일 형식은 `json.gz`입니다.
* 압축된 Parquet 파일을 내보낼 때 내보낸 파일 형식은 `gz.parquet`입니다.

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

다른 애플리케이션에 대한 데이터 내보내기 권한은 가산되지 않습니다. 예를 들어 Real-Time CDP Ultimate와 Adobe Journey Optimizer Ultimate를 구매하면 제품 설명에 따라 프로필 내보내기 권한이 두 권한 중 더 커집니다. 볼륨 권한은 라이선스가 부여된 총 프로필 수를 계산하고 Real-Time CDP Prime의 경우 500KB 또는 Real-Time CDP Ultimate의 경우 700KB를 곱하여 권한이 부여된 데이터의 양을 결정합니다.

반면 Data Distiller과 같은 추가 기능을 구입한 경우 권한이 부여된 데이터 내보내기 제한은 제품 계층과 추가 기능의 합계를 나타냅니다.

라이선스 대시보드에서 계약 제한에 대해 프로필 내보내기를 보고 추적할 수 있습니다.

## 알려진 제한 사항 {#known-limitations}

데이터 세트 내보내기의 일반 가용성 릴리스에 대한 다음 제한 사항을 염두에 두십시오.

* 현재는 증분 파일만 내보낼 수 있으며 데이터 세트 내보내기에 대한 종료 날짜를 선택할 수 없습니다.
* Experience Platform은 작은 데이터 세트의 경우에도 여러 파일을 내보낼 수 있습니다. 데이터 세트 내보내기는 시스템 간 통합을 위해 설계되었으며 성능에 최적화되었기 때문에 내보낸 파일 수를 사용자 지정할 수 없습니다.
* 내보낸 파일 이름은 현재 사용자 지정할 수 없습니다.
* API를 통해 생성된 데이터 세트는 현재 내보내기에 사용할 수 없습니다.
* 현재 UI가 대상으로 내보내는 데이터 세트를 삭제할 수 있도록 차단하지 않습니다. 대상으로 내보내는 데이터 세트는 삭제하지 마십시오. 데이터 집합을 삭제하기 전에 대상 데이터 흐름에서 [데이터 집합을 제거](#remove-dataset)합니다.
* 데이터 세트 내보내기에 대한 모니터링 지표는 현재 프로필 내보내기에 대한 숫자와 혼합되므로 실제 내보내기 숫자를 반영하지 않습니다.
* 타임스탬프가 365일보다 오래된 데이터는 데이터 세트 내보내기에서 제외됩니다. 자세한 내용은 예약된 데이터 세트 내보내기에 대한 [보호 기능](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)을 참조하십시오.
