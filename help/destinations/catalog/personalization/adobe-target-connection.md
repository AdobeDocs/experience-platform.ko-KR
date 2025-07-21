---
keywords: target 개인화, 대상, experience platform 대상, adobe target 대상,
title: Adobe Target 연결
description: Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험 기능을 제공하는 애플리케이션입니다.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: c037e75da7fa419051a7e38b365a5b6b3a1fc346
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 9%

---

# Adobe Target 연결 {#adobe-target-connection}

## 대상 변경 로그 {#changelog}

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 4월 | 기능 및 설명서 업데이트 | Target 대상에 연결하고 데이터 스트림을 사용할 때 이제 *에지 세그멘테이션을 위해 데이터 스트림을 활성화할 필요가 없습니다*. 즉, 수행할 수 있는 사용 사례는 다르지만 Target 대상이 일괄 처리 및 스트리밍 대상에서 작동합니다. 자세한 내용은 [연결 매개 변수](#parameters) 섹션의 표를 참조하십시오. |
| 2024년 1월 | 기능 및 설명서 업데이트 | 이제 기본 프로덕션 샌드박스 및 기타 기본이 아닌 샌드박스에 대해 Adobe Target 연결에 대상 및 프로필 속성을 공유할 수 있습니다. |
| 2023년 6월 | 기능 및 설명서 업데이트 | 2023년 6월부터 새 Adobe Target 대상 연결을 구성할 때 대상을 공유할 Adobe Target 작업 영역을 선택할 수 있습니다. 자세한 내용은 [연결 매개변수](#parameters) 섹션을 참조하십시오. 추가로 작업 영역에 대한 자세한 내용은 Adobe Target에서 [작업 공간을 구성하는 방법](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html)에 대한 튜토리얼을 참조하십시오. |
| 2023년 5월 | 기능 및 설명서 업데이트 | 2023년 5월부터 **[!UICONTROL Adobe Target]** 연결은 [특성 기반 개인화](../../ui/activate-edge-personalization-destinations.md#map-attributes)를 지원하며 일반적으로 모든 고객이 사용할 수 있습니다. |

{style="table-layout:auto"}

## 개요 {#overview}

Adobe Target은 웹 사이트, 모바일 앱 등을 통해 모든 인바운드 고객 상호 작용에서 실시간 AI 기반 개인화 및 실험 기능을 제공하는 애플리케이션입니다.

Adobe Target은 Adobe Experience Platform 대상 카탈로그의 개인화 연결입니다.

## 비디오 개요 {#video-overview}

Experience Platform에서 Adobe Target 연결을 구성하는 방법에 대한 간략한 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 구현 유형에 따라 지원되는 사용 사례 {#supported-use-cases}

아래 표에는 구현 유형에 따라 [Web SDK](/help/web-sdk/home.md)의 사용 여부와 [에지 세분화](/help/segmentation/home.md#edge)의 사용 여부에 따라 Adobe Target 대상에 대해 지원되는 사용 사례가 표시됩니다.

| Adobe Target 구현 *없음* Web SDK | Adobe Target 구현 *사용* Web SDK | Adobe Target 구현 *사용* Web SDK *및* 에지 세분화 해제 |
|---|---|---|
| <ul><li>데이터 스트림은 필요하지 않습니다. Adobe Target은 [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [서버측](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation) 또는 [하이브리드](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) 구현 메서드를 통해 배포할 수 있습니다.</li><li>[Edge 세그멘테이션](../../../segmentation/methods/edge-segmentation.md)은(는) 지원되지 않습니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md)는 지원되지 않습니다.</li><li>*기본 프로덕션 샌드박스* 및 기본값이 아닌 샌드박스에 대해 대상과 프로필 속성을 Adobe Target 연결에 공유할 수 있습니다.</li><li>데이터 스트림을 사용하지 않고 다음 세션 개인 맞춤화를 구성하려면 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html)을(를) 사용합니다.</li></ul> | <ul><li>Adobe Target 및 Experience Platform이 서비스로 구성된 데이터 스트림이 필요합니다.</li><li>Edge 세그멘테이션은 예상대로 작동합니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md#use-cases)가 지원됩니다.</li><li>다른 샌드박스의 대상 및 프로필 속성 공유가 지원됩니다.</li></ul> | <ul><li>Adobe Target 및 Experience Platform이 서비스로 구성된 데이터 스트림이 필요합니다.</li><li>[데이터 스트림을 구성](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)할 때 **Edge 세그먼테이션** 확인란을 선택하지 마십시오.</li><li>[다음 세션 개인화](../../ui/activate-edge-personalization-destinations.md#next-session)가 지원됩니다.</li><li>다른 샌드박스의 대상 및 프로필 속성 공유가 지원됩니다.</li></ul> |


## 전제 조건 {#prerequisites}

### 데이터 스트림 {#datastream}

[데이터 스트림 사용](#parameters)에 Adobe Target 연결을 구성할 때는 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md)을 구현해야 합니다.

데이터스트림을 사용하지 않고 Adobe Target 연결을 구성해도 웹 SDK을 구현할 필요가 없습니다.

>[!IMPORTANT]
>
>[!DNL Adobe Target] 연결을 만들기 전에 [동일 페이지 및 다음 페이지 개인화에 대한 개인화 대상을 구성](../../ui/activate-edge-personalization-destinations.md)하는 방법에 대한 안내서를 읽어 보십시오. 이 안내서는 여러 Experience Platform 구성 요소에서 동일한 페이지 및 다음 페이지 개인화 사용 사례에 필요한 구성 단계를 안내합니다. 동일한 페이지 및 다음 페이지 개인화 사용 사례를 달성하려면 Adobe Target 연결을 구성할 때 데이터 스트림을 사용해야 합니다.

### Adobe Target의 사전 요구 사항 {#prerequisites-in-adobe-target}

Adobe Target에서 사용자에게 다음이 있는지 확인합니다.

* [기본 작업 영역](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace)에 액세스;
* **승인자** [역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

[Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 및 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions)에 대한 권한 부여에 대해 자세히 알아보십시오.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

>[!IMPORTANT]
>
>동일한 페이지 및 다음 페이지 개인화 사용 사례&#x200B;*에 대해* Edge 대상을 활성화할 때 대상 *필수*&#x200B;이(가) [Active-On-Edge 병합 정책](../../../segmentation/ui/segment-builder.md#merge-policies)을(를) 사용합니다. [!DNL active-on-edge] 병합 정책을 사용하면 대상이 [Edge](../../../segmentation/methods/edge-segmentation.md)에서 지속적으로 평가되고 실시간 및 다음 페이지 개인화 사용 사례에 사용할 수 있습니다.  구현 유형에 따라 [사용 가능한 모든 사용 사례](#parameter)를 읽어 보십시오.
>&#x200B;>다른 병합 정책을 사용하는 Edge 대상을 Adobe Target 대상에 매핑하면 실시간 및 다음 페이지 사용 사례에 대해 해당 대상이 평가되지 않습니다.
>&#x200B;>[병합 정책 만들기](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy)에 대한 지침을 따르고 **[!UICONTROL Active-On-Edge 병합 정책]** 전환을 사용하도록 설정해야 합니다.


| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!DNL Profile request]** | 단일 프로필에 대해 Adobe Target 대상에 매핑된 모든 대상을 요청합니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="데이터스트림 정보"
>abstract="이 옵션은 대상자에 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에 Target 구성이 활성화된 데이터스트림만 표시됩니다. 에지 세분화를 사용하려면 데이터 스트림을 선택해야 합니다. 없음을 선택하면 에지 세분화를 사용하는 모든 사용 사례가 비활성화됩니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="데이터스트림 선택에 대해 자세히 알아보기"

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

Adobe Experience Platform은 자동으로 회사의 Adobe Target 인스턴스에 연결합니다. 인증이 필요하지 않습니다.

### 연결 매개변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Adobe Target 작업 영역 정보"
>abstract="대상자를 공유할 Adobe Target 작업 영역을 선택하십시오. 각 Adobe Target 연결에 대해 단일 작업 영역을 선택할 수 있습니다. 활성화 시 대상자는 해당하는 Experience Platform 데이터 사용 레이블을 따르는 동안 선택한 작업 영역으로 라우팅됩니다."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html" text="Adobe Target 작업 영역에 대해 자세히 알아보기"

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **이름**: 이 대상의 기본 이름을 입력하십시오.
* **설명**: 대상에 대한 설명을 입력하십시오. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다. 이 필드는 선택 사항입니다.
* **데이터스트림**: 대상자가 포함될 데이터 수집 데이터스트림을 결정합니다. 드롭다운 메뉴에는 Target 및 Adobe Experience Platform 서비스가 활성화된 데이터스트림만 표시됩니다. Adobe Experience Platform 및 Adobe Target용 데이터 스트림을 구성하는 방법에 대한 자세한 내용은 [데이터 스트림 구성](../../../datastreams/configure.md#aep)을 참조하십시오.

  >[!IMPORTANT]
  >
  >데이터 스트림은 각 Adobe Target 대상 연결에 대해 고유합니다. 여러 Adobe Target 대상 연결에 동일한 데이터스트림을 사용할 수 없습니다.
  >동일한 대상을 여러 데이터스트림에 매핑해야 하는 경우에는 각 데이터스트림에 대해 [새 대상 연결을 만들고](../../ui/connect-destination.md)다음 [대상 활성화 흐름](#activate)을 거쳐야 합니다.

   * **[!UICONTROL 없음]**: Adobe Target 개인화를 구성해야 하지만 [Experience Platform Web SDK](/help/web-sdk/home.md)을(를) 구현할 수 없는 경우 이 옵션을 선택하십시오. 이 옵션을 사용하는 경우 Experience Platform에서 Target으로 내보낸 대상은 다음 세션 개인화만 지원하며 에지 세분화는 비활성화됩니다. 구현 유형별 사용 가능한 사용 사례를 비교하려면 [지원되는 사용 사례](#supported-use-cases) 섹션의 표를 참조하십시오.

  | Adobe Target 구현 *없음* Web SDK | Adobe Target 구현 *사용* Web SDK | Adobe Target 구현 *사용* Web SDK *및* 에지 세분화 해제 |
  |---|---|---|
  | <ul><li>데이터 스트림은 필요하지 않습니다. Adobe Target은 [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [서버측](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation) 또는 [하이브리드](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) 구현 메서드를 통해 배포할 수 있습니다.</li><li>[Edge 세그멘테이션](../../../segmentation/methods/edge-segmentation.md)은(는) 지원되지 않습니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md)는 지원되지 않습니다.</li><li>*기본 프로덕션 샌드박스* 및 기본값이 아닌 샌드박스에 대해 대상과 프로필 속성을 Adobe Target 연결에 공유할 수 있습니다.</li><li>데이터 스트림을 사용하지 않고 다음 세션 개인 맞춤화를 구성하려면 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html)을(를) 사용합니다.</li></ul> | <ul><li>Adobe Target 및 Experience Platform이 서비스로 구성된 데이터 스트림이 필요합니다.</li><li>Edge 세그멘테이션은 예상대로 작동합니다.</li><li>[동일 페이지 및 다음 페이지 개인화](../../ui/activate-edge-personalization-destinations.md#use-cases)가 지원됩니다.</li><li>다른 샌드박스의 대상 및 프로필 속성 공유가 지원됩니다.</li></ul> | <ul><li>Adobe Target 및 Experience Platform이 서비스로 구성된 데이터 스트림이 필요합니다.</li><li>[데이터 스트림을 구성](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)할 때 **Edge 세그먼테이션** 확인란을 선택하지 마십시오.</li><li>[다음 세션 개인화](../../ui/activate-edge-personalization-destinations.md#next-session)가 지원됩니다.</li><li>다른 샌드박스의 대상 및 프로필 속성 공유가 지원됩니다.</li></ul> |

* **Workspace**: 대상을 공유할 Adobe Target [작업 영역](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html)을(를) 선택하십시오. 각 Adobe Target 연결에 대해 단일 작업 영역을 선택할 수 있습니다. 활성화하면 적용 가능한 [Experience Platform 데이터 사용 레이블](../../../data-governance/labels/overview.md)을 따르는 동안 대상자가 선택한 작업 영역으로 라우팅됩니다.

>[!NOTE]
>
>[특성이 있는 동일 페이지 및 다음 페이지 개인화를 위해 사용자 지정 Target 작업 영역](../../ui/activate-edge-personalization-destinations.md)을 사용하는 경우 [선택한 대상](../../ui/activate-edge-personalization-destinations.md#select-audiences)만 선택한 Target 작업 영역으로 전송됩니다. [매핑된 특성](../../ui/activate-edge-personalization-destinations.md#mapping)이(가) 기본 Target 작업 영역으로 전송됩니다.
>&#x200B;><br>
>&#x200B;>이 동작은 향후 업데이트에서 변경됩니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 대한 대상을 활성화하는 방법에 대한 지침은 [Edge 개인화 대상에 대상 활성화](../../ui/activate-edge-personalization-destinations.md)를 참조하십시오.

## Target 대상에서 대상 제거 {#remove}

기존 Adobe Target 연결에서 대상을 제거하는 데 필요한 추가 단계가 있습니다. 해당 대상이 이미 Adobe Target [activity](https://experienceleague.adobe.com/en/docs/target/using/activities/activities)에서 사용되고 있습니다. Adobe Target 활동에서 대상을 사용하는 경우 Adobe Target 연결에서 대상을 제거하려고 하면 오류가 발생합니다.

![Target 활동에서 사용하는 대상을 제거하려고 시도하여 오류가 표시되는 Experience Platform UI 이미지입니다.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

활동에서 대상을 사용 중일 때 Target 대상에서 대상을 제거하려면 먼저 대상을 사용 중인 Target 활동에서 대상을 제거하거나 활동을 모두 삭제해야 합니다. 그런 다음 Target 연결에서 대상을 제거할 수 있습니다.

대상자가 활동에서 사용되고 있지 않으면 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** > **[!UICONTROL 대상 데이터 흐름 선택]** > **[!UICONTROL 활성화 데이터]**(으)로 이동하여 제거할 대상자를 선택한 다음 **[!UICONTROL 대상자 제거]**&#x200B;를 선택하십시오.

## 내보낸 데이터 {#exported-data}

Adobe Target Adobe Experience Platform Edge Network에서 프로필 데이터를 *읽기*&#x200B;하므로 데이터를 내보내지 않습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)를 참조하십시오.
