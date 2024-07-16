---
title: UI를 사용하여 데이터 랜딩 영역을 플랫폼에 연결
description: Platform 사용자 인터페이스를 사용하여 데이터 랜딩 영역 소스 커넥터를 만드는 방법을 알아봅니다.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# UI를 사용하여 [!DNL Data Landing Zone]을(를) 플랫폼에 연결

>[!IMPORTANT]
>
>이 페이지는 Experience Platform의 [!DNL Data Landing Zone] *source* 커넥터에 한정됩니다. [!DNL Data Landing Zone] *대상* 커넥터에 연결하는 방법에 대한 자세한 내용은 [[!DNL Data Landing Zone] 대상 설명서 페이지](/help/destinations/catalog/cloud-storage/data-landing-zone.md)를 참조하세요.

[!DNL Data Landing Zone]은(는) Adobe Experience Platform으로 파일을 가져올 수 있는 안전한 클라우드 기반 파일 저장소 기능입니다. 데이터는 7일 후 [!DNL Data Landing Zone]에서 자동으로 삭제됩니다.

이 자습서에서는 Platform 사용자 인터페이스를 사용하여 [!DNL Data Landing Zone] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## [!DNL Data Landing Zone]에서 플랫폼으로 파일 가져오기

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 저장소] 범주에서 [!DNL Data Landing Zone]을(를) 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![데이터 랜딩 영역이 있는 원본 카탈로그를 선택했습니다.](../../../../images/tutorials/create/dlz/catalog.png)

플랫폼으로 가져올 데이터를 선택하고 미리 볼 수 있는 인터페이스를 제공하는 [!UICONTROL 데이터 추가] 단계가 나타납니다.

* 인터페이스의 왼쪽 부분은 폴더 브라우저이며, 컨테이너에서 플랫폼으로 가져올 수 있는 파일 목록을 제공합니다.
* 인터페이스의 오른쪽 부분에서 호환 가능한 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

Experience Platform에 가져올 파일을 선택하고 몇 분 동안 올바른 인터페이스가 미리보기 화면으로 업데이트될 수 있도록 하십시오.

![원본 작업 영역의 데이터 인터페이스를 추가합니다.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform은 파일의 데이터 형식, 지정된 열 구분 기호 및 압축 유형에 대한 정보를 포함하여 선택한 파일의 속성 정보를 자동으로 검색합니다.

미리보기 인터페이스를 사용하여 파일의 내용과 구조를 검사할 수 있습니다. 기본적으로 미리보기 인터페이스는 선택한 폴더의 첫 번째 파일을 표시합니다.

다른 파일을 미리 보려면 검사할 파일 이름 옆에 있는 미리 보기 아이콘을 선택합니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![원본 작업 영역의 데이터 미리 보기 페이지입니다.](../../../../images/tutorials/create/dlz/file-detection.png)

클라우드 스토리지 소스에 대한 데이터 흐름을 만드는 방법에 대한 자세한 단계별 안내서는 [데이터를 플랫폼으로 가져오기 위한 클라우드 스토리지 데이터 흐름 만들기](../../dataflow/batch/cloud-storage.md)에 대한 자습서를 참조하십시오.

## [!DNL Data Landing Zone] 자격 증명 검색

[!DNL Data Landing Zone]은(는) Adobe Experience Platform 소스 라이선스와 함께 제공되는 소스입니다. [!DNL Data Landing Zone]이(가) SAS URI 및 SAS 토큰 기반 인증을 사용합니다. [!UICONTROL 소스 카탈로그] 페이지에서 인증 자격 증명을 검색할 수 있습니다.

자격 증명을 검색하려면 **[!UICONTROL 데이터 랜딩 영역]** 카드를 선택한 다음 나타나는 오른쪽 레일에서 자격 증명을 복사하십시오.

![데이터 랜딩 영역에 대한 보기 옵션 목록입니다.](../../../../images/tutorials/create/dlz/view-credentials.png)

컨테이너 이름, SAS 토큰, 저장소 계정 이름, SAS URI 및 만료 날짜를 표시하는 팝오버가 나타납니다.

## [!DNL Data Landing Zone] 자격 증명 새로 고침

[!DNL Data Landing Zone] 자격 증명은 90일 후에 자동 만료되도록 설정되었으며 만료 후 [!DNL Data Landing Zone]에 다시 연결하려면 새 자격 증명을 사용해야 합니다. Experience Platform의 데이터 흐름은 만료 자격 증명의 영향을 받지 않으며 새 자격 증명을 사용하여 새 데이터 흐름 및 기존 데이터 흐름을 계속 사용할 수 있습니다.

[!DNL Data Landing Zone] 자격 증명을 새로 고치는 방법에는 두 가지가 있습니다.

>[!BEGINTABS]

>[!TAB 원본 카드 사용]

소스 카탈로그 페이지에서 자격 증명을 새로 고치려면 [!DNL Data Landing Zone] 카드에서 줄임표(**`...`**)를 선택한 다음 **[!UICONTROL 자격 증명 새로 고침]**&#x200B;을 선택합니다.

![원본 카드를 사용하여 자격 증명을 새로 고칩니다.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

계속하기 전에 확인을 묻는 팝업 창이 나타납니다. 준비가 되면 **[!UICONTROL 자격 증명 새로 고침]**&#x200B;을 선택하세요.

![자격 증명 새로 고침 확인 창입니다.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB 올바른 레일 사용]

올바른 레일을 사용하여 자격 증명을 새로 고치려면 **[!UICONTROL 데이터 랜딩 영역]** 원본 카드를 선택한 다음 **[!UICONTROL 추가 작업]**&#x200B;을 선택합니다. **[!UICONTROL 자격 증명 새로 고침]**&#x200B;을 선택한 다음 표시되는 팝업 창을 사용하여 확인합니다.

![올바른 레일을 사용하여 자격 증명을 새로 고칩니다.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## 다음 단계

이 자습서를 통해 [!DNL Data Landing Zone] 컨테이너에 액세스하고 자격 증명을 검색하고 새로 고치는 방법을 배웠습니다. 이제 [데이터 흐름을 만들어 클라우드 저장소에서 플랫폼으로 데이터를 가져오는 방법](../../dataflow/batch/cloud-storage.md)에 대한 다음 자습서로 진행할 수 있습니다.
