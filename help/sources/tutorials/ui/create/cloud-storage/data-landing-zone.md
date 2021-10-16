---
keywords: Experience Platform;홈;인기 항목;데이터 랜딩 영역;데이터 랜딩 영역
solution: Experience Platform
title: UI를 사용하여 플랫폼에 데이터 랜딩 영역 연결
topic-legacy: overview
type: Tutorial
description: 플랫폼 사용자 인터페이스를 사용하여 데이터 랜딩 영역 소스 커넥터를 만드는 방법을 알아봅니다.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# UI를 사용하여 [!DNL Data Landing Zone] 을 플랫폼에 연결

[!DNL Data Landing Zone] 는 Adobe Experience Platform에 프로비저닝된 임시 파일 저장소를 위한 클라우드 기반 데이터 저장소 기능입니다. 데이터는 7일 후 [!DNL Data Landing Zone]에서 자동으로 삭제됩니다.

이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 [!DNL Data Landing Zone] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 파일을 [!DNL Data Landing Zone]에서 플랫폼으로 가져오기

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 공간에 액세스합니다. [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 카테고리에서 [!DNL Data Landing Zone]를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/dlz/catalog.png)

Platform으로 가져올 데이터를 선택하고 미리 볼 수 있는 인터페이스를 제공하는 [!UICONTROL 데이터 추가] 단계가 나타납니다.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

클라우드 저장소 소스에 대한 데이터 흐름을 만드는 방법에 대한 단계별 세부 안내서는 [클라우드 저장소 데이터 흐름 만들기 의 자습서를 참조하여 플랫폼](../../dataflow/batch/cloud-storage.md)에 데이터를 가져오십시오.

## [!DNL Data Landing Zone] 자격 증명 검색 및 새로 고침

[!DNL Data Landing Zone] 는 Adobe Experience Platform 소스 라이센스와 함께 제공되는 기본 소스입니다. [!DNL Data Landing Zone] 는 SAS URI 및 SAS 토큰 기반 인증을 사용합니다. [!UICONTROL 소스 카탈로그] 페이지에서 인증 자격 증명을 검색하고 새로 고칠 수 있습니다.

[!UICONTROL 소스 카탈로그]에 있는 [!UICONTROL 클라우드 저장소] 카테고리에서 줄임표(**...**[!UICONTROL )의 데이터 랜딩 영역&#x200B;]**카드의**. 표시되는 드롭다운 메뉴에서 **[!UICONTROL 자격 증명 보기]**&#x200B;를 선택합니다.

![옵션](../../../../images/tutorials/create/dlz/options.png)

컨테이너 이름, SAS 토큰, 저장소 계정 이름 및 SAS URI를 표시하는 팝업 창이 나타납니다.

**[!UICONTROL 자격 증명 새로 고침]**&#x200B;을 선택하고 업데이트된 자격 증명을 처리할 때까지 몇 초 동안 기다립니다.

![자격 증명 보기](../../../../images/tutorials/create/dlz/credentials.png)

## 다음 단계

이 자습서를 따라 [!DNL Data Landing Zone] 컨테이너에 액세스하여 자격 증명을 검색하고 새로 고치는 방법을 학습했습니다. 이제 [데이터 흐름 만들기에서 다음 자습서를 진행하여 클라우드 저장소에서 플랫폼](../../dataflow/batch/cloud-storage.md)으로 데이터를 가져올 수 있습니다.
