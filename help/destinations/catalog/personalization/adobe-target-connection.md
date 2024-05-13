---
keywords: target 개인화, 대상, experience platform 대상, adobe target 대상,
title: Adobe Target 연결
description: Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험 기능을 제공하는 애플리케이션입니다.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: e9777960f347e32ff6288227ef95cec9cc4c55e7
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 11%

---

# Adobe Target 연결 {#adobe-target-connection}

## 대상 변경 로그 {#changelog}

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 4월 | 기능 및 설명서 업데이트 | 이제 데이터 스트림 ID를 사용하여 로 Target 대상에 연결할 때 다음을 수행합니다 *필요 없음* 를 사용하여 에지 세분화를 위해 데이터스트림을 활성화해야 합니다. 즉, 수행할 수 있는 사용 사례는 다르지만 Target 대상이 일괄 처리 및 스트리밍 대상에서 작동합니다. 다음에서 테이블 보기: [연결 매개 변수](#parameters) 섹션에 자세히 설명되어 있습니다. |
| 2024년 1월 | 기능 및 설명서 업데이트 | 이제 기본 프로덕션 샌드박스 및 기타 기본이 아닌 샌드박스에 대해 Adobe Target 연결에 대상 및 프로필 속성을 공유할 수 있습니다. |
| 2023년 6월 | 기능 및 설명서 업데이트 | 2023년 6월부터 새 Adobe Target 대상 연결을 구성할 때 대상을 공유할 Adobe Target 작업 영역을 선택할 수 있습니다. 자세한 내용은 [연결 매개변수](#parameters) 섹션을 참조하십시오. 추가로 작업 영역에 대한 자세한 내용은 Adobe Target에서 [작업 공간을 구성하는 방법](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=ko-KR)에 대한 튜토리얼을 참조하십시오. |
| 2023년 5월 | 기능 및 설명서 업데이트 | 2023년 5월 현재 **[!UICONTROL Adobe Target]** 연결 지원 [속성 기반 개인화](../../ui/activate-edge-personalization-destinations.md#map-attributes) 및 는 일반적으로 모든 고객이 사용할 수 있습니다. |

{style="table-layout:auto"}

## 개요 {#overview}

Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험 기능을 제공하는 애플리케이션입니다.

Adobe Target은 Adobe Experience Platform 대상 카탈로그의 개인화 연결입니다.

## 비디오 개요 {#video-overview}

Experience Platform에서 Adobe Target 연결을 구성하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 전제 조건 {#prerequisites}

### 데이터 스트림 ID {#datastream-id}

에 Adobe Target 연결을 구성할 때 [데이터 스트림 ID 사용](#parameters), 다음 권한이 있어야 합니다. [Adobe Experience Platform 웹 SDK](/help/web-sdk/home.md) 을 구현했습니다.

데이터 스트림 ID를 사용하지 않고 Adobe Target 연결을 구성해도 웹 SDK를 구현할 필요가 없습니다.

>[!IMPORTANT]
>
>만들기 전 [!DNL Adobe Target] 연결, 방법에 대한 안내서 읽기 [동일 페이지 및 다음 페이지 개인화를 위한 개인화 대상 구성](../../ui/activate-edge-personalization-destinations.md). 이 안내서에서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다. 동일한 페이지 및 다음 페이지 개인화 사용 사례를 달성하려면 Adobe Target 연결을 구성할 때 데이터 스트림 ID를 사용해야 합니다.

### Adobe Target의 사전 요구 사항 {#prerequisites-in-adobe-target}

Adobe Target에서 사용자에게 다음이 있는지 확인합니다.

* 액세스 권한: [기본 작업 영역](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* 다음 **승인자** [역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

다음에 대한 권한 부여에 대해 자세히 알아보십시오. [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 및 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | X | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!DNL Profile request]** | 단일 프로필에 대해 Adobe Target 대상에 매핑된 모든 대상을 요청합니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="데이터스트림 ID 정보"
>abstract="이 옵션은 대상자에 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 Target 구성이 활성화된 데이터스트림만 표시됩니다. 에지 세분화를 사용하려면 데이터스트림 ID를 선택해야 합니다. 없음을 선택하면 에지 세분화를 사용하는 모든 사용 사례가 비활성화됩니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ko-KR#parameters" text="데이터스트림 선택에 대해 자세히 알아보기"

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

Adobe Experience Platform은 자동으로 회사의 Adobe Target 인스턴스에 연결합니다. 인증이 필요하지 않습니다.

### 연결 매개변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Adobe Target 작업 영역 정보"
>abstract="대상자를 공유할 Adobe Target 작업 영역을 선택하십시오. 각 Adobe Target 연결에 대해 단일 작업 영역을 선택할 수 있습니다. 활성화 시 대상자는 해당하는 Experience Platform 데이터 사용 레이블을 따르는 동안 선택한 작업 영역으로 라우팅됩니다."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=ko-KR" text="Adobe Target 작업 영역에 대해 자세히 알아보기"

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **이름**: 이 대상의 기본 이름을 입력합니다.
* **설명**: 대상에 대한 설명을 입력합니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **데이터 스트림 ID**: 대상자를 포함할 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에는 Target 및 Adobe Experience Platform 서비스가 활성화된 데이터스트림만 표시됩니다. 다음을 참조하십시오 [데이터스트림 구성](../../../datastreams/configure.md#aep) Adobe Experience Platform 및 Adobe Target용 데이터스트림을 구성하는 방법에 대한 자세한 내용

  >[!IMPORTANT]
  >
  >데이터 스트림 ID는 각 Adobe Target 대상 연결에 대해 고유합니다. 동일한 대상을 여러 데이터 스트림에 매핑해야 하는 경우에는 다음을 수행해야 합니다 [새 대상 연결 만들기](../../ui/connect-destination.md) 각 데이터 스트림 ID에 대해 다음을 수행하십시오. [대상자 활성화 흐름](#activate).

   * **[!UICONTROL 없음]**: Adobe Target 개인화를 구성해야 하지만 를 구현할 수 없는 경우 이 옵션을 선택하십시오. [Experience Platform Web SDK](/help/web-sdk/home.md). 이 옵션을 사용하는 경우 Experience Platform에서 Target으로 내보낸 대상은 다음 세션 개인화만 지원하며 에지 세분화는 비활성화됩니다. 구현 유형별 사용 가능한 사용 사례를 비교하려면 아래 표를 참조하십시오.

  | Adobe Target 구현 *없이* 웹 SDK | Adobe Target 구현 *포함* 웹 SDK | Adobe Target 구현 *포함* 웹 SDK *및* 에지 세분화 끄기 |
  |---|---|---|
  | <ul><li>데이터 스트림은 필요하지 않습니다. Adobe Target은 다음을 통해 배포할 수 있습니다. [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [서버측](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation), 또는 [잡종](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) 구현 방법.</li><li>[에지 세분화](../../../segmentation/ui/edge-segmentation.md) 은(는) 지원되지 않습니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md) 은(는) 지원되지 않습니다.</li><li>대상 및 프로필 속성을 의 Adobe Target 연결에 공유할 수 있습니다. *기본 프로덕션 샌드박스* 및 기본값이 아닌 샌드박스.</li><li>데이터 스트림 ID를 사용하지 않고 다음 세션 개인화를 구성하려면 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>Adobe Target 및 Experience Platform이 서비스로 구성된 데이터 스트림이 필요합니다.</li><li>에지 세분화는 예상대로 작동합니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md#use-cases) 이 지원됩니다.</li><li>다른 샌드박스의 대상 및 프로필 속성 공유가 지원됩니다.</li></ul> | <ul><li>Adobe Target 및 Experience Platform이 서비스로 구성된 데이터 스트림이 필요합니다.</li><li>날짜 [데이터스트림 구성](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), 을(를) 선택하지 마십시오. **에지 세분화** 확인란.</li><li>[다음 세션 개인화](../../ui/activate-edge-personalization-destinations.md#next-session) 은(는) 지원됩니다.</li><li>다른 샌드박스의 대상 및 프로필 속성 공유가 지원됩니다.</li></ul> |

* **작업 영역**: Adobe Target 선택 [작업 영역](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=ko-KR) 대상자를 공유할 대상. 각 Adobe Target 연결에 대해 단일 작업 영역을 선택할 수 있습니다. 활성화 시 대상자는 적용 가능한 단계에 따라 선택한 작업공간으로 라우팅됩니다 [Experience Platform 데이터 사용 레이블](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>다음에 대한 사용자 지정 Target 작업 영역을 사용할 때 [속성을 사용한 동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md), 만 [선택한 대상자](../../ui/activate-edge-personalization-destinations.md#select-audiences) 선택된 Target 작업 영역으로 전송됩니다. 다음 [매핑된 속성](../../ui/activate-edge-personalization-destinations.md#mapping) 기본 Target 작업 영역으로 전송됩니다.
><br>
>이 동작은 향후 업데이트에서 변경됩니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [Edge 개인화 대상에 대한 대상자 활성화](../../ui/activate-edge-personalization-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## Target 대상에서 대상 제거 {#remove}

기존 Adobe Target 연결에서 대상을 이미 Adobe Target에서 사용 중인 경우 해당 대상을 제거하는 데 필요한 추가 단계가 있습니다 [활동](https://experienceleague.adobe.com/en/docs/target/using/activities/activities). Adobe Target 활동에서 대상을 사용하는 경우 Adobe Target 연결에서 대상을 제거하려고 하면 오류가 발생합니다.

![Target 활동에서 사용하는 대상을 제거하려고 시도하는 것으로 인해 오류가 표시되는 플랫폼 UI 이미지입니다.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

활동에서 대상을 사용 중일 때 Target 대상에서 대상을 제거하려면 먼저 대상을 사용 중인 Target 활동에서 대상을 제거하거나 활동을 모두 삭제해야 합니다. 그런 다음 Target 연결에서 대상을 제거할 수 있습니다.

대상자가 활동에서 사용되고 있지 않다면 다음 위치로 이동하십시오. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** > **[!UICONTROL 대상 데이터 흐름 선택]** > **[!UICONTROL 활성화 데이터]**&#x200B;제거할 대상자를 선택한 다음 을 선택합니다 **[!UICONTROL 대상자 제거]**.

## 내보낸 데이터 {#exported-data}

Adobe Target *읽기* Adobe Experience Platform Edge Network의 프로필 데이터이므로 데이터를 내보내지 않습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).
