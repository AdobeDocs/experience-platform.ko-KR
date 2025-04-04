---
title: Adobe Commerce 대상 커넥터
description: Adobe Commerce 및 Real-Time CDP 판매자가 Real-Time CDP 내에서 구축 및 관리되는 고객 대상에 맞게 맞춤화된, 관련성이 높은 사이트 콘텐츠 및 프로모션을 제공하여 쇼핑 경험을 개인화하는 방법을 알아봅니다.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 3%

---

# Adobe Commerce 연결 {#adobe-commerce}

## 개요 {#overview}

[!DNL Adobe Commerce] 대상 커넥터를 사용하면 하나 이상의 Real-Time CDP 대상을 선택하여 [!DNL Adobe Commerce] 계정에 활성화하여 쇼핑객에게 동적 개인화된 환경을 제공할 수 있습니다. 그런 다음 [!DNL Adobe Commerce] 내에서 해당 Real-Time CDP 대상자를 선택하여 &#39;2개 구매, 1개 무료&#39; 등의 장바구니에서 고유한 오퍼를 개인화할 수 있습니다. 또한 Adobe Real-Time CDP 대상에 맞게 맞춤화된 홍보용 오퍼를 통해 영웅 배너를 표시하고 제품 가격을 수정할 수 있습니다.

## 전제 조건 {#prerequisites}

이 커넥터는 Real-Time CDP Prime 또는 Ultimate 및 Adobe Commerce을 구입한 고객의 대상 카탈로그에서 사용할 수 있습니다.

이 대상 연결을 사용하려면 다음에 대한 액세스 권한이 있는지 확인하십시오.

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). 개발자 콘솔에 액세스하여 Adobe Commerce에서 확장의 [구성을 완료](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension)하는 데 필요한 서비스 계정 및 자격 증명 정보를 볼 수 있습니다.
- [Adobe Commerce Cloud 버전 2.4.4 이상](https://business.adobe.com/products/magento/magento-commerce.html)

Experience Platform에서 다음을 생성합니다.

- [스키마](../../../xdm/schema/composition.md). 생성하는 스키마는 Adobe Commerce에서 수집하려는 데이터를 나타냅니다. Commerce 관련 필드 그룹을 포함하는 스키마를 만드는 방법에 대해 [자세히 알아보기](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
- [데이터 집합](../../../catalog/datasets/user-guide.md#create). 데이터 집합은 데이터 수집을 위한 스토리지 및 관리 구성입니다. 위에서 만든 스키마에서 이 데이터 세트를 만듭니다.
- [데이터스트림](../../../datastreams/overview.md#create). Adobe Experience Platform에서 다른 Adobe DX 제품으로 데이터가 흐를 수 있는 ID입니다. 이 ID는 특정 Adobe Commerce 인스턴스 내의 특정 웹 사이트에 연결되어야 합니다. 이 데이터 스트림을 만들 때 위에서 만든 XDM 스키마를 지정합니다.

필수 구성 요소를 완료한 후 [!DNL Commerce] 대상에 연결합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

[!DNL Adobe Commerce] 대상에 연결하려면:

1. [Experience Platform 인터페이스](https://experience.adobe.com/platform/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**(으)로 이동합니다.
1. **[!UICONTROL Personalization]**&#x200B;을(를) 선택합니다.
1. Adobe Commerce 대상을 선택하여 강조 표시한 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.
1. [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

- **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
- **[!UICONTROL 설명]**: 대상에 대한 설명을 입력하십시오. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
- **[!UICONTROL 통합 별칭]**: 이 값은 JSON 개체 이름으로 Experience Platform Web SDK에 전송됩니다.
- **[!UICONTROL 데이터 스트림 ID]**: 페이지 응답에 포함된 대상이 포함된 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에 대상 구성이 활성화된 데이터스트림만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](../../../datastreams/overview.md)을 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## [!DNL Commerce] 대상에 대상 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

[!DNL Commerce] 대상에 대한 대상자 활성화에 대한 지침은 [프로필 및 대상자 활성화](../../ui/activate-edge-personalization-destinations.md)를 참조하세요.

## [!DNL Adobe Commerce]의 다음 단계

이제 Experience Platform 내에서 [!DNL Commerce] 대상을 구성했으므로 [!DNL Commerce]에 [!DNL Audience Activation] 확장을 설치하고 만든 Real-Time CDP 대상을 가져오도록 [!DNL Commerce Admin]을(를) 구성해야 합니다. 자세한 내용은 [[!DNL Commerce] 설명서](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html)를 참조하세요.

## Commerce에서 대상자 활성화 확인 {#exported-data}

[!DNL Adobe Commerce] 계정에 Real-Time CDP 대상을 활성화하면 _관리자_ 사이드바로 이동한 다음 **[!UICONTROL 고객]** > **[!UICONTROL Real-Time CDP 대상]**(으)로 이동하면 사용할 수 있는 대상을 볼 수 있습니다.

![Real-Time CDP 대상 대시보드](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
