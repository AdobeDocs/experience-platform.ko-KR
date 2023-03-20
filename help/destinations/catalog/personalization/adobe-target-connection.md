---
keywords: target 개인화; 대상; experience platform target 대상;adobe target 대상
title: Adobe Target 연결
description: Adobe Target은 웹 사이트, 모바일 앱 등에서 모든 인바운드 고객 상호 작용에 실시간 AI 기반의 개인화 및 실험 기능을 제공하는 애플리케이션입니다.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: f97b667f8d4dc311683b018bb1c1792aae871648
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# Adobe Target 연결 {#adobe-target-connection}

## 대상 변경 로그 {#changelog}

>[!IMPORTANT]
>
>향상된 Adobe Target V2 대상 커넥터의 베타 릴리스를 사용하면 대상 카탈로그에 두 개의 Adobe Target 카드가 표시될 수 있습니다.
>Adobe Target V2 대상 커넥터는 현재 베타 버전이며 일부 고객만 사용할 수 있습니다. V1 Adobe 카드에서 제공하는 기능 외에도 Target V2 커넥터는 [매핑 단계](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 프로필 속성을 Adobe Target에 매핑할 수 있는 활성화 워크플로우에 속성 기반의 동일 페이지 및 다음 페이지 개인화를 활성화합니다.

![나란히 보기에 있는 두 Adobe Target 대상 카드의 이미지입니다.](/help/destinations/assets/catalog/personalization/adobe-target-connection/adobe-target-side-by-side-view.png)

## 개요 {#overview}

Adobe Target은 웹 사이트, 모바일 앱 등에서 모든 인바운드 고객 상호 작용에 실시간 AI 기반의 개인화 및 실험 기능을 제공하는 애플리케이션입니다.

Adobe Target 는 Adobe Experience Platform 대상 카탈로그의 개인화 연결입니다.

## 사전 요구 사항 {#prerequisites}

### 데이터 스트림 ID {#datastream-id}

Adobe Target 연결을 구성할 때 [데이터 스트림 ID 사용](#parameters), 다음을 수행해야 합니다. [Adobe Experience Platform Web SDK](../../../edge/home.md) 구현됨.

데이터 스트림 ID를 사용하지 않고 Adobe Target 연결을 구성해도 Web SDK를 구현할 필요가 없습니다.

>[!IMPORTANT]
>
>만들기 전 [!DNL Adobe Target] 연결, 방법에 대한 안내서를 참조하십시오. [동일한 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](../../ui/configure-personalization-destinations.md). 이 안내서에서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다. 동일한 페이지 및 다음 페이지 개인화를 사용하려면 Adobe Target 연결을 구성할 때 데이터 스트림 ID를 사용해야 합니다.

### Adobe Target의 사전 요구 사항 {#prerequisites-in-adobe-target}

Adobe Target에서 사용자가 다음을 보유하고 있는지 확인합니다.

* 에 액세스 [기본 작업 공간](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* 다음 **승인자** [역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

에 대한 권한 부여에 대한 자세한 내용 [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) 및 대상 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!DNL Profile request]** | 단일 프로필에 대해 Adobe Target 대상에 매핑된 모든 세그먼트를 요청합니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

**홈 페이지 배너 개인화**

홈 대여 및 판매 회사는 Adobe Experience Platform의 고객 세그먼트 자격에 따라 배너를 사용하여 홈 페이지를 개인화하려고 합니다. 회사는 개인화된 경험을 제공해야 하는 대상을 선택하고, Target 오퍼에 대한 타깃팅 기준으로 Adobe Target에 보낼 수 있습니다.

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="데이터 스트림 ID 기본 정보"
>abstract="이 옵션은 세그먼트를 포함할 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에는 Target 구성이 활성화된 데이터 세트만 표시됩니다. 에지 세그멘테이션을 사용하려면 데이터 스트림 ID를 선택해야 합니다. 없음 을 선택하면 에지 세그멘테이션을 사용하는 모든 사용 사례가 비활성화됩니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="데이터 저장소 선택에 대한 자세한 정보"

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

Adobe Experience Platform은 회사의 Adobe Target 인스턴스에 자동으로 연결됩니다. 인증이 필요하지 않습니다.

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **이름**: 이 대상의 기본 이름을 입력합니다.
* **설명**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **데이터 스트림 ID**: 이 설정은 세그먼트가 포함될 데이터 수집 데이터 스트림을 결정합니다. 드롭다운 메뉴에는 Target 및 Adobe Experience Platform 서비스가 활성화된 데이터 세트만 표시됩니다. 자세한 내용은 [데이터 스트림 구성](../../../edge/datastreams/configure.md#aep) Adobe Experience Platform 및 Adobe Target용 데이터 스트림을 구성하는 방법에 대한 자세한 정보.
   * **[!UICONTROL 없음]**: Adobe Target 개인화를 구성해야 하지만 구현할 수 없는 경우 이 옵션을 선택합니다 [웹 SDK Experience Platform](../../../edge/home.md). 이 옵션을 사용하는 경우 Experience Platform에서 Target으로 내보낸 세그먼트는 다음 세션 개인화만 지원하며, 에지 세그먼테이션은 비활성화되어 있습니다. 자세한 내용은 아래 표를 참조하십시오.

| 선택한 데이터 스트림이 없습니다. | 선택한 데이터 스트림 |
|---|---|
| <ul><li>[에지 세그멘테이션](../../../segmentation/ui/edge-segmentation.md) 은 지원되지 않습니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/configure-personalization-destinations.md) 지원되지 않습니다.</li><li>에 대해서만 세그먼트를 Adobe Target 연결에 공유할 수 있습니다 *기본 프로덕션 샌드박스*.</li><li>데이터 스트림 ID를 사용하지 않고 다음 세션 개인화를 구성하려면 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>에지 세그먼테이션은 예상대로 작동합니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/configure-personalization-destinations.md) 이 지원됩니다.</li><li>다른 샌드박스에 대해 세그먼트 공유가 지원됩니다.</li></ul> |

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [프로필 요청 대상에 프로필 및 세그먼트 활성화](../../ui/activate-profile-request-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

Adobe Target은 Adobe Experience Platform Edge Network에서 프로필 데이터를 읽으므로 데이터를 내보내지 않습니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).
