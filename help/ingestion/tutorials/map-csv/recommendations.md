---
title: AI 생성 Recommendations(베타)를 사용하여 XDM 스키마에 CSV 파일 매핑
description: 이 자습서에서는 AI에서 생성한 권장 사항을 사용하여 XDM 스키마에 CSV 파일을 매핑하는 방법을 설명합니다.
source-git-commit: d6f858af8bc44be74b1aaf12b973fb6818c1b2a5
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# AI에서 생성된 권장 사항(베타)을 사용하여 XDM 스키마에 CSV 파일 매핑

>[!IMPORTANT]
>
>이 기능은 현재 베타 버전이며 조직에서 아직 액세스할 수 없을 수 있습니다. 설명서 및 기능은 변경될 수 있습니다.
>
>Platform에서 일반적으로 사용할 수 있는 CSV 매핑 기능에 대한 자세한 내용은 다음 문서를 참조하십시오 [기존 스키마에 CSV 파일 매핑](./existing-schema.md).

CSV 데이터를 로 수집하려면 [!DNL Adobe Experience Platform]를 지정하는 경우 데이터를 [!DNL Experience Data Model] (XDM) 스키마. 매핑할 항목을 선택할 수 있습니다 [기존 스키마](./existing-schema.md)로 설정되지만, 사용할 스키마나 구성 방법을 정확히 모를 경우 Platform UI 내에서 ML(기계 학습) 모델을 기반으로 한 동적 권장 사항을 사용할 수 있습니다.

## 시작하기

이 자습서에서는 다음 구성 요소를 이해하고 있어야 합니다 [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
   * 최소한, 당신은 그 개념을 이해해야 한다 [xdm의 동작](../../../xdm/home.md#data-behaviors)별로 보고서를 분류할 경우에 대비하여 [!UICONTROL 프로필] 클래스(레코드 동작) 또는 [!UICONTROL ExperienceEvent] 클래스(시계열 동작)
* [일괄 수집](../../batch-ingestion/overview.md): 메서드를 사용하는 방법 [!DNL Platform] 사용자가 제공한 데이터 파일에서 데이터를 가져옵니다.
* [Adobe Experience Platform 데이터 준비](../../batch-ingestion/overview.md): 수집된 데이터를 XDM 스키마에 맞게 매핑하고 변형할 수 있는 기능 세트입니다. 에 대한 문서 [데이터 준비 함수](../../../data-prep/functions.md) 는 스키마 매핑에 특히 관련이 있습니다.

## 데이터 흐름 세부 정보 제공

Experience Platform UI에서 **[!UICONTROL 소스]** 을 클릭합니다. 설정 **[!UICONTROL 카탈로그]** 보기, 로 이동합니다. **[!UICONTROL 로컬 시스템]** 카테고리. 아래 **[!UICONTROL 로컬 파일 업로드]**, 선택 **[!UICONTROL 데이터 추가]**.

![다음 [!UICONTROL 소스] 플랫폼 UI의 카탈로그, [!UICONTROL 데이터 추가] 아래에 [!UICONTROL 로컬 파일 업로드] 선택](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

다음 **[!UICONTROL CSV XDM 스키마 매핑]** 워크플로우가 나타나고, **[!UICONTROL 데이터 흐름 세부 정보]** 단계.

선택 **[!UICONTROL ML 권장 사항을 사용하여 새 스키마 만들기]**&#x200B;새 컨트롤이 나타납니다. 매핑할 CSV 데이터에 적절한 클래스를 선택합니다([!UICONTROL 프로필] 또는 [!UICONTROL ExperienceEvent]). 드롭다운 메뉴를 사용하여 비즈니스에 대한 관련 산업을 선택하거나, 제공된 카테고리가 적용되지 않는 경우 비워 둘 수 있습니다(선택적). 조직이 [business-to-business(B2B)](../../../xdm/tutorials/relationship-b2b.md) 모델, **[!UICONTROL B2B 데이터]** 확인란을 선택합니다.

![다음 [!UICONTROL 데이터 흐름 세부 정보] html 권장 사항 선택 사항을 선택한 상태로 단계가 진행됩니다. [!UICONTROL 프로필] 클래스 및 [!UICONTROL 통신] 업계](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

여기에서 CSV 데이터에서 만들 스키마의 이름과 해당 스키마 아래에 수집된 데이터가 포함될 출력 데이터 세트의 이름을 입력합니다.

계속하기 전에 데이터 플로우에 대해 다음 추가 기능을 선택적으로 구성할 수 있습니다.

| 입력 이름 | 설명 |
| --- | --- |
| [!UICONTROL 설명] | 데이터 흐름에 대한 설명입니다. |
| [!UICONTROL 오류 진단] | 활성화되면 새로 수집된 배치에 대해 오류 메시지가 생성되며, 이 생성은에서 해당 배치를 가져올 때 볼 수 있습니다 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 부분 수집] | 활성화되면 지정된 오류 임계값 내에서 새 배치 데이터에 대한 유효한 레코드를 수집합니다. 이 임계값을 사용하여 전체 배치에 실패하기 전에 허용 가능한 오류 비율을 구성할 수 있습니다. |
| [!UICONTROL 데이터 흐름 세부 정보] | CSV 데이터를 플랫폼으로 가져올 데이터 흐름의 이름 및 선택적 설명을 제공합니다. 이 워크플로우를 시작할 때 데이터 로드에 자동으로 기본 이름이 할당됩니다. 이름 변경은 선택 사항입니다. |
| [!UICONTROL 경고] | 다음 목록에서 선택 [제품 내 경고](../../../observability/alerts/overview.md) 데이터 흐름 상태가 시작되면 받게 될 데이터 흐름 상태와 관련된 정보를 받게 됩니다. |

{style=&quot;table-layout:auto&quot;}

데이터 흐름 구성을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

![다음 [!UICONTROL 데이터 흐름 세부 정보] 섹션이 완료되었습니다.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 데이터 선택

설정 **[!UICONTROL 데이터 선택]** 단계별로 왼쪽 열을 사용하여 CSV 파일을 업로드합니다. 선택할 수 있습니다 **[!UICONTROL 파일 선택]** 파일 탐색기 대화 상자를 열어 파일을 선택하거나 파일을 직접 열에 드래그하여 놓을 수 있습니다.

![다음 [!UICONTROL 파일 선택] 단추 및 아래에 강조 표시된 드래그 앤 드롭 영역 [!UICONTROL 데이터 선택] 단계](../../images/tutorials/map-csv-recommendations/upload-files.png)

파일을 업로드한 후 수신한 데이터의 처음 10개 행을 보여주는 샘플 데이터 섹션이 표시되어 올바르게 업로드되었는지 확인할 수 있습니다. 선택 **[!UICONTROL 다음]** 계속하십시오.

![샘플 데이터 행은 작업 공간 내에서 채워집니다](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 스키마 매핑 구성

ML 모델은 데이터 흐름 구성 및 업로드된 CSV 파일을 기반으로 새 스키마를 생성하기 위해 실행됩니다. 프로세스가 완료되면 [!UICONTROL 매핑] 단계는 생성된 스키마 구조의 전체 탐색 가능한 보기와 함께 각 개별 필드에 대한 매핑을 표시하도록 채워집니다.

![다음 [!UICONTROL 매핑] UI의 단계에 매핑되어 있는 모든 CSV 필드와 결과 스키마 구조를 표시합니다](../../images/tutorials/map-csv-recommendations/schema-generated.png)

여기에서 원할 경우 [필드 매핑 편집](#edit-mappings) 또는 [연결된 필드 그룹을 변경합니다.](#edit-schema) 필요에 따라 만족하면 을 선택합니다. **[!UICONTROL 완료]** 매핑을 완료하고 이전에 구성한 데이터 흐름을 시작하려면 다음을 수행하십시오. CSV 데이터는 시스템에 수집되고, 생성된 스키마 구조를 기반으로 데이터 세트를 채우므로 다운스트림 Platform 서비스에서 사용할 수 있습니다.

![다음 [!UICONTROL 완료] 단추를 선택하고 CSV 매핑 프로세스를 완료합니다](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 필드 매핑 편집 {#edit-mappings}

필드 매핑 미리 보기를 사용하여 기존 매핑을 편집하거나 완전히 제거합니다. UI에서 매핑 세트를 관리하는 방법에 대한 자세한 내용은 [데이터 준비 매핑에 대한 UI 안내서](../../../data-prep/ui/mapping.md#mapping-interface).

### 필드 그룹 편집 {#edit-field-groups}

CSV 필드는 ML 모델을 사용하여 기존 XDM 필드 그룹에 자동으로 매핑됩니다. 특정 CSV 필드에 대한 필드 그룹을 변경하려면, 을(를) 선택합니다 **[!UICONTROL 편집]** 스키마 트리 옆에 있습니다.

![다음 [!UICONTROL 편집] 스키마 트리 옆에 있는 단추 선택](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

매핑의 모든 필드에 대한 표시 이름, 데이터 유형 및 필드 그룹을 편집할 수 있는 대화 상자가 나타납니다. 편집 아이콘(![편집 아이콘](../../images/tutorials/map-csv-recommendations/edit-icon.png))을 클릭하여 선택 전에 오른쪽 열에서 세부 사항을 편집합니다 **[!UICONTROL 적용]**.

![변경 중인 소스 필드에 대한 권장 필드 그룹](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

소스 필드에 대한 스키마 권장 사항 조정을 마치면 를 선택합니다 **[!UICONTROL 저장]** 변경 사항을 적용하려면

## 다음 단계

이 안내서에서는 AI에서 생성한 권장 사항을 사용하여 XDM 스키마에 CSV 파일을 매핑하는 방법을 다룹니다. 이렇게 하면 배치 수집을 통해 해당 데이터를 플랫폼으로 가져올 수 있습니다.

CSV 파일을 기존 스키마에 매핑하는 단계는 다음을 참조하십시오. [기존 스키마 매핑 워크플로우](./existing-schema.md). 사전 빌드된 소스 연결을 통해 실시간으로 플랫폼으로 데이터를 스트리밍하는 방법에 대한 자세한 내용은 [소스 개요](../../../sources/home.md).
