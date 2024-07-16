---
keywords: Experience Platform;홈;인기 항목;계정 업데이트
description: 경우에 따라 기존 소스 계정의 세부 사항을 업데이트해야 할 수도 있습니다. 소스 작업 공간에서는 이름, 설명 및 자격 증명을 포함하여 기존 배치 또는 스트리밍 연결의 세부 정보를 추가, 편집 및 삭제할 수 있는 기능을 제공합니다.
solution: Experience Platform
title: UI에서 Source 연결 계정 세부 정보 업데이트
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# UI에서 계정 세부 정보 업데이트

경우에 따라 기존 소스 계정의 세부 사항을 업데이트해야 할 수도 있습니다. [!UICONTROL 소스] 작업 영역에서는 이름, 설명 및 자격 증명을 포함하여 기존 일괄 처리 또는 스트리밍 연결의 세부 정보를 추가, 편집 및 삭제할 수 있는 기능을 제공합니다.

이 자습서에서는 [!UICONTROL Sources] 작업 영역에서 기존 계정의 세부 정보 및 자격 증명을 업데이트하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [소스](../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
- [샌드박스](../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## 계정 업데이트

[Experience Platform UI](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. 기존 계정을 보려면 상단 헤더에서 **[!UICONTROL 계정]**&#x200B;을 선택하십시오.

![카탈로그](../../images/tutorials/update/catalog.png)

**[!UICONTROL 계정]** 페이지가 나타납니다. 이 페이지에는 소스, 사용자 이름, 데이터 흐름 수 및 생성 날짜에 대한 정보를 포함하여 볼 수 있는 계정 목록이 있습니다.

왼쪽 상단의 필터 아이콘 ![filter](../../images/tutorials/update/filter.png)을(를) 선택하여 정렬 패널을 시작합니다.

![accounts-list](../../images/tutorials/update/accounts-list.png)

정렬 패널은 모든 소스의 목록을 제공합니다. 목록에서 두 개 이상의 소스를 선택하여 다른 소스와 연관된 필터링된 계정 선택에 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 계정 목록을 확인합니다. 업데이트할 계정을 식별했으면 계정 이름 옆의 생략 부호(`...`)를 선택합니다.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

드롭다운 메뉴가 나타나며 **[!UICONTROL 데이터 추가]**, **[!UICONTROL 세부 정보 편집]** 및 **[!UICONTROL 삭제]**&#x200B;에 대한 옵션을 제공합니다. 메뉴에서 **[!UICONTROL 세부 정보 편집]**&#x200B;을 선택하여 계정을 업데이트합니다.

![업데이트](../../images/tutorials/update/update.png)

**[!UICONTROL 계정 세부 정보 편집]** 대화 상자를 통해 계정의 이름, 설명 및 인증 자격 증명을 업데이트할 수 있습니다. 원하는 정보를 업데이트했으면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![계정 세부 정보 편집](../../images/tutorials/update/edit-account-details.png)

잠시 후 화면 하단에 성공적으로 업데이트되었는지 확인하는 확인 상자가 나타납니다.

![update-confirmed](../../images/tutorials/update/update-confirmed.png)

## 다음 단계

이 자습서에 따라 [!UICONTROL 소스] 작업 영역을 사용하여 기존 소스 계정의 정보를 업데이트했습니다.

[!DNL Flow Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [흐름 서비스 API를 사용하여 연결 정보 업데이트](../../tutorials/api/update.md)에 대한 자습서를 참조하십시오.
