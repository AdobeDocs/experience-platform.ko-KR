---
keywords: Experience Platform;home;popular topics; delete dataflows
description: Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 데이터 흐름을 삭제하는 단계를 제공합니다.
solution: Experience Platform
title: 데이터 흐름 삭제
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# 데이터 흐름 삭제

Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 데이터 흐름을 삭제하는 [!UICONTROL 단계를] 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model] (XDM) 시스템](../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL 실시간 고객 프로필]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## UI를 사용하여 데이터 흐름 삭제

[Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택하여 **[!UICONTROL 소스 작업 영역에]** 액세스합니다. [ **[!UICONTROL 카탈로그]** ] 화면에는 계정 및 데이터 흐름을 만들 수 있는 다양한 소스가 표시됩니다. 각 소스에는 연결된 기존 계정 및 데이터 흐름 수가 표시됩니다.

데이터 **[!UICONTROL 흐름]** 을 선택하여 데이터 흐름 **[!UICONTROL 페이지에]** 액세스합니다.

![dataset-flow-activity](../../images/tutorials/delete/dataflows.png)

기존 데이터 흐름 목록이 나타납니다. 이 페이지에서는 소스, 사용자 이름, 실행 상태 및 마지막 실행 날짜와 같은 기존 데이터 프롤에 대한 정렬 가능한 정보의 목록입니다. 왼쪽 상단의 **단계 아이콘을** 선택하여 정렬합니다.

![데이터 흐름 목록](../../images/tutorials/delete/dataflows-list.png)

사용 가능한 소스 목록이 포함된 정렬 패널이 화면의 왼쪽에 나타납니다.
정렬 기능을 사용하여 둘 이상의 소스를 선택할 수 있습니다.

액세스할 소스를 선택하고 기본 인터페이스의 데이터 흐름 목록에서 삭제할 데이터 흐름을 찾습니다. 이 예에서 선택한 소스가 표시되고 데이터 흐름 이름 **[!DNL Azure Blob Storage]** 은 **[!UICONTROL 고객 프로필 데이터]**&#x200B;웨어입니다. 정렬 패널에서 여러 소스를 선택하는 경우 목록을 만든 날짜별로 정렬하기 때문에 최근에 만든 데이터 흐름 중에서 먼저 표시됩니다.

삭제할 데이터 흐름을 선택합니다.

![데이터 흐름 정렬](../../images/tutorials/delete/dataflows-sort.png)

선택한 **[!UICONTROL 데이터]** 흐름 및 예약 **[!UICONTROL 편집 옵션에 대한 정보가 포함된 속성]**&#x200B;패널이 화면의 오른쪽에나타납니다.

데이터 흐름을 삭제하려면 [삭제]를 **[!UICONTROL 선택합니다]**.

![데이터 흐름 정렬](../../images/tutorials/delete/dataflows-properties.png)

최종 확인 대화 상자가 나타나면 삭제 **[!UICONTROL 를]** 선택하여 프로세스를 완료합니다.

![delete](../../images/tutorials/delete/delete.png)

잠시 후 화면 하단에 녹색 확인 상자가 표시되어 성공적인 삭제를 확인합니다.

![확인](../../images/tutorials/delete/confirmed.png)

## 다음 단계

이 튜토리얼을 따라 소스 작업 영역에서 기존 계정 및 데이터 흐름 **[!UICONTROL 에]** 성공적으로 액세스했습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [[!DNL Real-time Customer Profile] 개요](../../../profile/home.md)
- [[!DNL Data Science Workspace] 개요](../../../data-science-workspace/home.md)