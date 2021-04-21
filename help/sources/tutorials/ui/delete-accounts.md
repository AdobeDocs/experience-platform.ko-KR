---
keywords: Experience Platform;home;popular topics계정 삭제
description: Adobe Experience Platform의 소스 커넥터는 예약된 기준에 따라 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 계정을 삭제하는 절차를 제공합니다.
solution: Experience Platform
title: UI에서 소스 연결 계정 삭제
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 원본 연결 계정 삭제

Adobe Experience Platform의 소스 커넥터는 예약된 기준에 따라 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 **[!UICONTROL Sources]** 작업 영역에서 계정을 삭제하는 절차를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## UI를 사용하여 계정 삭제

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL Sources]**&#x200B;를 선택하여 **[!UICONTROL Sources]** 작업 영역에 액세스합니다. **[!UICONTROL Catalog]** 화면에는 계정 및 데이터 흐름을 만들 수 있는 다양한 소스가 표시됩니다. 각 소스에는 연관된 기존 계정 및 데이터 흐름 수가 표시됩니다.

**[!UICONTROL Accounts]** 페이지에 액세스하려면 **[!UICONTROL Accounts]**&#x200B;을 선택합니다.

![카탈로그 계정](../../images/tutorials/delete-accounts/catalog.png)

기존 계정 목록이 나타납니다. 이 페이지에는 소스, 사용자 이름, 연결된 데이터 흐름 및 만든 날짜와 같은 기존 계정에 대한 정렬 가능한 정보 목록이 표시됩니다. 정렬할 왼쪽 위에 있는 **단계 아이콘**&#x200B;을 선택합니다.

![데이터 흐름 목록](../../images/tutorials/delete-accounts/accounts.png)

사용 가능한 소스 목록이 포함된 정렬 패널이 화면의 왼쪽에 나타납니다. 정렬 기능을 사용하여 둘 이상의 소스를 선택할 수 있습니다.

액세스할 소스를 선택하고 기본 인터페이스의 계정 목록에서 삭제할 계정을 찾습니다. 이 예에서 선택한 소스는 **[!DNL Azure Blob Storage]**&#x200B;이고 계정 이름은 **[!UICONTROL blobTestConnector]**&#x200B;입니다. 정렬 패널에서 여러 소스를 선택하면 목록이 만든 날짜별로 정렬되므로 최근에 만든 계정이 먼저 표시됩니다.

삭제할 계정을 선택합니다.

![데이터 흐름 정렬](../../images/tutorials/delete-accounts/sort.png)

선택한 계정에 대한 정보가 포함된 **[!UICONTROL Properties]** 패널이 화면의 오른쪽에 나타납니다.

삭제할 계정의 이름 옆에 줄임표(`...`)를 선택합니다. **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** 및 **[!UICONTROL Delete]**&#x200B;에 대한 옵션을 제공하는 팝업 패널이 나타납니다. 계정을 삭제하려면 **[!UICONTROL Delete]**&#x200B;을(를) 선택합니다.

![데이터 흐름 정렬](../../images/tutorials/delete-accounts/delete.png)

최종 확인 대화 상자가 나타나면 **[!UICONTROL Delete]**&#x200B;을 선택하여 프로세스를 완료합니다.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## 다음 단계

이 튜토리얼을 따라 **[!UICONTROL Sources]** 작업 영역을 사용하여 기존 계정을 성공적으로 삭제했습니다.

[!DNL Flow Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [Flow Service API](../../tutorials/api/delete.md)를 사용하여 연결을 삭제하는 튜토리얼을 참조하십시오.
