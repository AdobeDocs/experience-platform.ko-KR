---
title: 메타 전환 API 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 메타 전환 API 확장에 대해 알아봅니다.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 확장 개요

다음 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 에 서버측 마케팅 데이터를 연결할 수 있습니다. [!DNL Meta] 광고 타겟팅을 최적화하고, 작업 당 비용을 절감하고, 결과를 측정하기 위한 기술. 이벤트는 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID 및 는 클라이언트측 이벤트와 유사한 방식으로 처리됩니다.

사용 [!DNL Meta Conversions API] 확장 프로그램에서 API 기능을 활용할 수 있습니다 [이벤트 전달](../../../ui/event-forwarding/overview.md) 데이터를 로 보내는 규칙 [!DNL Meta] Adobe Experience Platform Edge Network에서 지원됩니다. 이 문서에서는 이벤트 전달에서 확장을 설치하고 기능을 사용하는 방법을 설명합니다 [규칙](../../../ui/managing-resources/rules.md).

## 전제 조건

을 사용하는 것이 좋습니다 [!DNL Meta Pixel] 그리고 [!DNL Conversions API] 동일한 이벤트를 클라이언트 측과 서버 측에서 각각 공유 및 전송하려면 이 방법에서 선택하지 않은 이벤트를 복구하는 데 도움이 됩니다 [!DNL Meta Pixel]. 설치하기 전에 [!DNL Conversions API] 확장의 경우 [[!DNL Meta Pixel] 확장](../../client/meta/overview.md) 를 클라이언트측 태그 구현에 통합하는 방법에 대한 단계입니다.

>[!NOTE]
>
>의 섹션 [이벤트 중복 제거](#deduplication) 이 문서의 뒷부분에서 동일한 이벤트가 브라우저와 서버 모두에서 수신될 수 있으므로 동일한 이벤트가 두 번 사용되지 않도록 하는 단계를 다룹니다.

를 사용하려면 [!DNL Conversions API] 확장, 이벤트 전달에 대한 액세스 권한이 있고 유효한 가 있어야 합니다. [!DNL Meta] 액세스 권한이 있는 계정 [!DNL Ad Manager] 및 [!DNL Event Manager]. 특히 기존 ID를 복사해야 합니다 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) 또는 [새로 만들기 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) 대신)로 확장 프로그램을 사용자 계정에 구성할 수 있습니다.

## 확장 설치

를 설치하려면 [!DNL Meta Conversions API] 확장, 데이터 수집 UI 또는 Experience Platform UI로 이동하고 다음을 선택합니다 **[!UICONTROL 이벤트 전달]** 왼쪽 탐색에서 를 클릭합니다. 여기에서 확장을 추가할 속성을 선택하거나 대신 새 속성을 만듭니다.

원하는 속성을 선택하거나 만들었으면 을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색에서 **[!UICONTROL 카탈로그]** 탭. 을 검색합니다. [!UICONTROL 메타 전환 API] 카드를 선택한 다음 **[!UICONTROL 설치]**.

![다음 [!UICONTROL 설치] 버튼 선택 중 [!UICONTROL 메타 전환 API] 확장)을 클릭하여 제품에서 사용할 수 있습니다.](../../../images/extensions/server/meta/install.png)

표시되는 구성 보기에서 다음을 제공해야 합니다 [!DNL Pixel] 확장을 계정에 연결하기 위해 이전에 복사한 ID입니다. ID를 입력에 직접 붙여넣거나 데이터 요소를 대신 사용할 수 있습니다.

또한 액세스 토큰을 제공하여 [!DNL Conversions API] 특히, 자세한 내용은 [!DNL Conversions API] 설명서 [액세스 토큰 생성](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 을 참조하십시오.

완료되면 을 선택합니다 **[!UICONTROL 저장]**

![다음 [!DNL Pixel] 확장 구성 보기에서 데이터 요소로 제공된 ID입니다.](../../../images/extensions/server/meta/configure.png)

확장이 설치되었으며 이제 이벤트 전달 규칙에서 해당 기능을 사용할 수 있습니다.

## 이벤트 전달 규칙 구성 {#rule}

이 섹션에서는 [!DNL Conversions API] 일반 이벤트 전달 규칙의 확장입니다. 실제로 수락된 모든 항목을 전송하려면 여러 규칙을 구성해야 합니다 [표준 이벤트](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] 및 [!DNL Conversions API].

>[!NOTE]
>
>이벤트는 다음과 같습니다. [실시간으로 전송](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 또는 가능한 한 실시간으로 보다 나은 광고 캠페인 최적화를 위해 사용할 수 있습니다.

새 이벤트 전달 규칙 만들기를 시작하고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 **[!UICONTROL 메타 전환 API 확장]** 확장을 위해 를 선택한 다음 **[!UICONTROL 전환 API 이벤트 보내기]** 를 사용 중입니다.

![다음 [!UICONTROL 페이지 보기 보내기] 데이터 수집 UI에서 규칙에 대해 선택되는 작업 유형입니다.](../../../images/extensions/server/meta/select-action.png)

전송할 이벤트 데이터를 구성할 수 있는 컨트롤이 나타납니다 [!DNL Meta] 사용 [!DNL Conversions API]. 이러한 옵션을 제공된 입력에 직접 입력하거나 기존 데이터 요소를 선택하여 값을 대신 표시할 수 있습니다. 구성 옵션은 아래에 설명된 대로 네 개의 기본 섹션으로 나누어져 있습니다.

| 구성 섹션 | 설명 |
| --- | --- |
| [!UICONTROL 서버 이벤트 매개 변수] | 발생한 시간 및 이벤트를 트리거한 소스 작업을 포함하여 이벤트에 대한 일반 정보입니다. 자세한 내용은 [!DNL Meta] 개발자 설명서 를 참조하십시오. [표준 이벤트 매개 변수](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 수락함 [!DNL Conversions API].<br><br>두 가지 모두를 사용하는 경우 [!DNL Meta Pixel] 그리고 [!DNL Conversions API] 이벤트를 보내려면 두 이벤트를 모두 포함해야 합니다 **[!UICONTROL 이벤트 이름]** (`event_name`) 및 **[!UICONTROL 이벤트 ID]** (`event_id`)에 사용할 수 있습니다. [이벤트 중복 제거](#deduplication).<br><br>다음 작업도 수행할 수 있습니다 **[!UICONTROL 제한된 데이터 사용 활성화]** 고객 옵트아웃을 준수하기 위해 자세한 내용은 [!DNL Conversions API] 설명서 [데이터 처리 옵션](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 이 기능에 대한 자세한 내용은 |
| [!UICONTROL 고객 정보 매개 변수] | 이벤트를 고객에 지정하는 데 사용되는 사용자 ID 데이터입니다. 이러한 값 중 일부는 API로 전송되기 전에 해시해야 합니다.<br><br>일반적인 API 연결과 높은 이벤트 일치 품질(EMQ)을 보장하려면 모두 보내는 것이 좋습니다 [허용된 고객 정보 매개 변수](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 함께 사용할 수도 있습니다. 이러한 매개 변수도 [EMQ에 미치는 영향과 중요도에 따라 우선 순위가 지정됩니다.](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL 사용자 지정 데이터] | JSON 개체 형태로 제공되는 광고 게재 최적화에 사용할 추가 데이터입니다. 자세한 내용은 [[!DNL Conversions API] 설명서](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) 를 참조하십시오.<br><br>구매 이벤트를 전송하는 경우 이 섹션을 사용하여 필수 속성을 제공해야 합니다 `currency` 및 `value`. |
| [!UICONTROL 테스트 이벤트] | 이 옵션은 구성으로 인해 서버 이벤트를 수신하는지 여부를 확인하는 데 사용됩니다 [!DNL Meta] 예상대로요 이 기능을 사용하려면 **[!UICONTROL 테스트 이벤트로 보내기]** 확인란을 선택한 다음 아래 입력에 원하는 테스트 이벤트 코드를 제공합니다. 이벤트 전달 규칙이 배포되면 확장 및 작업을 올바르게 구성한 경우 페이지에 표시되는 활동이 표시됩니다 **[!DNL Test Events]** 에서 보기 [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

완료되면 을 선택합니다 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다.

![[!UICONTROL 변경 내용 유지] 작업 구성에 대해 선택되고 있습니다.](../../../images/extensions/server/meta/keep-changes.png)

규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**. 마지막으로 새 이벤트 전달 게시 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 이벤트 중복 제거 {#deduplication}

다음에서 언급했듯이 [사전 요구 사항 섹션](#prerequisites)를 설정하는 것이 좋습니다 [!DNL Meta Pixel] 태그 확장 및 [!DNL Conversions API] 이벤트 전달 확장 을 사용하여 중복 설정에서 클라이언트와 서버에서 동일한 이벤트를 전송할 수 있습니다. 이렇게 하면 한 확장이나 다른 확장에서 선택하지 않은 이벤트를 복구할 수 있습니다.

클라이언트와 서버에서 서로 다른 이벤트 유형을 두 이벤트 간에 겹치지 않고 전송하는 경우 중복 제거가 필요하지 않습니다. 그러나 하나의 이벤트가 두 이벤트 모두에서 공유되는 경우 [!DNL Meta Pixel] 그리고 [!DNL Conversions API]를 채울 때는 이러한 중복 이벤트가 중복 제거되어 보고에 부정적인 영향을 주지 않는지 확인해야 합니다.

공유 이벤트를 보낼 때 클라이언트와 서버 모두에서 보내는 모든 이벤트에 이벤트 ID와 이름을 포함하는지 확인합니다. ID와 이름이 동일한 여러 이벤트를 수신하면, [!DNL Meta] 는 자동으로 몇 가지 전략을 사용하여 이러한 전략을 제거하고 가장 관련 있는 데이터를 유지합니다. 자세한 내용은 [!DNL Meta] 설명서 [중복 제거 [!DNL Meta Pixel] 및 [!DNL Conversions API] events](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 자세한 내용은 이 프로세스를 참조하십시오.

## 다음 단계

이 안내서에서는 서버측 이벤트 데이터를 로 전송하는 방법을 다룹니다 [!DNL Meta] 사용 [!DNL Meta Conversions API] 확장. 여기에서 더 자세히 연결하여 통합을 확장하는 것이 좋습니다 [!DNL Pixels] 해당되는 경우 더 많은 이벤트를 공유할 수 있습니다. 다음 중 하나를 수행하면 광고 성능을 더 향상시키는 데 도움이 될 수 있습니다.

* 다른 항목 연결 [!DNL Pixels] 아직 [!DNL Conversions API] 통합.
* 특정 이벤트를 [!DNL Meta Pixel] 클라이언트측에서 이러한 동일한 이벤트를 [!DNL Conversions API] 서버측에서도 가능합니다.

자세한 내용은 [!DNL Meta] 설명서 [에 대한 우수 사례 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 를 참조하십시오. Adobe Experience Cloud의 태그 및 이벤트 전달에 대한 일반적인 정보는 [태그 개요](../../../home.md).
