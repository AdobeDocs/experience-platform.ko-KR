---
keywords: advertising; the trade desk;
title: 더 트레이드데스크
seo-title: 더 트레이드데스크
description: '트레이드데스크(Trade Desk)는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 리타겟팅하고 실행할 수 있는 셀프 서비스 플랫폼입니다. '
seo-description: 트레이드데스크(Trade Desk)는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 리타겟팅하고 실행할 수 있는 셀프 서비스 플랫폼입니다.
translation-type: tm+mt
source-git-commit: a64f9f1f078d8380cc25c9760eac1699512a5870
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# [!DNL The Trade Desk] 대상

## 개요 {#overview}

[!DNL The Trade Desk] 대상을 사용하면 프로필 데이터를 보낼 수 있습니다 [!DNL The Trade Desk].

[!DNL The Trade Desk] 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 리타겟팅하고 실행할 수 있는 셀프 서비스 플랫폼입니다.

프로필 데이터를 대상 [!DNL The Trade Desk]으로 보내려면 먼저 대상에 연결해야 합니다.

## 대상 사양 {#destination-specs}

대상에 대한 다음 세부 사항을 [!DNL The Trade Desk] 참고하십시오.

* 다음 ID를 [대상으로](../../identity-service/namespaces.md) 보낼 수 [!DNL The Trade Desk] 있습니다. [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## 사용 사례 {#use-cases}

마케터는 [!DNL Trade Desk IDs] 또 다른 디바이스 ID로 구축된 세그먼트를 사용하여 리타겟팅이나 고객 타겟팅된 디지털 캠페인을 제작하고 싶습니다.

## 내보내기 유형 {#export-type}

**[!DNL Segment export]** - 세그먼트(대상)의 모든 멤버를 대상으로 내보냅니다.

## 대상에 연결 {#connect-destination}

1. [ **[!UICONTROL 연결]** ] > **[!UICONTROL 대상]**&#x200B;에서 [!DNL The Trade Desk]를 선택하고 구성을 **[!UICONTROL 선택합니다]**.

   ![무역부 대상 구성](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 **[!UICONTROL 의 차이에 대한 자세한]****[!UICONTROL 내용은 대상 작업 공간 설명서의]**&#x200B;카탈로그 [섹션을](../destinations/destinations-workspace.md#catalog) 참조하십시오.
   >
   >![무역부 대상 활성화](assets/tradedesk-destination-activate.png)

2. 인증 [!UICONTROL 단계에서] 연결 [!DNL The Trade Desk] 세부 사항을 입력해야 합니다.

   * **[!UICONTROL 이름]**:나중에 이 대상을 인식하는 이름입니다.
   * **[!UICONTROL 설명]**:나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
   * **[!UICONTROL 계정 ID]**:계정 [!DNL Trade Desk] ID .
   * **[!UICONTROL 클라이언트 암호]**:클라이언트 자격 증명 `clientSecret` 에 사용되는 [!DNL OAuth2] 매개 변수입니다.
   * **[!UICONTROL 서버 위치]**:사용해야 하는 지역 서버를 담당자에게 [!DNL The Trade Desk] 문의하십시오. 다음 중에서 선택할 수 있는 지역 서버가 있습니다.

      * **[!UICONTROL 유럽]**
      * **[!UICONTROL 싱가포르]**
      * **[!UICONTROL 도쿄]**
      * **[!UICONTROL 북미 동부]**
      * **[!UICONTROL 북미 서부]**
      * **[!UICONTROL 라틴 아메리카]**
   * **[!UICONTROL 마케팅 활용 사례]**:마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 사용 사례에 대한 자세한 내용은 Adobe Experience Platform의 [데이터 거버넌스](../privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](../../data-governance/policies/overview.md#core-actions).

   ![Trade Desk Authentication Step](assets/tradedesk-destination-authentication.png)

3. 대상 **[!UICONTROL 만들기를 클릭합니다]**. 이제 대상이 만들어집니다. 나중에 세그먼트를 [!UICONTROL 활성화하려면 저장] 및 종료를 [!UICONTROL 클릭하거나] 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 두 경우 모두 워크플로우의 나머지 [에 대해 다음 섹션, 세그먼트](#activate-segments)활성화를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](activate-destinations.md#select-attributes) 프로필 및 세그먼트 활성화를 참조하십시오.

세그먼트 [예약](activate-destinations.md#segment-schedule) 단계에서 세그먼트를 대상의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑하는 경우 쉽게 사용할 수 있도록 세그먼트 [!DNL Platform] 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 그러나 대상의 세그먼트 ID 또는 이름은 [!DNL Platform] 계정의 세그먼트 ID와 일치하지 않아도 됩니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

여러 장치 매핑(쿠키 ID, [!DNL IDFA][!DNL GAID],)을 사용하는 경우 세 가지 매핑 모두에 동일한 매핑 값을 사용해야 합니다. [!DNL The Trade Desk] 모두 하나의 세그먼트로 취합하고 장치 수준 분류를 통해

![세그먼트 매핑 ID](assets/segment-mapping-id.png)


## 내보낸 데이터 {#exported-data}

데이터를 대상으로 성공적으로 [!DNL The Trade Desk] 내보냈는지 확인하려면 [!DNL The Trade Desk] 계정을 확인하십시오. 정품 인증이 성공적으로 완료되면 사용자의 계정에 대상이 채워집니다.
