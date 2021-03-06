---
keywords: Experience Platform;홈;인기 항목;고객 속성
solution: Experience Platform
title: UI에서 고객 속성 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: UI에서 소스 연결을 만들어 고객 특성 프로필 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: b1b820c93ff1731b797f2b5e3ace7d2d6995b98b
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# UI에서 고객 속성 소스 연결 만들기

이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 소스 연결을 만드는 단계를 제공합니다. 고객 속성에 대한 자세한 내용은 [고객 속성 개요](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=ko-KR).

>[!IMPORTANT]
>
>현재 고객 속성 소스는 데이터 흐름 활성화 또는 비활성화를 지원하지 않습니다.

## 소스 연결 만들기

>[!NOTE]
>
>고객 속성 프로필 데이터에 대해 소스 연결을 이미 설정한 경우 소스와 연결하는 옵션이 비활성화됩니다.

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 연결을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL Adobe 애플리케이션] 카테고리, 선택 **[!UICONTROL 고객 속성]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 고객 속성 데이터 소스 선택

다음 [!UICONTROL 데이터 추가] 화면에 고객 속성에 대해 사용 가능한 모든 데이터 소스가 표시됩니다. 고객 속성 소스 연결당 하나의 데이터 세트만 선택할 수 있습니다.

>[!NOTE]
>
>필드 그룹, 스키마 및 데이터 세트는 흐름 프로비저닝의 일부로서 즉시 생성됩니다. 이러한 수정 사항은 그대로 유지되며, 필요한 경우 수동으로 삭제해야 합니다.

스키마 진화는 고객 특성 소스에서 지원되지 않습니다. 고객 특성 데이터 소스의 스키마 입력이 변경되면 Platform과 호환되지 않습니다. 해결 방법으로, 관련 데이터 세트, 스키마 및 필드 그룹과 함께 기존 고객 속성 데이터 플로우를 삭제한 다음 업데이트된 스키마 및 데이터 소스를 사용하여 새 고객 속성 데이터 플로우를 만들 수 있습니다.

>[!IMPORTANT]
>
>고객 속성 데이터 흐름을 삭제할 수 있지만 해당 데이터 세트는 데이터 흐름을 삭제한 후에도 계속 유지됩니다. 다음 안내서를 참조하십시오. [데이터 집합 삭제](../../../../../catalog/datasets/user-guide.md) 데이터 세트를 수동으로 삭제하는 방법에 대한 절차를 설명합니다.

새 연결을 만들려면 목록에서 데이터 소스를 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 데이터 흐름 세부 정보 제공

다음 [!UICONTROL 데이터 흐름 세부 정보] 데이터 흐름의 이름과 간단한 설명을 입력할 수 있는 단계가 나타납니다. 이 프로세스 중에 [!UICONTROL 오류 진단], [!UICONTROL 부분 수집], 및 [!UICONTROL 경고].

[!UICONTROL 오류 진단] 에서는 데이터 플로우에서 발생하는 모든 잘못된 레코드에 대해 자세한 오류 메시지를 생성하는 반면, [!UICONTROL 부분 수집] 수동으로 정의하는 특정 임계값까지 오류가 포함된 데이터를 수집할 수 있습니다. 자세한 내용은 [부분 배치 수집 개요](../../../../../ingestion/batch-ingestion/partial.md) 추가 정보.

경고를 활성화하여 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 소스 경고 구독](../../alerts.md).

데이터 집합에 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

![데이터 흐름 세부 정보](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 데이터 흐름 검토

다음 [!UICONTROL 검토] 새 데이터 흐름을 만들기 전에 검토할 수 있는 단계가 나타납니다. 세부 사항은 다음 범주 내에 그룹화됩니다.

* **[!UICONTROL 연결]**: 소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 수를 표시합니다.
* **[!UICONTROL 데이터 세트 및 맵 필드 할당]**: 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 세트를 표시합니다.

![검토](../../../../images/tutorials/create/customer-attributes/review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 생성됩니다. 초기 수집이 완료되면 고객 특성 프로필 데이터를 다음과 같은 다운스트림 Platform 서비스에서 사용할 수 있습니다 [!DNL Real-time Customer Profile] 및 [!DNL Segmentation Service]. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
