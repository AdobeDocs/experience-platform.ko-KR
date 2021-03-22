---
keywords: 광고;무역센터
title: 무역센터 연결
description: 'Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 리타겟팅하고 실행할 수 있는 셀프 서비스 플랫폼입니다. '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# [!DNL The Trade Desk] 연결

## 개요 {#overview}

[!DNL The Trade Desk] 대상은 프로필 데이터를 다음으로 보내는 데 도움이  [!DNL The Trade Desk]됩니다.

[!DNL The Trade Desk] 디스플레이, 비디오 및 모바일 인벤토리 소스에서 리타겟팅하고 대상 디지털 캠페인을 실행할 수 있는 광고 구매자를 위한 셀프 서비스 플랫폼입니다.

프로필 데이터를 [!DNL Trade Desk]에 보내려면 먼저 대상에 연결해야 합니다.

## 대상 사양 {#destination-specs}

[!DNL Trade Desk] 대상에 대한 다음 세부 사항을 참조하십시오.

* 다음 [id](../../../identity-service/namespaces.md)를 [!DNL The Trade Desk] 대상으로 보낼 수 있습니다.[!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

>[!IMPORTANT]
>
>[!DNL The Trade Desk]을(를) 사용하여 첫 번째 대상을 만들고 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을(를) 활성화하지 않은 경우(Adobe Audience Manager 또는 다른 응용 프로그램에서) Adobe 컨설팅 또는 고객 지원 센터에 문의하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL The Trade Desk] 통합을 설정한 경우 설정한 ID 동기화가 플랫폼으로 이월됩니다.

## 사용 사례 {#use-cases}

마케터로서, [!DNL Trade Desk IDs] 또는 디바이스 ID를 기반으로 구축된 세그먼트를 사용하여 리타겟팅 또는 대상 타깃팅된 디지털 캠페인을 만들 수 있기를 바랍니다.

## 내보내기 유형 {#export-type}

**[!DNL Segment export]** - 세그먼트(대상)의 모든 구성원을 대상으로 내보냅니다.

## 대상 {#connect-destination}에 연결

**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;에서 [!DNL The Trade Desk]를 선택하고 **[!UICONTROL Configure]**&#x200B;을 선택합니다.

![대상 거래 데스크 구성](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL Activate]** 단추가 표시될 수 있습니다. **[!UICONTROL Activate]**&#x200B;과 **[!UICONTROL Configure]** 사이의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.
>
>![대상 거래 센터 활성화](../../assets/catalog/advertising/tradedesk/activate.png)

[!UICONTROL Authentication] 단계에서 [!DNL The Trade Desk] 연결 세부 정보를 입력해야 합니다.

* **[!UICONTROL Name]**:나중에 이 대상을 인식할 이름.
* **[!UICONTROL Description]**:나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Account ID]**:고객 [!DNL Trade Desk] [!UICONTROL Account ID]의
* **[!UICONTROL Server Location]**:사용할  [!DNL Trade Desk] 지역 서버를 담당자에게 요청하십시오. 다음 중에서 선택할 수 있는 지역 서버가 있습니다.

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing action]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 Adobe Experience Platform](../../../data-governance/policies/overview.md) 페이지의 [데이터 거버넌스 페이지를 참조하십시오. 개별 Adobe 정의 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

![영업 데스크 인증 단계](../../assets/catalog/advertising/tradedesk/authenticate.png)

**[!UICONTROL Create destination]**&#x200B;을 클릭합니다. 이제 대상이 만들어집니다. 나중에 세그먼트를 활성화하려면 [!UICONTROL Save & Exit]을(를) 클릭하거나 [!UICONTROL Next]을(를) 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 이 두 경우 모두 나머지 워크플로에 대해 다음 섹션 [세그먼트 활성화](#activate-segments)를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md#select-attributes)에 활성화를 참조하십시오.

[세그먼트 일정](../../ui/activate-destinations.md#segment-schedule) 단계에서 세그먼트를 대상의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑하는 경우 사용하기 쉽도록 [!DNL Platform] 세그먼트 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 그러나 대상의 세그먼트 ID 또는 이름은 [!DNL Platform] 계정의 세그먼트 ID와 일치할 필요가 없습니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

여러 장치 매핑(쿠키 ID, [!DNL IDFA], [!DNL GAID])을 사용하는 경우 세 가지 매핑 모두에 동일한 매핑 값을 사용해야 합니다. [!DNL The Trade Desk] 이러한 모든 세그먼트를 하나의 세그먼트로 취합하고 장치 수준 분류를 사용합니다.

![세그먼트 매핑 ID](../../assets/common/segment-mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL The Trade Desk] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Trade Desk] 계정을 확인하십시오. 활성화가 성공하면 고객이 계정에 채워집니다.
