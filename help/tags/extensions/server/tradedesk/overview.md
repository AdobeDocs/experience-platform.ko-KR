---
title: 트레이드 데스크 실시간 전환 API 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 Trade Desk 실시간 전환 API 확장에 대해 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 8000bbf36e6763b8fca17c2ae0d5c2fe53bc6964
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 1%

---

# [!DNL The Trade Desk Real-Time Conversions API] 확장 개요

[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) 이벤트를 보낼 수 있습니다. [!DNL The Trade Desk] 리타겟팅 및 속성을 활용합니다.

다음을 사용할 수 있습니다. [!DNL The Trade Desk Real-Time Conversions API] Adobe Experience Platform Edge Network에서 (으)로 데이터를 전송하는 확장 [!DNL The Trade Desk] 에서 API의 기능을 활용하여 [이벤트 전달](../../../ui/event-forwarding/overview.md) 규칙.

사용 [!DNL The Trade Desk Real-Time Conversions API] 확장에서는 의 API 기능을 활용할 수 있습니다. [이벤트 전달](../../../ui/event-forwarding/overview.md) 데이터를 보낼 규칙 [!DNL The Trade Desk] Adobe Experience Platform Edge Network.

확장을 설치하고 이벤트 전달에서 해당 기능을 사용하는 방법을 알아보려면 이 문서 를 참조하십시오 [규칙](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>이 확장 및 설명서 페이지는 다음 방법으로 유지 관리됩니다. [!DNL The Trade Desk] 팀. 문의 사항이나 업데이트 요청은 해당 업체에 직접 문의하시기 바랍니다.

## 전제 조건 {#prerequisites}

관련 광고주 ID, UPixel ID 및 추적기 ID가 있어야 합니다. [!DNL The Trade Desk] 계정 을(를) 사용하여 [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>판매자인 경우 판매자 ID도 받아야 합니다.

## 설치 및 구성 [!DNL The Trade Desk] 실시간 전환 API {#install}

확장을 설치하려면 [이벤트 전달 속성 만들기](../../../ui/event-forwarding/overview.md#properties) 또는 편집할 기존 속성을 선택합니다.

선택 **[!UICONTROL 확장]** 왼쪽 탐색. 다음에서 **[!UICONTROL 카탈로그]** 탭에서 **[!UICONTROL 트레이드 데스크]** 실시간 전환 API 카드를 선택한 다음 를 선택합니다. **[!UICONTROL 설치]**.

![다음을 표시하는 확장 카탈로그 [!DNL The Trade Desk] 확장 카드 강조 표시 설치.](../../../images/extensions/server/tradedesk/install-extension.png)

다음 화면에서 다음을 입력합니다. [!UICONTROL 광고주 ID], 및 선택적으로 [!UICONTROL 판매자 ID]. ID의 를 이러한 입력에 직접 붙여넣거나 데이터 요소를 대신 사용할 수 있습니다. 이 값은에 대한 이벤트 호출을 만들 때 사용되는 기본값 역할을 합니다. [!DNL The Trade Desk] 실시간 전환 API. 선택 **[!UICONTROL 저장]** 완료 시.

데이터 요소를 만들어 태그 속성의 확장에 사용할 수 있도록 하는 방법에 대해 알아보려면 다음을 따르십시오. [데이터 요소 만들기](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) 튜토리얼.

![다음 [!DNL The Trade Desk] 확장 구성 페이지 [!UICONTROL 광고주 ID] 및 [!UICONTROL 판매자 ID] 강조 표시된 필드입니다.](../../../images/extensions/server/tradedesk/configure-extension.png)

확장이 설치되었으며 이제 이벤트 전달 규칙에 해당 기능을 사용할 수 있습니다.

## 이벤트 전달 규칙 구성 {#rule}

확장을 설치하고 구성했으면 이벤트를 보내는 방법과 시기를 결정하는 이벤트 전달 규칙 만들기를 시작할 수 있습니다 [!DNL The Trade Desk].

수락된 모든 파일을 보내려면 여러 규칙을 구성하는 것이 좋습니다 [요청 속성](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) 경유 [!DNL The Trade Desk] 및 [!DNL The Trade Desk] 실시간 전환 API.

>[!NOTE]
>
>실시간으로 또는 가능한 한 실시간에 가깝게 이벤트를 전송해야 합니다.

새 이벤트 전달 만들기 [규칙](../../../ui/managing-resources/rules.md) 이벤트 전달 속성에서 다음을 수행합니다. 아래 **[!UICONTROL 작업]**, 새 작업을 추가하고 확장을 로 설정합니다. **[!UICONTROL 트레이드 데스크]**. 그런 다음 을 선택합니다. **[!UICONTROL 실시간 전환]** 대상: **[!UICONTROL 작업 유형]**.

![이벤트 전달 규칙 작업 구성을 추가하는 데 필요한 필드가 강조 표시된 이벤트 전달 속성 규칙 보기.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

선택 후 전송할 이벤트 데이터를 추가로 구성하기 위한 추가 제어 기능이 나타납니다. [!DNL The Trade Desk]. 선택 **[!UICONTROL 변경 내용 유지]** 을 눌러 규칙을 저장합니다.

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
| 노출 | 이벤트가 기여하는 노출에 대한 고유 ID 역할을 하는 36자 문자열(대시 포함). |
| 주문 ID | 이벤트의 관련 주문 식별자. |
| td1-td10 | 추가 전환 메타데이터를 제공하는 데 사용할 수 있는 10개의 순차적으로 번호가 매겨진 사용자 지정 동적 속성입니다. |

{style="table-layout:auto"}

![다음 [!DNL Basic Request Properties] 필드로의 데이터 입력 예를 보여 주는 섹션입니다.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

다음을 참조하십시오. [!DNL The Trade Desk] 개발자 설명서 를 참조하십시오. [요청 속성](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) 수락한 사람 [!DNL The Trade Desk] 실시간 전환 API.

**[!UICONTROL 개체 요청 매개 변수]**

항목, 개인 정보 보호 및 데이터 처리와 같은 JSON 형식의 요청 매개 변수에 대해 알아보려면 다음 섹션을 참조하십시오.

![다음 [!DNL Object Request Parameters] 사용 가능한 필드를 보여주는 섹션입니다.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

다음을 참조하십시오. [실시간 전환 이벤트](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) 에 대한 자세한 내용은 설명서 를 참조하십시오. [!UICONTROL 개체 요청 매개 변수] 및 해당 속성입니다.

**[!UICONTROL 구성 재정의]**

>참고
>
>다음 [!UICONTROL 구성 재정의] 필드를 사용하면 다른 필드를 설정할 수 있습니다 [!DNL Advertiser ID] 및/또는 [!DNL Merchant ID] 모든 규칙에서.

| 입력 | 설명 |
| --- | --- |
| 광고주 ID | 확장 구성에 제공된 광고주 ID를 재정의하려는 광고주 ID입니다. |
| 판매자 ID | 확장 구성에서 제공한 판매자 ID를 재정의하려는 판매자 ID입니다. |

![다음 [!DNL Configuration Overrides] 사용 가능한 필드를 보여주는 섹션입니다.](../../../images/extensions/server/tradedesk/configure-overrides.png)

규칙에 만족하면 다음을 선택합니다. **[!UICONTROL 라이브러리에 저장]**. 마지막으로 새 이벤트 전달을 게시합니다. [빌드](../../../ui/publishing/builds.md) 라이브러리에 대한 변경 사항을 활성화합니다.

## 다음 단계

이 안내서에서는 서버측 이벤트 데이터를에 보내는 방법을 다룹니다. [!DNL The Trade Desk] 사용 [!DNL The Trade Desk] 실시간 전환 API 확장. 여기에서는 캠페인에 따라 적용할 수 있는 특정 전환 이벤트를 보내는 고유한 규칙을 만들어 통합을 확장하는 것이 좋습니다. 의 이벤트 전달 기능에 대한 자세한 내용 [!DNL Adobe Experience Platform], 다음을 읽습니다 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).

다음을 참조하십시오. [!DNL The Trade Desk] 설명서 [에 대한 우수 사례 [!DNL The Trade Desk] 실시간 전환 API](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 를 참조하십시오.

Experience Platform 디버거 및 이벤트 전달 모니터링 도구를 사용하여 구현을 디버깅하는 방법에 대한 자세한 내용은 [Adobe Experience Platform Debugger 개요](../../../../debugger/home.md) 및 [이벤트 전달 시 활동 모니터링](../../../ui/event-forwarding/monitoring.md).
