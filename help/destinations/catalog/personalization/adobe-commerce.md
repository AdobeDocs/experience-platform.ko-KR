---
title: (베타) Adobe Commerce 대상 커넥터
description: Real-Time CDP 내에서 구축되고 관리되는 고객 세그먼트에 맞게 사용자 지정된 고도로 적절한 사이트 컨텐츠와 프로모션을 제공하여 Adobe Commerce 및 Real-Time CDP 가맹점이 쇼핑 경험을 개인화할 수 있는 방법을 알아봅니다.
source-git-commit: 566f26ec0f13bfaceb0ee59f3e4c72e767bc8cc9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# (베타) Adobe Commerce 연결 {#adobe-commerce}

## 개요 {#overview}

>[!IMPORTANT]
> 
>다음 **[!UICONTROL Adobe Commerce]** 커넥터는 베타에 있으며 일부 고객만 사용할 수 있습니다.

다음 [!DNL Adobe Commerce] 대상 커넥터를 사용하면 하나 이상의 Real-Time CDP 세그먼트를 선택하여 원하는 위치에 활성화할 수 있습니다 [!DNL Adobe Commerce] 고객을 위한 동적 개인화된 경험을 제공하기 위한 계정입니다. 내 [!DNL Adobe Commerce]그런 다음 이러한 Real-Time CDP 세그먼트를 선택하여 장바구니에서 &#39;buy 2 get 1 free&#39; 등의 고유한 오퍼를 개인화할 수 있습니다. Adobe Real-Time CDP 세그먼트에 맞게 사용자 지정된 프로모션 오퍼를 통해 대표 배너를 표시하고 제품 가격을 수정할 수도 있습니다.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## 전제 조건 {#prerequisites}

이 확장은 Real-Time CDP Prime 또는 Ultimate 및 Adobe Commerce을 구입한 일부 베타 고객의 대상 카탈로그에서 사용할 수 있습니다.

Beta 고객은 다음 항목에 액세스할 수 있어야 합니다.

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud 버전 2.4.3 이상](https://business.adobe.com/products/magento/magento-commerce.html)

Experience Platform에서 다음을 만듭니다.

- [스키마](../../../xdm/schema/composition.md). 만드는 스키마는 Adobe Commerce에서 수집할 데이터를 나타냅니다. [추가 정보](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) 상거래 관련 필드 그룹을 포함하는 스키마를 만드는 방법에 대한 정보.
- [데이터 세트](../../../catalog/datasets/user-guide.md#create). 데이터 집합은 데이터 수집을 위한 저장 및 관리 구성입니다. 위에서 만든 스키마에서 이 데이터 세트를 만들어야 합니다.
- [데이터 스트림](../../../edge/datastreams/overview.md#create). Adobe Experience Platform에서 다른 Adobe DX 제품으로 데이터를 전송할 수 있는 ID입니다. 이 ID는 특정 Adobe Commerce 인스턴스 내의 특정 웹 사이트에 연결되어 있어야 합니다. 이 데이터 스트림을 만들 때 위에서 만든 XDM 스키마를 지정합니다.

사전 요구 사항을 완료하면 [!DNL Commerce] 대상.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

에 연결하려면 [!DNL Adobe Commerce] 대상:

1. 에서 [플랫폼 인터페이스](https://experience.adobe.com/platform/), 이동 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**.
1. 선택 **[!UICONTROL 개인화]**.
1. 강조 표시할 Adobe Commerce 대상을 선택한 다음, 을 선택합니다 **[!UICONTROL 설정]**.
1. 에 설명된 단계를 수행합니다. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

- **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
- **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
- **[!UICONTROL 통합 별칭]**: 이 값은 JSON 개체 이름으로 Experience Platform Web SDK에 전송됩니다.
- **[!UICONTROL 데이터 스트림 ID]**: 이에 따라 페이지에 대한 응답에 세그먼트를 포함할 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에는 대상 구성이 활성화된 데이터 세트만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](../../../edge/datastreams/overview.md) 자세한 내용

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 [!DNL Commerce] 대상 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [프로필 요청 대상에 프로필 및 세그먼트 활성화](../../ui/activate-profile-request-destinations.md) 대상 세그먼트를 [!DNL Commerce] 대상.

## 의 다음 단계 [!DNL Adobe Commerce]

이제 다음을 구성했으므로 [!DNL Commerce] Experience Platform 내에서 대상을 구성해야 합니다 [!DNL Commerce Admin] 만든 Real-Time CDP 세그먼트를 가져오기 위해 자세한 내용은 [[!DNL Commerce] 설명서](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/customer-segment-rtcdp.html) 추가 정보

## 데이터 내보내기의 유효성 검사 {#exported-data}

Real-Time CDP 세그먼트를 [!DNL Adobe Commerce] 계정, [!DNL Admin] 장바구니 가격 규칙을 만들 때:

![Adobe Commerce 관리](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](/help/data-governance/home.md).
