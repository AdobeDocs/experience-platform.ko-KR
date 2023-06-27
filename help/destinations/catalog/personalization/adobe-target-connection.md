---
keywords: target 개인화, 대상, experience platform 대상, adobe target 대상,
title: Adobe Target 연결
description: Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험 기능을 제공하는 애플리케이션입니다.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 3b2fedf4f7b17c4fb32afb5978bfac6f618f5bc3
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 17%

---

# Adobe Target 연결 {#adobe-target-connection}

## 대상 변경 로그 {#changelog}

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 6월 | 기능 및 설명서 업데이트 | 2023년 6월부터 새 Adobe Target 대상 연결을 구성할 때 대상을 공유할 Adobe Target 작업 영역을 선택할 수 있습니다. 자세한 내용은 [연결 매개변수](#parameters) 섹션을 참조하십시오. 추가로 작업 영역에 대한 자세한 내용은 Adobe Target에서 [작업 공간을 구성하는 방법](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en)에 대한 튜토리얼을 참조하십시오. |
| 2023년 5월 | 기능 및 설명서 업데이트 | 2023년 5월 현재 **[!UICONTROL Adobe Target]** 연결 지원 [속성 기반 개인화](../../ui/activate-edge-personalization-destinations.md#map-attributes) 및 는 일반적으로 모든 고객이 사용할 수 있습니다. |

{style="table-layout:auto"}

## 개요 {#overview}

Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험 기능을 제공하는 애플리케이션입니다.

Adobe Target은 Adobe Experience Platform 대상 카탈로그의 개인화 연결입니다.

Experience Platform에서 Adobe Target 연결을 구성하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 사전 요구 사항 {#prerequisites}

### 데이터 스트림 ID {#datastream-id}

에 Adobe Target 연결을 구성할 때 [데이터 스트림 ID 사용](#parameters), 다음 권한이 있어야 합니다. [Adobe Experience Platform 웹 SDK](../../../edge/home.md) 을 구현했습니다.

데이터 스트림 ID를 사용하지 않고 Adobe Target 연결을 구성해도 웹 SDK를 구현할 필요가 없습니다.

>[!IMPORTANT]
>
>만들기 전 [!DNL Adobe Target] 연결, 방법에 대한 안내서 읽기 [동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](../../ui/activate-edge-personalization-destinations.md). 이 안내서에서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다. 동일 페이지 및 다음 페이지 개인화를 사용하려면 Adobe Target 연결을 구성할 때 데이터 스트림 ID를 사용해야 합니다.

### Adobe Target의 사전 요구 사항 {#prerequisites-in-adobe-target}

Adobe Target에서 사용자에게 다음이 있는지 확인합니다.

* 액세스 권한: [기본 작업 영역](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* 다음 **승인자** [역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

다음에 대한 권한 부여에 대해 자세히 알아보십시오. [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) 및 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!DNL Profile request]** | 단일 프로필에 대해 Adobe Target 대상에서 매핑된 모든 세그먼트를 요청하고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="데이터스트림 ID 정보"
>abstract="이 옵션은 세그먼트에 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 Target 구성이 활성화된 데이터스트림만 표시됩니다. 에지 세분화를 사용하려면 데이터스트림 ID를 선택해야 합니다. 없음을 선택하면 에지 세분화를 사용하는 모든 사용 사례가 비활성화됩니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ko-KR#parameters" text="데이터스트림 선택에 대해 자세히 알아보기"

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

Adobe Experience Platform은 자동으로 회사의 Adobe Target 인스턴스에 연결합니다. 인증이 필요하지 않습니다.

### 연결 매개 변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Adobe Target 작업 영역 정보"
>abstract="대상자를 공유할 Adobe Target 작업 영역을 선택하십시오. 각 Adobe Target 연결에 대해 단일 작업 영역을 선택할 수 있습니다. 활성화 시 대상자는 해당하는 Experience Platform 데이터 사용 레이블을 따르는 동안 선택한 작업 영역으로 라우팅됩니다."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en" text="Adobe Target 작업 영역에 대해 자세히 알아보기"

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **이름**: 이 대상의 기본 이름을 입력합니다.
* **설명**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **데이터 스트림 ID**: 세그먼트를 포함할 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에는 Target 및 Adobe Experience Platform 서비스가 활성화된 데이터스트림만 표시됩니다. 다음을 참조하십시오 [데이터스트림 구성](../../../edge/datastreams/configure.md#aep) Adobe Experience Platform 및 Adobe Target용 데이터스트림을 구성하는 방법에 대한 자세한 내용
   * **[!UICONTROL 없음]**: Adobe Target 개인화를 구성해야 하지만 를 구현할 수 없는 경우 이 옵션을 선택하십시오. [Experience Platform Web SDK](../../../edge/home.md). 이 옵션을 사용하는 경우 Experience Platform에서 Target으로 내보낸 세그먼트는 다음 세션 개인화만 지원하며 에지 세분화는 비활성화됩니다. 자세한 내용은 아래 표를 참조하십시오.
* **작업 영역**: Adobe Target 선택 [작업 영역](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) 대상자를 공유할 대상. 각 Adobe Target 연결에 대해 단일 작업 영역을 선택할 수 있습니다. 활성화 시 대상자는 적용 가능한 단계에 따라 선택한 작업공간으로 라우팅됩니다 [Experience Platform 데이터 사용 레이블](../../../data-governance/labels/overview.md).

| 선택한 데이터 스트림 없음 | 데이터 스트림 선택됨 |
|---|---|
| <ul><li>[에지 세분화](../../../segmentation/ui/edge-segmentation.md) 은(는) 지원되지 않습니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md) 은(는) 지원되지 않습니다.</li><li>에 대해서만 Adobe Target 연결에 세그먼트를 공유할 수 있습니다. *기본 프로덕션 샌드박스*.</li><li>데이터 스트림 ID를 사용하지 않고 다음 세션 개인화를 구성하려면 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>에지 세분화는 예상대로 작동합니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md) 이 지원됩니다.</li><li>다른 샌드박스에 대해 세그먼트 공유가 지원됩니다.</li></ul> |

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [프로필 요청 대상에 프로필 및 세그먼트 활성화](../../ui/activate-edge-personalization-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

## 내보낸 데이터 {#exported-data}

Adobe Target은 Adobe Experience Platform Edge Network에서 프로필 데이터를 읽으므로 데이터를 내보내지 않습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).
