---
keywords: Experience Platform;home;popular topics;update accounts
description: 경우에 따라 기존 소스 계정의 세부 사항을 업데이트해야 할 수 있습니다. 소스 작업 공간에서는 이름, 설명, 자격 증명 등 기존 배치 또는 스트리밍 연결의 세부 사항을 추가, 편집 및 삭제할 수 있습니다.
solution: Experience Platform
title: UI에서 계정 세부 사항 업데이트
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 9b48bc1426e6259ea0b2cf9b420b55b92712f7c2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# UI에서 계정 세부 사항 업데이트

경우에 따라 기존 소스 계정의 세부 사항을 업데이트해야 할 수 있습니다. 소스 [!UICONTROL 작업] 공간에서는 이름, 설명, 자격 증명 등 기존 배치 또는 스트리밍 연결의 세부 사항을 추가, 편집 및 삭제할 수 있습니다.

이 자습서에서는 소스 작업 공간에서 기존 계정의 세부 사항 및 자격 증명을 업데이트하는 [!UICONTROL 단계를] 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [소스](../../home.md):DNL Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
- [샌드박스](../../../sandboxes/home.md):DNL Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 계정 업데이트

Experience Platform [UI에](https://platform.adobe.com) 로그인한 다음 왼쪽 탐색 **[!UICONTROL 에서 소스]** 를 선택하여 [!UICONTROL 소스 작업 영역에] 액세스합니다. 상단 헤더에서 **[!UICONTROL 계정을]** 선택하여 기존 계정을 봅니다.

![카탈로그](../../images/tutorials/update/catalog.png)

계정 **[!UICONTROL 페이지가]** 나타납니다. 이 페이지에는 소스, 사용자 이름, 데이터 흐름 수 및 작성 날짜에 대한 정보를 비롯하여 볼 수 있는 계정 목록이 있습니다.

왼쪽 상단에 있는 필터 아이콘 ![필터를](../../images/tutorials/update/filter.png) 선택하여 정렬 패널을 실행합니다.

![계정 목록](../../images/tutorials/update/accounts-list.png)

정렬 패널은 모든 소스 목록을 제공합니다. 목록에서 둘 이상의 소스를 선택하여 다른 소스와 연관된 필터링된 계정 선택을 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 계정 목록을 확인합니다. 업데이트할 계정을 식별했으면 계정 이름 옆에 있는 줄임표(`...`)를 선택합니다.

![계정 정렬](../../images/tutorials/update/accounts-sort.png)

데이터 추가, 세부 사항 **[!UICONTROL 편집]**&#x200B;및 삭제 옵션을 제공하는 드롭다운 메뉴가 **[!UICONTROL 나타납니다]******. 메뉴에서 **[!UICONTROL 세부]** 사항 편집을 선택하여 계정을 업데이트합니다.

![업데이트](../../images/tutorials/update/update.png)

계정 **[!UICONTROL 세부 사항]** 편집 대화 상자를 사용하면 계정의 이름, 설명 및 인증 자격 증명을 업데이트할 수 있습니다. 원하는 정보를 업데이트했으면 저장을 **[!UICONTROL 선택합니다]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

잠시 후 화면 하단에 녹색 확인 상자가 표시되어 성공적인 업데이트를 확인합니다.

![업데이트 확인](../../images/tutorials/update/update-confirmed.png)

## 다음 단계

이 튜토리얼을 따라 [!UICONTROL 소스] 작업 영역을 사용하여 계정 정보를 업데이트했습니다.

API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 Flow Service API를 사용하여 연결 정보를 [!DNL Flow Service] 업데이트하는 방법에 대한 자습서를 참조하십시오 [](../../tutorials/api/update.md).