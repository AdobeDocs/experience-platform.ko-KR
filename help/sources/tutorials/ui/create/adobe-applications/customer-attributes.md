---
keywords: Experience Platform;home;popular topics;customer attributes
solution: Experience Platform
title: UI에서 고객 속성 소스 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform에 수집하기 위해 UI에서 소스 커넥터를 만드는 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 8%

---


# UI에서 고객 속성 소스 커넥터 만들기

이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform에 수집하기 위해 UI에서 소스 커넥터를 만드는 단계를 제공합니다. 고객 속성에 대한 자세한 내용은 [개요 문서를 참조하십시오](https://docs.adobe.com/content/help/ko-KR/core-services/interface/customer-attributes/attributes.html).

## 소스 연결 만들기

소스 작업 영역에 액세스하려면 [Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택합니다. [ **[!UICONTROL 카탈로그]** ] 화면에는 인바운드 연결을 만들 수 있는 사용 가능한 소스가 표시되며 각 소스에는 연관된 기존 연결 수가 표시됩니다. 고객 속성에 대한 옵션 **[!UICONTROL 을]** 선택한 다음 데이터 **[!UICONTROL 추가를 선택합니다]**. 연결이 설정될 때까지 잠시 기다려 주십시오. 연결이 성공적으로 이루어지면 리디렉션됩니다.

>[!NOTE]
>
>고객 속성 프로필 데이터에 대한 소스 커넥터를 이미 설정한 경우 소스와 연결하는 옵션이 비활성화됩니다.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

[ **소스 활동** ] 화면에는 고객 속성 프로필 데이터에 대해 이전에 설정한 모든 연결이 나열되며, 데이터 선택을 클릭하여 새 연결을 만들 수 **있습니다**.

>[!NOTE]
>
>다른 데이터를 가져오기 위해 소스에 대한 여러 인바운드 연결을 만들 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

사용 가능한 고객 속성 프로필 데이터 세트 목록에서 가져올 데이터 세트를 선택하고 [!DNL Platform] 다음을 **클릭합니다**.

>[!NOTE]
>
>고객 속성 소스 연결당 하나의 데이터 세트만 선택할 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

새 인바운드 연결을 생성하기 전에 **검토할 수 있는 검토** 단계가 나타납니다. 연결 세부 사항은 다음을 포함하여 범주별로 그룹화됩니다.

* **소스 세부 정보**:소스 연결 유형과 선택한 소스 데이터를 표시합니다.
* **Target 세부 정보**:다른 소스 커넥터를 만들 때 이 컨테이너는 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집 중인 데이터 세트를 표시합니다. 고객 속성 프로필 데이터는 자동으로 매핑되고 실시간 고객 프로파일에 수집됩니다.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 생성됩니다. 초기 수렴이 완료되면, 고객 속성 프로필 데이터를 다운스트림 [!DNL Platform] 서비스(예: [!DNL Real-time Customer Profile] 및 [!DNL Segmentation Service])에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
