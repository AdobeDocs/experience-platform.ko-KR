---
keywords: Experience Platform;홈;인기 항목;계정 업데이트
description: 경우에 따라 기존 소스 계정의 세부 사항을 업데이트해야 할 수 있습니다. 소스 작업 영역은 이름, 설명 및 자격 증명을 포함하여 기존 배치 또는 스트리밍 연결의 세부 사항을 추가, 편집 및 삭제할 수 있는 기능을 제공합니다.
solution: Experience Platform
title: UI에서 소스 연결 계정 세부 사항 업데이트
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# UI에서 계정 세부 사항 업데이트

경우에 따라 기존 소스 계정의 세부 사항을 업데이트해야 할 수 있습니다. 다음 [!UICONTROL 소스] workspace에서는 이름, 설명 및 자격 증명을 포함하여 기존 배치 또는 스트리밍 연결의 세부 사항을 추가, 편집 및 삭제할 수 있는 기능을 제공합니다.

이 자습서에서는 [!UICONTROL 소스] 작업 공간.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
- [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 계정 업데이트

에 로그인합니다. [Experience Platform UI](https://platform.adobe.com) 그런 다음 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 선택 **[!UICONTROL 계정]** 기존 계정을 보려면 상단 헤더에서 클릭하십시오.

![카탈로그](../../images/tutorials/update/catalog.png)

다음 **[!UICONTROL 계정]** 페이지가 나타납니다. 이 페이지에는 소스, 사용자 이름, 데이터 흐름 수 및 작성 날짜에 대한 정보를 포함하여 볼 수 있는 계정 목록이 있습니다.

필터 아이콘을 선택합니다 ![필터](../../images/tutorials/update/filter.png) 왼쪽 상단에서 정렬 패널을 시작합니다.

![계정 목록](../../images/tutorials/update/accounts-list.png)

정렬 패널에서는 모든 소스 목록을 제공합니다. 목록에서 둘 이상의 소스를 선택하여 다른 소스와 연결된 필터링된 계정 선택에 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 계정 목록을 확인합니다. 업데이트할 계정을 식별했으면 줄임표(`...`) 내의 아무 곳에나 삽입할 수 있습니다.

![계정 정렬](../../images/tutorials/update/accounts-sort.png)

옵션을 제공하는 드롭다운 메뉴가 나타납니다 **[!UICONTROL 데이터 추가]**, **[!UICONTROL 세부 사항 편집]**, 및 **[!UICONTROL 삭제]**. 선택 **[!UICONTROL 세부 사항 편집]** 메뉴에서 계정을 업데이트합니다.

![업데이트](../../images/tutorials/update/update.png)

다음 **[!UICONTROL 계정 세부 사항 편집]** 대화 상자에서는 계정의 이름, 설명 및 인증 자격 증명을 업데이트할 수 있습니다. 원하는 정보를 업데이트했으면 을 선택합니다 **[!UICONTROL 저장]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

잠시 후 화면 하단에 확인 상자가 표시되어 성공적인 업데이트를 확인합니다.

![업데이트 확인](../../images/tutorials/update/update-confirmed.png)

## 다음 단계

이 자습서를 따라 다음을 성공적으로 사용했습니다. [!UICONTROL 소스] 작업 영역에서 기존 소스 계정의 정보를 업데이트합니다.

를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 절차 [!DNL Flow Service] API입니다. 다음 페이지에서 자습서를 참조하십시오. [흐름 서비스 API를 사용하여 연결 정보 업데이트](../../tutorials/api/update.md).
