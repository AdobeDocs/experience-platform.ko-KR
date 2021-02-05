---
keywords: Experience Platform;홈;인기 항목;사용자 특성;InDesign;home;popular topics;customer attributes
solution: Experience Platform
title: UI에서 고객 속성 소스 연결 만들기
topic: overview
type: Tutorial
description: 고객 속성 프로필 데이터를 Adobe Experience Platform에 수집하기 위해 UI에서 소스 연결을 만드는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 5%

---


# UI에서 고객 속성 소스 연결 만들기

이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform에 수집하기 위해 UI에서 소스 연결을 만드는 단계를 제공합니다. 고객 속성에 대한 자세한 내용은 [개요 문서](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html)를 참조하십시오.

## 소스 연결 만들기

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 소스 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에는 인바운드 연결을 만들 수 있는 사용 가능한 소스가 표시되고 각 소스에는 연관된 기존 연결 수가 표시됩니다. **[!UICONTROL 고객 속성]**&#x200B;에 대한 옵션을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다. 연결이 성공적으로 이루어지면 연결이 리디렉션될 것입니다.

>[!NOTE]
>
>고객 속성 프로필 데이터에 대한 소스 커넥터를 이미 설정한 경우 소스와 연결하는 옵션이 비활성화됩니다.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

**소스 활동** 화면에는 고객 속성 프로필 데이터에 대해 이전에 설정한 모든 연결이 나열됩니다. **데이터 선택**&#x200B;을 클릭하여 새 연결을 만들 수 있습니다.

>[!NOTE]
>
>다른 데이터를 가져오기 위해 소스에 대한 여러 인바운드 연결을 만들 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

사용 가능한 고객 속성 프로필 데이터 집합 목록에서 [!DNL Platform]에 가져올 항목을 선택하고 **다음**&#x200B;을 클릭합니다.

>[!NOTE]
>
>고객 속성 소스 연결당 하나의 데이터 세트만 선택할 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

새로 인바운드 연결을 만들기 전에 검토할 수 있도록 **검토** 단계가 나타납니다. 연결 세부 사항은 다음을 포함한 카테고리별로 그룹화됩니다.

* **소스 세부 정보**:소스 연결 유형과 선택한 소스 데이터를 표시합니다.
* **Target 세부 정보**:다른 소스 커넥터를 만들 때 이 컨테이너는 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집 중인 데이터 세트를 표시합니다. 고객 속성 프로필 데이터는 자동으로 매핑되고 실시간 고객 프로파일에 수집됩니다.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 생성됩니다. 초기 인제스트가 완료되면 고객 속성 프로필 데이터를 [!DNL Real-time Customer Profile] 및 [!DNL Segmentation Service] 같은 다운스트림 [!DNL Platform] 서비스에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
