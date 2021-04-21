---
keywords: Experience Platform;홈;인기 항목;ID 그래프 뷰어;ID 그래프 뷰어;그래프 뷰어;그래프 뷰어;ID 네임스페이스;ID;ID;Service;ID 서비스;Identity Service;Identity Service
solution: Experience Platform
title: ID 그래프 뷰어 개요
topic-legacy: tutorial
description: ID 그래프는 특정 고객에 대해 서로 다른 ID 간의 관계를 보여주는 지도로, 고객이 다양한 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여줍니다.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# ID 그래프 뷰어 개요

ID 그래프는 특정 고객에 대해 서로 다른 ID 간의 관계를 보여주는 지도로, 고객이 다양한 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여줍니다. 모든 고객 ID 그래프는 고객 활동에 대한 대응으로 거의 실시간으로 Adobe Experience Platform Identity Service에서 통합 관리 및 업데이트됩니다.

플랫폼 사용자 인터페이스의 ID 그래프 뷰어를 사용하면 어떤 고객 ID가 함께 결합되어 있는지, 어떤 방식으로 결합되어 있는지 시각화하고 더 잘 이해할 수 있습니다. 뷰어를 사용하면 그래프의 여러 부분과 드래그 앤 인터랙션할 수 있으므로 복잡한 ID 관계를 검사하거나 보다 효율적으로 디버깅할 수 있을 뿐만 아니라 정보 활용 방법을 통해 투명도를 높일 수 있습니다.

## 자습서 비디오

다음 비디오는 ID 그래프 뷰어에 대한 이해를 지원하기 위한 것입니다.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## 시작하기

ID 그래프 뷰어를 사용하려면 관련 다양한 Adobe Experience Platform 서비스를 이해해야 합니다. ID 그래프 뷰어로 작업하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Identity Service]](../home.md):다양한 디바이스와 시스템에 ID를 연결함으로써 개별 고객과 고객의 행동을 보다 정확하게 파악할 수 있습니다.

### 용어

- **ID(노드):** ID 또는 노드는 일반적으로 한 엔티티에 고유한 데이터입니다. ID는 네임스페이스 및 ID 값으로 구성됩니다.
- **링크(가장자리):** 링크 또는 가장자리는 ID 간의 연결을 나타냅니다.
- **그래프(클러스터):** 그래프 또는 클러스터는 개인을 나타내는 ID 및 링크 그룹입니다.

## ID 그래프 뷰어에 액세스

UI에서 ID 그래프 뷰어를 사용하려면 왼쪽 탐색에서 **[!UICONTROL Identities]**&#x200B;을 선택한 다음 **[!UICONTROL Identity graph]** 탭을 선택합니다. **[!UICONTROL Identity Namespace]** 화면에서 **[!UICONTROL Select identity namespace]** 아이콘을 클릭하여 사용할 네임스페이스를 검색합니다.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

**[!UICONTROL Select identity namespace]** 패널이 나타납니다. 이 화면에는 네임스페이스의 **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]**, **[!UICONTROL Owner]**, **[!UICONTROL Last updated]** 날짜 및 **[!UICONTROL Description]**&#x200B;에 대한 정보를 포함하여 조직에서 사용할 수 있는 네임스페이스 목록이 포함되어 있습니다. 유효한 ID 값이 연결되어 있는 한 제공된 네임스페이스를 사용할 수 있습니다.

사용할 네임스페이스를 선택하고 **[!UICONTROL Select]**&#x200B;을 클릭하여 계속 진행합니다.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

네임스페이스를 선택하고 나면 **[!UICONTROL Identity value]** 텍스트 상자에 특정 고객에 해당하는 값을 입력하고 **[!UICONTROL View]**&#x200B;을 선택합니다.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### 데이터 세트에서 ID 그래프 뷰어에 액세스

데이터 집합 인터페이스를 사용하여 ID 그래프 뷰어에 액세스할 수도 있습니다. 데이터 집합 [!UICONTROL Browse] 페이지에서 상호 작용할 데이터 집합을 선택한 다음 **[!UICONTROL Preview dataset]**

![미리 보기 데이터 세트](../images/identity-graph-viewer/preview-dataset.png)

미리 보기 창에서 지문 아이콘을 선택하여 ID 그래프 뷰어를 통해 표시되는 ID를 확인합니다.

>[!TIP]
>
>지문 아이콘은 데이터 세트에 2개 이상의 ID가 있는 경우에만 나타납니다.

![지문](../images/identity-graph-viewer/fingerprint.png)

ID 그래프 뷰어가 나타납니다. 화면의 왼쪽에는 선택한 네임스페이스에 연결된 모든 ID와 입력한 ID 값이 표시된 ID 그래프가 있습니다. 각 ID 노드는 네임스페이스와 해당 ID 값으로 구성됩니다. ID를 선택하고 유지하여 그래프를 드래그하여 상호 작용할 수 있습니다. 또는 ID 위로 마우스를 가져가면 ID 값에 대한 정보를 볼 수 있습니다. 그래프 출력은 또한 화면 중앙에 놓기 목록으로 표시됩니다.

>[!IMPORTANT]
>
>ID 그래프에는 유효한 네임스페이스 및 ID 쌍은 물론 생성하기 위해 연결된 ID가 최소 2개 필요합니다. 그래프 뷰어에서 표시할 수 있는 최대 ID 수는 150개입니다. 자세한 내용은 아래의 [부록](#appendix) 섹션을 참조하십시오.

![identity-graph](../images/identity-graph-viewer/graph-viewer.png)

**[!UICONTROL Identities]** 테이블에서 강조 표시된 행을 업데이트하고 ID의 **[!UICONTROL Value]**, **[!UICONTROL Batch ID]** 및 그 **[!UICONTROL Last updated]** 날짜를 포함하는 오른쪽 레일에 제공된 정보를 업데이트하려면 ID를 선택합니다.

![select-identity](../images/identity-graph-viewer/select-identity.png)

그래프를 통해 필터링하고 **[!UICONTROL Identities]** 테이블 위에 있는 정렬 옵션을 사용하여 특정 네임스페이스를 분리할 수 있습니다. 드롭다운 메뉴에서 강조 표시할 네임스페이스를 선택합니다.

![filter by-namespace](../images/identity-graph-viewer/filter-namespace.png)

그래프 뷰어가 돌아와서 선택한 네임스페이스를 강조 표시합니다. 필터 옵션은 선택한 네임스페이스에 대한 정보만 반환하도록 **[!UICONTROL Identities]** 테이블도 업데이트합니다.

![필터링됨](../images/identity-graph-viewer/filtered.png)

그래프 뷰어 상자의 오른쪽 상단에는 확대 옵션이 포함되어 있습니다. 그래프를 확대하려면 **(+)** 아이콘을 선택하고 축소하려면 **(-)** 아이콘을 선택합니다.

![확대/축소](../images/identity-graph-viewer/zoom.png)

헤더에서 **[!UICONTROL Data source]**&#x200B;을 선택하여 배치에 대한 자세한 정보를 볼 수 있습니다. **[!UICONTROL Data source]** 테이블에는 그래프와 연결된 **[!UICONTROL Batch IDs]** 목록과 해당 **[!UICONTROL Linked IDs]**, 소스 스키마 및 통합 날짜가 표시됩니다.

![데이터 소스](../images/identity-graph-viewer/data-source-table.png)

ID 그래프 내의 링크를 선택하여 링크에 기여한 모든 소스 배치를 볼 수 있습니다.

![select-links](../images/identity-graph-viewer/select-edge.png)

또는 일괄 처리를 선택하여 이 일괄 처리에 기여한 모든 링크를 볼 수 있습니다.

![select-links](../images/identity-graph-viewer/select-batch.png)

ID 클러스터가 큰 ID 그래프도 ID 그래프 뷰어를 통해 액세스할 수 있습니다.

![대규모 클러스터](../images/identity-graph-viewer/large-cluster.png)

## 부록

다음 섹션에서는 ID 그래프 뷰어를 사용하여 작업하는 데 필요한 추가 정보를 제공합니다.

### 오류 메시지 이해

ID 그래프 뷰어에 액세스할 때 오류가 발생할 수 있습니다. 다음은 ID 그래프 뷰어로 작업할 때 주의해야 할 사전 요구 사항 및 제한 사항 목록입니다.

- 선택한 네임스페이스에 ID 값이 있어야 합니다.
- ID 그래프 뷰어는 생성하려면 최소 2개의 연결된 ID가 필요합니다. ID 값이 하나만 있고 연결된 ID가 없을 수 있으며 이 경우 이 값은 [!DNL Profile] 뷰어에만 존재합니다.
- ID 그래프 뷰어는 최대 150ID를 초과할 수 없습니다.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## 다음 단계

이 문서를 읽고 플랫폼 UI에서 고객의 ID 그래프를 살펴보는 방법을 알아보았습니다. 플랫폼의 ID에 대한 자세한 내용은 [ID 서비스 개요](../home.md)를 참조하십시오.

## Changelog

| Date | 작업 |
| ---- | ------ |
| 2021-01 | <ul><li>인제스트한 스트리밍 데이터 및 비프로덕션 샌드박스에 대한 지원을 추가했습니다.</li><li>사소한 버그가 수정되었습니다.</li></ul> |
| 2021-02 | <ul><li>ID 그래프 뷰어는 데이터 집합 미리 보기를 통해 액세스할 수 있습니다.</li><li>사소한 버그가 수정되었습니다.</li><li>ID 그래프 뷰어는 일반적으로 사용할 수 있게 됩니다.</li></ul> |
