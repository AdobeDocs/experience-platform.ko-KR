---
title: (베타) 클라우드 스토리지 대상으로 데이터 세트 내보내기
type: Tutorial
description: Adobe Experience Platform에서 기본 설정 클라우드 스토리지 위치로 데이터 세트를 내보내는 방법을 알아봅니다.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: aebb1494a6ed667730997048d30a2ca3e00f9452
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---

# (베타) 클라우드 스토리지 대상으로 데이터 세트 내보내기

>[!IMPORTANT]
>
>* 데이터 세트를 내보내는 기능은 현재 베타에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.
>* 이 베타 기능은 Real-time Customer Data Platform에 정의된 대로 1세대 데이터의 내보내기를 지원합니다 [제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* 이 기능은 Real-Time CDP Prime 및 Ultimate 패키지를 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.


이 문서에서는 내보내는 데 필요한 워크플로우에 대해 설명합니다 [데이터 세트](/help/catalog/datasets/overview.md) Adobe Experience Platform에서 선호하는 클라우드 스토리지 위치(예: ) [!DNL Amazon S3], SFTP 위치 또는 [!DNL Google Cloud Storage] Experience Platform UI 사용.

Experience Platform API를 사용하여 데이터 세트를 내보낼 수도 있습니다. 다음 문서를 참조하십시오. [데이터 세트 API 내보내기 자습서](/help/destinations/api/export-datasets.md) 추가 정보.

## 세그먼트를 활성화하거나 데이터 세트를 내보내는 경우 {#when-to-activate-segments-or-activate-datasets}

Experience Platform 카탈로그의 일부 파일 기반 대상은 세그먼트 활성화와 데이터 세트 내보내기를 모두 지원합니다.

* 데이터를 대상 관심사나 자격별로 그룹화된 프로필로 구조화하려는 경우 세그먼트를 활성화하는 것이 좋습니다.
* 또는 대상 관심사나 자격에 따라 그룹화되거나 구조화되지 않은 원시 데이터 세트를 내보내려고 할 때 데이터 세트 내보내기를 고려해 보십시오. 이 데이터를 보고, 데이터 과학 워크플로우, 규정 준수 요구 사항 및 기타 많은 사용 사례를 충족하는 데 사용할 수 있습니다.

이 문서에는 데이터 세트를 내보내는 데 필요한 모든 정보가 포함되어 있습니다. 세그먼트를 클라우드 스토리지 또는 이메일 마케팅 대상에 활성화하려면 다음을 참조하십시오. [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](/help/destinations/ui/activate-batch-profile-destinations.md).

## 사전 요구 사항 {#prerequisites}

클라우드 스토리지 대상으로 데이터 세트를 내보내려면 성공적으로 [대상에 연결](./connect-destination.md). 아직 하지 않았다면 을(를) 참조하십시오. [대상 카탈로그](../catalog/overview.md)를 클릭하고 지원되는 대상을 탐색하고 사용할 대상을 구성합니다.

### 필요 권한 {#permissions}

데이터 세트를 내보내려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, 및 **[!UICONTROL 데이터 집합 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

데이터 세트를 내보내는 데 필요한 권한이 있고 대상이 데이터 세트 내보내기를 지원하는지 확인하려면 대상 카탈로그를 찾아보십시오. 대상에 **[!UICONTROL 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]** 그런 다음 적절한 권한이 있습니다.

## 대상을 선택합니다 {#select-destination}

지침에 따라 데이터 세트를 내보낼 수 있는 대상을 선택합니다.

1. 이동 **[!UICONTROL 연결 > 대상]**, 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 카탈로그]** 탭.

   ![카탈로그 컨트롤이 강조 표시된 대상 카탈로그 탭입니다.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 선택 **[!UICONTROL 활성화]** 또는 **[!UICONTROL 데이터 세트 내보내기]** 로 데이터 세트를 내보낼 대상에 해당하는 카드에서

   ![활성화 컨트롤이 강조 표시된 대상 카탈로그 탭입니다.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 선택 **[!UICONTROL 데이터 유형 데이터 세트]** 데이터 세트를 내보낼 대상 연결을 선택한 다음, **[!UICONTROL 다음]**.

>[!TIP]
> 
>데이터 세트를 내보내는 새 대상을 설정하려면 를 선택합니다 **[!UICONTROL 새 대상 구성]** 트리거하다 [대상에 연결](/help/destinations/ui/connect-destination.md) 워크플로우.

![데이터 세트 컨트롤이 강조 표시된 대상 활성화 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 다음 **[!UICONTROL 데이터 세트 선택]** 보기가 나타납니다. 다음 섹션으로 이동하여 다음을 수행합니다 [데이터 세트 선택](#select-datasets) 내보내기.

## 데이터 세트 선택 {#select-datasets}

데이터 세트 이름 왼쪽에 있는 확인란을 사용하여 대상으로 내보낼 데이터 세트를 선택한 다음 선택합니다 **[!UICONTROL 다음]**.

![내보낼 데이터 세트를 선택할 수 있는 데이터 세트 선택 단계를 보여주는 데이터 세트 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 데이터 집합 내보내기 예약 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="데이터 세트에 대한 파일 내보내기 옵션"
>abstract="선택 **증분 파일 내보내기** 마지막 내보내기 이후 데이터 세트에 추가된 데이터만 내보냅니다. <br> 첫 번째 증분 파일 내보내기에는 데이터 집합에 있는 모든 데이터가 포함되며 채우기 역할을 합니다. 향후 증분 파일에는 첫 번째 내보내기 이후 데이터 세트에 추가된 데이터만 포함됩니다."

에서 **[!UICONTROL 예약]** 1단계에서 시작 날짜와 데이터 세트 내보내기에 대한 내보내기 간격을 설정할 수 있습니다.

다음 **[!UICONTROL 증분 파일 내보내기]** 옵션이 자동으로 선택됩니다. 첫 번째 파일이 데이터 세트의 전체 스냅샷이고 그 다음 파일은 이전 내보내기 이후 데이터 세트에 대한 증분 추가인 내보내기를 트리거합니다.

>[!IMPORTANT]
>
>처음 내보낸 증분 파일에는 데이터 집합에 있는 기존 데이터가 모두 포함되어 채우기 기능으로 작동합니다.

![예약 단계를 보여주는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 를 사용하십시오 **[!UICONTROL 빈도]** 선택기를 사용하여 내보내기 빈도를 선택합니다.

   * **[!UICONTROL 일별]**: 증분 파일 내보내기를 지정하는 시간에 매일 예약합니다.
   * **[!UICONTROL 시간별]**: 3, 6, 8 또는 12시간마다 증분 파일 내보내기 예약

2. 를 사용하십시오 **[!UICONTROL 시간]** 선택기를 사용하여 시간 선택, 위치 [!DNL UTC] 형식을 지정할 수도 있습니다.

3. 를 사용하십시오 **[!UICONTROL 날짜]** 선택기를 사용하여 내보낼 간격을 선택합니다. 기능의 베타 버전에서는 내보내기에 대한 종료 날짜를 설정할 수 없습니다. 자세한 내용은 [알려진 제한 사항](#known-limitations) 섹션을 참조하십시오.

4. 선택 **[!UICONTROL 다음]** 일정을 저장하고 **[!UICONTROL 검토]** 단계.

>[!NOTE]
> 
>데이터 집합 내보내기의 경우 파일 이름에 사전 설정된 기본 형식이 있으며, 이 형식은 수정할 수 없습니다. 섹션을 참조하십시오 [성공적인 데이터 세트 내보내기 확인](#verify) 를 참조하십시오.

## 검토 {#review}

설정 **[!UICONTROL 검토]** 페이지에서 선택 사항에 대한 요약을 볼 수 있습니다. 선택 **[!UICONTROL 취소]** 흐름을 분해하려면 **[!UICONTROL 뒤로]** 설정을 수정하려면 **[!UICONTROL 완료]** 선택 내용을 확인하고 데이터 세트를 대상으로 내보내기를 시작합니다.

![검토 단계를 보여주는 데이터 집합 내보내기 워크플로우입니다.](/help/destinations/assets/ui/export-datasets/review.png)

## 성공적인 데이터 세트 내보내기 확인 {#verify}

데이터 세트를 내보낼 때 Experience Platform은 `.json` 또는 `.parquet` 파일을 입력한 저장 위치에 저장합니다. 제공한 내보내기 일정에 따라 스토리지 위치에 새 파일이 저장될 것으로 예상됩니다.

Experience Platform은 지정한 저장소 위치에 폴더 구조를 만들어 내보낸 데이터 세트 파일을 보관합니다. 다음 패턴을 따라 내보내기 시간 마다 새 폴더가 만들어집니다.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

기본 파일 이름은 임의로 생성되며 내보낸 파일 이름이 고유한지 확인합니다.

### 샘플 데이터 세트 파일 {#sample-files}

저장소 위치에 이러한 파일이 있으면 성공적으로 내보내기를 확인합니다. 내보낸 파일의 구조를 이해하기 위해 샘플을 다운로드할 수 있습니다 [.parquet 파일](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 또는 [.json 파일](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## 대상에서 데이터 세트 제거 {#remove-dataset}

기존 데이터 흐름에서 데이터 세트를 제거하려면 아래 단계를 수행하십시오.

1. 에 로그인합니다. [Experience Platform UI](https://platform.adobe.com/) 을(를) 선택합니다. **[!UICONTROL 대상]** 왼쪽 탐색 막대에서 을 클릭합니다. 선택 **[!UICONTROL 찾아보기]** 기존 대상 데이터 흐름을 보려면 상단 헤더에서 클릭하십시오.

   ![대상 연결이 표시된 대상 찾아보기 보기가 표시되고 나머지 항목은 흐리게 표시됩니다.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >필터 아이콘을 선택합니다 ![Filter-icon](../assets/ui/edit-activation/filter.png) 왼쪽 상단에서 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상 목록을 제공합니다. 목록에서 둘 이상의 대상을 선택하여 선택한 대상과 연관된 필터링된 데이터 흐름 선택을 볼 수 있습니다.

1. 에서 **[!UICONTROL 활성화 데이터]** 열에서 데이터 세트 컨트롤을 선택하여 이 내보내기 데이터 세트에 매핑된 모든 데이터 세트를 봅니다.

   ![활성화 데이터 열에 강조 표시된 사용 가능한 데이터 세트 탐색 옵션입니다.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 다음 **[!UICONTROL 활성화 데이터]** 대상에 대한 페이지가 나타납니다. 선택 **[!UICONTROL 데이터 세트 제거]** 오른쪽 레일에서 데이터 세트 제거 확인 대화 상자를 트리거합니다.

   ![오른쪽 레일에 데이터 집합 제거 컨트롤을 보여주는 데이터 집합 제거 대화 상자가 표시됩니다.](../assets/ui/export-datasets/remove-dataset-control.png)

1. 확인 대화 상자에서 를 선택합니다. **[!UICONTROL 제거]** 내보내기에서 대상으로 데이터 세트를 즉시 제거하려면 다음을 수행하십시오.

   ![데이터 플로우에서 데이터 집합 제거 확인 옵션을 표시하는 대화 상자](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 알려진 제한 사항 {#known-limitations}

데이터 집합 내보내기의 베타 릴리스에 대해서는 다음 제한 사항을 염두에 두십시오.

* 현재 단일 권한(**[!UICONTROL 데이터 집합 대상 관리 및 활성화]**)에 데이터 집합 대상의 관리 및 활성화 권한이 포함되어 있습니다. 이러한 컨트롤은 나중에 더 세부적인 권한으로 분할됩니다. 를 검토합니다. [필수 권한](#permissions) 섹션을 참조하십시오.
* 현재 증분 파일만 내보낼 수 있으며 데이터 세트 내보내기에 종료 날짜를 선택할 수 없습니다.
* 내보낸 파일 이름은 현재 사용자 지정할 수 없습니다.
* 현재 UI는 대상으로 내보내는 데이터 세트를 삭제하지 못하도록 차단하지 않습니다. 대상으로 내보내는 데이터 세트는 삭제하지 마십시오. [데이터 세트 제거](#remove-dataset) 대상 데이터 플로우에서 삭제하기 전에 해당 데이터 플로우에서 해당 데이터를 삭제해야 합니다.
* 데이터 집합 내보내기에 대한 모니터링 지표는 현재 프로필 내보내기에 대한 숫자와 혼합되어 실제 내보내기 번호를 반영하지 않습니다.
