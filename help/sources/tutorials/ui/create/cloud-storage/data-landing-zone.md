---
keywords: Experience Platform;홈;인기 항목;데이터 랜딩 영역;데이터 랜딩 영역
title: UI를 사용하여 플랫폼에 데이터 랜딩 영역 연결
description: 플랫폼 사용자 인터페이스를 사용하여 데이터 랜딩 영역 소스 커넥터를 만드는 방법을 알아봅니다.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: fb16ea940ef394a15dd24fe703239b4487fafb18
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Connect [!DNL Data Landing Zone] UI를 사용하여 플랫폼 구현

[!DNL Data Landing Zone] 는 Adobe Experience Platform으로 파일을 가져올 수 있는 안전한 클라우드 기반 파일 저장 기능입니다. 데이터는 [!DNL Data Landing Zone] 7일 후

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Data Landing Zone] 플랫폼 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 파일 가져오기 [!DNL Data Landing Zone] 플랫폼

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 클라우드 스토리지] 카테고리, 선택 [!DNL Data Landing Zone] 그런 다음 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/dlz/catalog.png)

다음 [!UICONTROL 데이터 추가] Platform으로 가져올 데이터를 선택하고 미리 볼 수 있는 인터페이스를 제공하는 단계가 나타납니다.

* 인터페이스 왼쪽 부분은 폴더 브라우저로, 이 브라우저에서 Platform으로 가져올 수 있는 컨테이너의 파일 목록을 제공합니다.
* 인터페이스의 오른쪽 부분에서 호환되는 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

Platform으로 가져올 파일을 선택하고 올바른 인터페이스가 미리 보기 화면으로 업데이트될 때까지 잠시 기다립니다.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform은 선택한 파일의 속성 정보를 자동으로 검색합니다. 여기에는 파일의 데이터 형식에 대한 정보, 지정된 열 구분 기호 및 압축 유형이 포함됩니다.

미리 보기 인터페이스를 사용하면 파일의 내용 및 구조를 검사할 수 있습니다. 기본적으로 미리 보기 인터페이스에서는 선택한 폴더에 첫 번째 파일이 표시됩니다.

다른 파일을 미리 보려면 검사할 파일 이름 옆에 있는 미리 보기 아이콘을 선택합니다.

완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![파일 감지](../../../../images/tutorials/create/dlz/file-detection.png)

클라우드 스토리지 소스용 데이터 흐름을 만드는 방법에 대한 단계별 세부 안내서는 [플랫폼으로 데이터를 가져오기 위한 클라우드 스토리지 데이터 흐름 만들기](../../dataflow/batch/cloud-storage.md).

## 검색 및 새로 고침 [!DNL Data Landing Zone] 자격 증명

[!DNL Data Landing Zone] 는 Adobe Experience Platform 소스 라이센스와 함께 제공되는 기본 소스입니다. [!DNL Data Landing Zone] 는 SAS URI 및 SAS 토큰 기반 인증을 사용합니다. 에서 인증 자격 증명을 검색하고 새로 고칠 수 있습니다 [!UICONTROL 소스 카탈로그] 페이지.

에서 [!UICONTROL 소스 카탈로그]아래에 있는 [!UICONTROL 클라우드 스토리지] 카테고리에서 줄임표( )를 선택합니다&#x200B;**...**) 내의 **[!UICONTROL 데이터 랜딩 영역]** 카드. 표시되는 드롭다운 메뉴에서 을(를) 선택합니다 **[!UICONTROL 자격 증명 보기]**.

![옵션](../../../../images/tutorials/create/dlz/options.png)

컨테이너 이름, SAS 토큰, 저장소 계정 이름 및 SAS URI를 표시하는 팝업 창이 나타납니다.

선택 **[!UICONTROL 자격 증명 새로 고침]** 업데이트된 자격 증명이 처리되려면 몇 초 동안 기다립니다.

>[!TIP]
>
>사용자 [!DNL Data Landing Zone] 자격 증명은 90일 후 자동으로 만료되도록 설정되며, 새 자격 증명을 사용하여 다음에 다시 연결해야 합니다 [!DNL Data Landing Zone] 만료 후. 플랫폼의 데이터 흐름은 만료 자격 증명으로 영향을 받지 않으며 새 자격 증명으로 새 데이터 흐름과 기존 데이터 흐름으로 계속 작업할 수 있습니다.

![자격 증명 보기](../../../../images/tutorials/create/dlz/credentials.png)

## 다음 단계

이 자습서에 따르면 [!DNL Data Landing Zone] 자격 증명을 검색하고 새로 고치는 방법을 알아봅니다. 이제 다음 자습서를 [데이터 흐름 만들기 를 사용하여 클라우드 저장소에서 플랫폼으로 데이터 가져오기](../../dataflow/batch/cloud-storage.md).
