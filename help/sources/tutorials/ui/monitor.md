---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 흐름 모니터링 및 삭제
topic: overview
translation-type: tm+mt
source-git-commit: f08ad2c9cc48c08bcdc0e278481992e8789000b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# 데이터 흐름 모니터링 및 삭제

Adobe Experience Platform의 소스 커넥터는 외부에서 가져온 데이터를 예약된 기준으로 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 기존 계정 및 데이터 흐름을 보는 단계를 *[!UICONTROL 제공합니다]* . 또한 이 자습서에서는 *[!UICONTROL 소스 작업 영역에서 데이터 흐름을 삭제하는 단계도]* 제공합니다.

## 시작하기

이 자습서에서는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [XDM(Experience Data Model) 시스템](../../../xdm/home.md): 고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [실시간 고객 프로필](../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 계정 모니터링

Adobe Experience Platform에 [로그인한](https://platform.adobe.com) 다음 왼쪽 탐색 **[!UICONTROL 모음에서]** 소스 *[!UICONTROL 를 선택하여]* 소스 작업 영역에액세스합니다. [ *[!UICONTROL 카탈로그]* ] 화면에는 계정 및 데이터 흐름을 만들 수 있는 다양한 소스가 표시됩니다. 각 소스에는 연결된 기존 계정 및 데이터 흐름 수가 표시됩니다.

상단 헤더에서 *[!UICONTROL 계정을]* 선택하여 기존 계정을 봅니다.

![카탈로그](../../images/tutorials/monitor/catalog.png)

계정 *[!UICONTROL 페이지가]* 나타납니다. 이 페이지에는 소스, 사용자 이름, 데이터 흐름 수 및 작성 날짜에 대한 정보를 비롯하여 볼 수 있는 계정 목록이 있습니다.

왼쪽 상단에 있는 단계 아이콘을 선택하여 정렬 창을 실행합니다.

![계정](../../images/tutorials/monitor/accounts-list.png)

정렬 패널을 사용하면 특정 소스의 계정에 액세스할 수 있습니다. 작업할 소스를 선택하고 오른쪽 목록에서 계정을 선택합니다.

![계정 선택](../../images/tutorials/monitor/accounts-sort.png)

계정 *[!UICONTROL 페이지에서]* 액세스한 계정과 연결된 기존 데이터 흐름 목록을 볼 수 있습니다. 보려는 데이터 흐름을 선택합니다.

![계정 페이지](../../images/tutorials/monitor/dataflows.png)

데이터 *[!UICONTROL 흐름 활동]* 화면이 나타납니다. 이 페이지는 그래프 형식으로 소비되는 메시지 비율을 표시합니다.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

## 데이터 흐름 모니터링

데이터 파일은 계정을 보지 않고도 *[!UICONTROL 카탈로그]* 페이지에서 직접 액세스할 수 *[!UICONTROL 있습니다]*. 상단 헤더에서 *[!UICONTROL 데이터 흐름]* 을 선택하여 기존 데이터 흐름 목록을 봅니다.

![카탈로그 데이터 흐름](../../images/tutorials/monitor/catalog-dataflows.png)

기존 데이터 흐름 목록이 나타납니다. 이 페이지에서는 소스, 사용자 이름, 데이터 흐름 수 및 상태에 대한 정보를 비롯하여 볼 수 있는 데이터 흐름 목록이 있습니다. 왼쪽 상단의 단계 아이콘을 선택하여 정렬합니다.

![데이터 흐름 목록](../../images/tutorials/monitor/dataflows-list.png)

정렬 패널이 나타납니다. 스크롤 메뉴에서 액세스할 소스를 선택하고 오른쪽의 목록에서 데이터 흐름을 선택합니다.

![데이터 흐름 정렬](../../images/tutorials/monitor/dataflows-sort.png)

데이터 *[!UICONTROL 흐름 활동]* 화면이 나타납니다. 이 페이지는 그래프 형식으로 소비되는 메시지 비율을 표시합니다.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

데이터 흐름 및 섭취 모니터링에 대한 자세한 내용은 스트리밍 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오](../../../ingestion/quality/monitor-data-flows.md).

## 데이터 흐름 삭제

데이터 흐름 화면에 액세스하여 잘못 작성되었거나 더 이상 필요하지 않은 데이터 흐름을 삭제할 수 있습니다. 정렬 단계 아이콘을 사용하여 삭제할 데이터 흐름을 찾아 데이터 흐름을 선택하여 **[!UICONTROL 속성]** 패널을 엽니다.

데이터 흐름을 삭제하려면 오른쪽 **[!UICONTROL 상단의]** 속성에서 삭제를 선택합니다.

![데이터 흐름 삭제](../../images/tutorials/monitor/dataflows-sort-delete.png)

최종 확인 메시지가 나타납니다. 삭제를 **[!UICONTROL 선택하여]** 확인합니다.

![확인-삭제](../../images/tutorials/monitor/confirm-delete.png)

잠시 후 화면 하단에 녹색 확인 상자가 표시되어 성공적인 삭제를 확인합니다.

![delete-successful](../../images/tutorials/monitor/deletion-confirmed.png)

또는 [계정] 화면에서 데이터 흐름 *[!UICONTROL 을]* 삭제할 수 있습니다. 정렬 단계 아이콘을 사용하여 액세스할 계정을 찾고 목록에서 계정을 선택합니다.

![계정 선택](../../images/tutorials/monitor/accounts-sort.png)

계정 *[!UICONTROL 페이지가]* 나타납니다. 삭제할 데이터 흐름을 선택한 다음 속성 패널에서 **[!UICONTROL 삭제]** 를 선택하여 프로세스를 완료합니다.

![계정 삭제](../../images/tutorials/monitor/accounts-delete.png)

위의 확인 단계를 따라 프로세스를 완료합니다.

## 다음 단계

이 튜토리얼을 따라 소스 작업 영역에서 기존 계정 및 데이터 흐름 *[!UICONTROL 에]* 성공적으로 액세스했습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../profile/home.md)
- [데이터 과학 작업 공간 개요](../../../data-science-workspace/home.md)