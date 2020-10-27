---
keywords: Experience Platform;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: 데이터 집합 사용자 가이드
topic: datasets
description: 이 데이터 집합 사용자 안내서는 Adobe Experience Platform 사용자 인터페이스 내의 데이터 집합을 사용할 때 일반적인 작업을 수행하는 방법에 대한 지침을 제공합니다.
translation-type: tm+mt
source-git-commit: 1c00456ee06c1fc09c8e4ce070c90255f51811e1
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# 데이터 집합 사용자 가이드

이 사용자 안내서에서는 Adobe Experience Platform 사용자 인터페이스 내의 데이터 세트를 사용하여 작업할 때 일반적인 작업을 수행하는 방법에 대한 지침을 제공합니다.

## 시작하기

이 사용 안내서를 보려면 다음 Adobe Experience Platform 구성 요소에 대한 작업 정보가 필요합니다.

* [데이터 집합](overview.md):데이터 지속성을 위한 스토리지 및 관리 구성 [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기](../../xdm/tutorials/create-schema-ui.md):사용자 인터페이스 내에서 사용자 정의 XDM 스키마를 사용하여 고유한 사용자 정의 XDM 스키마 [!DNL Schema Editor] 를 만드는 방법을 [!DNL Platform] 학습합니다.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md):고객 데이터 사용과 관련된 규정, 제한 사항 및 정책을 준수할 수 있습니다.

## 데이터 집합 보기

UI [!DNL Experience Platform] 에서 왼쪽 탐색 **[!UICONTROL 의 데이터 세트]** 를 클릭하여 **[!UICONTROL 데이터 집합]** 대시보드를 엽니다. 대시보드에는 조직에 사용할 수 있는 모든 데이터 집합이 나열됩니다. 나열된 각 데이터 세트에 대한 세부 사항(예: 해당 이름, 데이터 세트에서 준수되는 스키마, 가장 최근 통합 실행 상태)이 표시됩니다.

![](../images/datasets/user-guide/browse_datasets.png)

데이터 세트 이름을 클릭하여 데이터 세트 **[!UICONTROL 활동]** 화면에 액세스하고 선택한 데이터 세트에 대한 세부 사항을 확인합니다. 활동 탭에는 사용 중인 메시지 비율과 성공 및 실패한 배치의 목록을 시각화하는 그래프가 포함되어 있습니다.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## 데이터 세트 미리 보기

데이터 **[!UICONTROL 집합 활동]** 화면에서 화면 오른쪽 상단 근처에 있는 데이터 집합 **** 미리 보기를 클릭하여 최대 100개의 데이터 행을 미리 봅니다. 데이터 세트가 비어 있으면 미리 보기 링크가 비활성화되고 미리 보기를 사용할 수 없다고 표시됩니다.

![](../images/datasets/user-guide/click_to_preview.png)

미리 보기 창에서 데이터 세트에 대한 스키마의 계층 구조 보기가 오른쪽에 표시됩니다.

![](../images/datasets/user-guide/preview_dataset.png)

데이터에 액세스하기 위한 보다 강력한 방법을 위해, 데이터 [!DNL Experience Platform] 와 같은 다운스트림 서비스 [!DNL Query Service] [!DNL JupyterLab] 를 제공하고, 자세한 내용은 다음 문서를 참조하십시오.

* [쿼리 서비스 개요](../../query-service/home.md)
* [JupiterLab 사용 안내서](../../data-science-workspace/jupyterlab/overview.md)

## 데이터 세트 만들기 {#create}

새 데이터 세트를 만들려면 데이터 집합 **[!UICONTROL 대시보드에서]** 데이터 집합 **[!UICONTROL 만들기를 클릭하여]** 시작합니다.

![](../images/datasets/user-guide/click_to_create.png)

다음 화면에는 새 데이터 세트를 만들기 위한 다음 두 가지 옵션이 표시됩니다.

* [스키마에서 데이터 집합 만들기](#schema)
* [CSV 파일에서 데이터 집합 만들기](#csv)

### 기존 스키마를 사용하여 데이터 집합 만들기 {#schema}

데이터 집합 **[!UICONTROL 만들기]** 화면에서 **[!UICONTROL 스키마에서]** 데이터 집합 만들기를 클릭하여 빈 데이터 집합을 새로 만듭니다.

![](../images/datasets/user-guide/create_dataset_schema.png)

스키마 **[!UICONTROL 선택]** 단계가 나타납니다. 스키마 목록을 탐색하고 다음 을 클릭하기 전에 데이터 세트에서 유지할 스키마를 **[!UICONTROL 선택합니다]**.

![](../images/datasets/user-guide/select_schema.png)

데이터 세트 **[!UICONTROL 구성]** 단계가 나타납니다. 데이터 세트에 이름과 선택적 설명을 제공한 다음 **[!UICONTROL 마침을]** 클릭하여 데이터 세트를 만듭니다.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### CSV 파일로 데이터 집합 만들기 {#csv}

CSV 파일을 사용하여 데이터 세트를 만들면, 제공된 CSV 파일과 일치하는 구조를 데이터 세트에 제공하기 위해 임시 스키마가 만들어집니다. 데이터 집합 **[!UICONTROL 만들기]** 화면에서 CSV 파일에서 **[!UICONTROL 데이터 집합 만들기 상자를 클릭합니다]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

구성 **[!UICONTROL 단계가]** 나타납니다. 데이터 세트에 이름과 선택적 설명을 제공한 다음 다음을 **[!UICONTROL 클릭합니다]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

데이터 **[!UICONTROL 추가]** 단계가 나타납니다. CSV 파일을 화면 가운데로 드래그 앤 드롭하여 업로드하거나, **[!UICONTROL 찾아보기를]** 클릭하여 파일 디렉토리를 탐색합니다. 파일 크기는 최대 10GB입니다. CSV 파일이 업로드되면 **[!UICONTROL 저장을]** 클릭하여 데이터 세트를 만듭니다.

>[!NOTE]
>
>CSV 열 이름은 영숫자 문자로 시작해야 하며 문자, 숫자 및 밑줄만 포함할 수 있습니다.

![](../images/datasets/user-guide/add_csv_data.png)

## 실시간 고객 프로파일에 대한 데이터 세트 활성화

모든 데이터 세트에 인제스트한 데이터로 고객 프로파일을 강화할 수 있습니다. 이렇게 하려면 데이터 세트가 준수하는 스키마는 에서 사용할 수 있도록 호환되어야 합니다 [!DNL Real-time Customer Profile]. 호환 스키마는 다음 요구 사항을 충족합니다.

* 스키마에 ID 속성으로 지정된 속성이 하나 이상 있습니다.
* 스키마에 기본 ID로 정의된 ID 속성이 있습니다.

스키마 활성화에 대한 자세한 내용 [!DNL Profile]은 스키마 편집기 사용자 [안내서를 참조하십시오](../../xdm/tutorials/create-schema-ui.md).

프로필에 대한 데이터 세트를 활성화하려면 해당 데이터 세트 **[!UICONTROL 활동]** 화면에 액세스하고 **[!UICONTROL 속성]** 열 내에서 **[!UICONTROL 프로필]** 전환을클릭합니다. 활성화되면 데이터 세트에 수집되는 데이터도 고객 프로필을 채우는 데 사용됩니다.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

데이터 세트에 이미 데이터가 포함되어 있고 이 데이터 세트에 대해 활성화된 경우 기존 데이터 [!DNL Profile]는 이 데이터 세트에 사용되지 않습니다 [!DNL Profile]. 데이터 세트를 활성화한 후 기존 데이터 [!DNL Profile]를 다시 인제스트하여 고객 프로필을 채우는 것이 좋습니다.

## 데이터 세트에 대한 데이터 거버넌스 관리 및 적용

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블에 대한 자세한 내용은 [데이터 거버넌스 개요를](../../data-governance/home.md) 참조하거나 [데이터 세트에 레이블을 적용하는 방법에 대한 지침은 데이터 사용 레이블 사용자 안내서](../../data-governance/labels/overview.md) 를 참조하십시오.

## 데이터 집합 삭제

먼저 데이터 세트 **[!UICONTROL 활동]** 화면에 액세스하여 데이터 세트를 삭제할 수 있습니다. 그런 다음 데이터 **[!UICONTROL 세트]** 삭제를 클릭하여 삭제합니다.

>[!NOTE]
>
>Adobe 애플리케이션 및 서비스(예: Adobe Analytics, Adobe Audience Manager 또는 [!DNL Offer Decisioning])에서 생성 및 활용하는 데이터 세트는 삭제할 수 없습니다.

![](../images/datasets/user-guide/delete_dataset.png)

확인 상자가 나타납니다. 데이터 **[!UICONTROL 세트]** 삭제를 확인하려면 삭제를 클릭합니다.

![](../images/datasets/user-guide/confirm_delete.png)

## 프로필 사용 데이터 집합 삭제

데이터 세트에 대해 활성화된 경우 UI를 통해 데이터 세트 [!DNL Profile]를 삭제하면 데이터 세트 수집이 비활성화되지만 백엔드의 데이터 세트는 자동으로 삭제되지 않습니다. 제공된 프로필 및 ID 데이터를 포함한 데이터 세트를 완전히 삭제하려면 추가 삭제 요청이 있어야 합니다. 저장소에서 데이터를 제대로 삭제하는 방법에 대한 단계는 프로필 시스템 작업(&quot;요청 삭제&quot;라고도 함)에 대한 [!DNL Profile] API [!DNL Real-time Customer Profile] 하위 가이드를 참조하십시오 [](../../profile/api/profile-system-jobs.md).

## 데이터 수집 모니터링

UI [!DNL Experience Platform] 의 왼쪽 탐색 **[!UICONTROL 에서]** 모니터링 을 클릭합니다. 모니터링 **[!UICONTROL 대시보드를]** 사용하면 일괄 처리 또는 스트리밍 통합 중 하나에서 인바운드 데이터의 상태를 볼 수 있습니다. 개별 배치의 상태를 보려면 일괄 처리( **[!UICONTROL end-to-end]** ) 또는 **[!UICONTROL 스트리밍 종단간]**&#x200B;을 클릭합니다. 대시보드에는 성공, 실패 또는 진행 중인 일괄 처리 또는 스트리밍 통합 실행이 모두 나열됩니다. 각 목록에서는 배치 ID, 대상 데이터 세트 이름, 수집되는 레코드 수 등 일괄 처리에 대한 세부 정보를 제공합니다. 대상 데이터 세트에 대해 활성화된 경우 [!DNL Profile]인제스트된 ID 및 프로필 레코드 수도 표시됩니다.

![](../images/datasets/user-guide/batch_listing.png)

개별 **[!UICONTROL 배치 ID를]** 클릭하여 **[!UICONTROL 배치 개요]** 대시보드에 액세스하고 일괄 처리를 인제스트하지 못한 경우 오류 로그를 비롯한 일괄 처리에 대한 세부 정보를 볼 수 있습니다.

![](../images/datasets/user-guide/batch_overview.png)

배치를 삭제하려면 대시보드 오른쪽 상단에 있는 일괄 **[!UICONTROL 삭제]** 를 클릭하면 됩니다. 이렇게 하면 배치가 원래 수집했던 데이터 세트에서 해당 레코드가 제거됩니다.

![](../images/datasets/user-guide/delete_batch.png)

## 다음 단계

이 사용자 안내서에서는 [!DNL Experience Platform] 사용자 인터페이스에서 데이터 세트를 사용하여 작업할 때 일반적인 작업을 수행하는 지침을 제공합니다. 데이터 세트와 관련된 일반적인 [!DNL Platform] 워크플로우를 수행하는 단계는 다음 자습서를 참조하십시오.

* [API를 사용하여 데이터 세트 만들기](create.md)
* [데이터 액세스 API를 사용하여 데이터 집합 데이터 쿼리](../../data-access/home.md)
* [API를 사용하여 실시간 고객 프로필 및 ID 서비스에 대한 데이터 세트 구성](../../profile/tutorials/dataset-configuration.md)