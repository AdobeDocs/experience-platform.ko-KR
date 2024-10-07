---
title: 트레이드 데스크 실시간 전환 API 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 Trade Desk 실시간 전환 API 확장에 대해 알아봅니다.
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: eb650da02ac69c5afbebfe6ba371cc19617f79d0
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# [!DNL The Trade Desk Real-Time Conversions API] 확장 개요

[이벤트 전달](../../../ui/event-forwarding/overview.md) Edge Network에서 API의 기능을 사용하여 [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) 확장을 사용하여 Adobe Experience Platform 규칙에서 [!DNL The Trade Desk](으)로 데이터를 보낼 수 있습니다.

[!DNL The Trade Desk Real-Time Conversions API] 확장을 사용하면 [이벤트 전달](../../../ui/event-forwarding/overview.md) Edge Network에서 API의 기능을 활용하여 Adobe Experience Platform 규칙에서 [!DNL The Trade Desk](으)로 데이터를 보낼 수 있습니다.

확장을 설치하고 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)에서 해당 기능을 사용하는 방법을 알아보려면 이 문서를 참조하십시오.

>[!NOTE]
>
>이 확장 및 설명서 페이지는 [!DNL The Trade Desk] 팀에서 관리합니다. 문의 사항이나 업데이트 요청은 해당 업체에 직접 문의하시기 바랍니다.

## 전제 조건 {#prerequisites}

[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)을(를) 구성하려면 [!DNL The Trade Desk] 계정 내에서 관련 광고주 ID, UPixel ID 및 추적기 ID가 있어야 합니다.

>[!INFO]
>
>판매자인 경우 판매자 ID도 받아야 합니다.

## [!DNL The Trade Desk] 실시간 전환 API 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 대신 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 **[!UICONTROL 트레이드 데스크]** 실시간 전환 API 카드를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![설치를 강조 표시하는 [!DNL The Trade Desk] 확장 카드를 표시하는 확장 카탈로그입니다.](../../../images/extensions/server/tradedesk/install-extension.png)

다음 화면에서는 [!UICONTROL 광고주 ID]를 입력하고 선택적으로 [!UICONTROL 판매자 ID]를 입력합니다. ID의 를 이러한 입력에 직접 붙여넣거나 데이터 요소를 대신 사용할 수 있습니다. [!DNL The Trade Desk] 실시간 전환 API에 대한 이벤트 호출을 수행할 때 사용되는 기본값 역할을 합니다. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

데이터 요소를 만들고 태그 속성의 확장에 사용할 수 있도록 하는 방법에 대해 알아보려면 [데이터 요소 만들기](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) 자습서를 따르십시오.

![강조 표시된 [!UICONTROL 광고주 ID] 및 [!UICONTROL 판매자 ID] 필드의 [!DNL The Trade Desk] 확장 구성 페이지입니다.](../../../images/extensions/server/tradedesk/configure-extension.png)

확장이 설치되었으며 이제 이벤트 전달 규칙에 해당 기능을 사용할 수 있습니다.

## 이벤트 전달 규칙 구성 {#rule}

확장을 설치하고 구성했으면 이벤트를 [!DNL The Trade Desk]에 보내는 방법과 시기를 결정하는 이벤트 전달 규칙을 만들 수 있습니다.

[!DNL The Trade Desk] 및 [!DNL The Trade Desk] 실시간 전환 API를 통해 허용된 모든 [요청 속성](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties)을(를) 전송하려면 여러 규칙을 구성하는 것이 좋습니다.

>[!NOTE]
>
>실시간으로 또는 가능한 한 실시간에 가깝게 이벤트를 전송해야 합니다.

이벤트 전달 속성에 새 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)을(를) 만듭니다. **[!UICONTROL 작업]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL The Trade Desk]**(으)로 설정합니다. 그런 다음 **[!UICONTROL 작업 유형]**&#x200B;에 대해 **[!UICONTROL 실시간 전환]**&#x200B;을 선택합니다.

![이벤트 전달 규칙 작업 구성을 추가하는 데 필요한 필드가 강조 표시된 이벤트 전달 속성 규칙 보기입니다.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

선택 후 [!DNL The Trade Desk](으)로 전송할 이벤트 데이터를 추가로 구성하기 위한 추가 컨트롤이 나타납니다. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 규칙을 저장합니다.

구성 옵션은 아래에 설명된 대로 세 개의 기본 섹션으로 나뉩니다.

**[!UICONTROL 기본 요청 속성]**

| 입력 | 설명 |
| --- | --- |
| 추적기 ID | 이벤트 추적기의 플랫폼 ID입니다. |
| 픽셀 ID | 이벤트의 범용 픽셀 ID입니다. |
| 레퍼러 URL | 이벤트가 발생한 웹 사이트 URL(있는 경우). |
| 이벤트 이름 | 파트너 플랫폼에서 정의한 이벤트 유형입니다. |
| 값 | 10진수 문자열의 수익 추적 값(예: &quot;19.98&quot;). |
| 통화 | ISO 형식의 통화 코드. |
| 클라이언트 IP | 클라이언트 IPv4 또는 IPv6 IP 주소입니다. |
| 광고 ID | 이벤트에 대한 고유 광고 ID. |
| 광고 ID 유형 | 광고 ID 속성에 지정된 광고 ID의 유형: TDID, IDFA, AAID, DAID, NAID, IDL, EUID 또는 UID2. |
| 노출 횟수 | 이벤트가 기여하는 노출에 대한 고유 ID 역할을 하는 36자 문자열(대시 포함). |
| 주문 ID | 이벤트의 관련 주문 식별자. |
| td1-td10 | 추가 전환 메타데이터를 제공하는 데 사용할 수 있는 10개의 순차적으로 번호가 매겨진 사용자 지정 동적 속성입니다. |

{style="table-layout:auto"}

![필드에 입력된 데이터 예제를 보여 주는 [!DNL Basic Request Properties] 섹션입니다.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

[!DNL The Trade Desk] 실시간 전환 API에서 수락한 [요청 속성](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties)에 대한 자세한 내용은 [!DNL The Trade Desk] 개발자 설명서를 참조하십시오.

**[!UICONTROL 개체 요청 매개 변수]**

추가 정보가 포함된 JSON 개체. 축소된 키-값 입력 세트를 사용하거나 원시 JSON을 제공하는 옵션이 있습니다. 또한 오른쪽의 디스크(![디스크 아이콘](/help/images/icons/database.png))를 선택하여 데이터 요소에서 동적 데이터를 검색할 수 있습니다.


![사용 가능한 필드를 표시하는 [!DNL Object Request Parameters] 섹션입니다.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

[!UICONTROL 개체 요청 매개 변수] 및 해당 속성에 대한 자세한 내용은 [실시간 전환 이벤트](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) 설명서를 참조하십시오.

**[!UICONTROL 구성 재정의]**

>[!NOTE]
>
>[!UICONTROL 구성 재정의] 필드를 사용하면 모든 규칙에서 다른 [!DNL Advertiser ID] 및/또는 [!DNL Merchant ID]을(를) 설정할 수 있습니다.

| 입력 | 설명 |
| --- | --- |
| 광고주 ID | 해당 이벤트와 연결된 광고주의 고유 식별자입니다. 확장 구성에서 제공한 ID를 재정의하기 위해 다른 광고주 ID를 제공할 수 있습니다. |
| 판매자 ID | 온보딩 절차 전체에서 [!DNL The Trade Desk]이(가) 각 판매자에게 제공하는 고유 식별자입니다. 확장 구성에서 제공한 ID를 재정의하기 위해 다른 판매자 ID를 제공할 수 있습니다. |

![사용 가능한 필드를 표시하는 [!DNL Configuration Overrides] 섹션입니다.](../../../images/extensions/server/tradedesk/configure-overrides.png)

규칙에 만족하면 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다. 마지막으로 새 이벤트 전달 [build](../../../ui/publishing/builds.md)을(를) 게시하여 라이브러리에 대한 변경 사항을 활성화하십시오.

## 다음 단계

이 안내서에서는 [!DNL The Trade Desk] 실시간 전환 API 확장을 사용하여 서버측 이벤트 데이터를 [!DNL The Trade Desk]에 보내는 방법을 다룹니다. 여기에서는 캠페인에 따라 적용할 수 있는 특정 전환 이벤트를 보내는 고유한 규칙을 만들어 통합을 확장하는 것이 좋습니다. [!DNL Adobe Experience Platform]의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하십시오.

통합을 효과적으로 구현하는 방법에 대한 자세한 지침은 [실시간 전환 API 모범 사례 [!DNL The Trade Desk] 의 [!DNL The Trade Desk] 설명서를 참조하십시오.](https://www.facebook.com/business/help/308855623839366?id=818859032317965)

Experience Platform 디버거 및 이벤트 전달 Adobe Experience Platform Debugger 도구를 사용하여 구현을 디버깅하는 방법에 대한 자세한 내용은 [모니터링 개요](../../../../debugger/home.md) 및 [이벤트 전달에서 활동 모니터링](../../../ui/event-forwarding/monitoring.md)을 참조하십시오.
