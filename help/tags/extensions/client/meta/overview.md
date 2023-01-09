---
title: 메타 픽셀 확장 개요
description: Adobe Experience Platform의 메타 픽셀 태그 확장에 대해 알아봅니다.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] 확장 개요

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) 는 웹 사이트에서 방문자 활동을 추적할 수 있는 JavaScript 기반 분석 도구입니다. 추적한 방문자 작업(전환이라고 함)은으로 전송됩니다 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) 광고, 캠페인, 전환 단계 등의 효과를 측정하는 데 사용할 수 있는 위치입니다.

다음 [!DNL Meta Pixel] 태그 확장을 사용하면 [!DNL Pixel] 기능이 포함되어 있습니다. 이 문서에서는 확장을 설치하고 [규칙](../../../ui/managing-resources/rules.md).

## 전제 조건

확장을 사용하려면 유효한 [!DNL Meta] 액세스 권한이 있는 계정 [!DNL Ads Manager]. 특히 다음을 수행해야 합니다 [새로 만들기 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) 및 [!DNL Pixel ID] 따라서 확장을 계정에 구성할 수 있습니다. 이미 존재하는 경우 [!DNL Meta Pixel]대신 해당 ID를 사용할 수 있습니다.

을 사용하는 것이 좋습니다 [!DNL Meta Pixel] 와 함께 [!DNL Meta Conversions API] 동일한 이벤트를 클라이언트 측과 서버 측에서 각각 공유 및 전송하려면 이 방법에서 선택하지 않은 이벤트를 복구하는 데 도움이 됩니다 [!DNL Meta Pixel]. 의 안내서를 참조하십시오. [[!DNL Meta Conversions API] 이벤트 전달을 위한 확장](../../client/meta/overview.md) 를 서버측 구현에 통합하는 방법에 대한 단계입니다. 조직은 [이벤트 전달](../../../ui/event-forwarding/overview.md) 서버측 확장을 사용하기 위해.

## 확장 설치

를 설치하려면 [!DNL Meta Pixel] 확장, 데이터 수집 UI 또는 Experience Platform UI로 이동하고 다음을 선택합니다 **[!UICONTROL 태그]** 왼쪽 탐색에서 를 클릭합니다. 여기에서 확장을 추가할 속성을 선택하거나 대신 새 속성을 만듭니다.

원하는 속성을 선택하거나 만들었으면 을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색에서 **[!UICONTROL 카탈로그]** 탭. 을 검색합니다. [!UICONTROL 메타 픽셀] 카드를 선택한 다음 **[!UICONTROL 설치]**.

![다음 [!UICONTROL 설치] 버튼 선택 중 [!UICONTROL 메타 픽셀] 확장)을 클릭하여 제품에서 사용할 수 있습니다.](../../../images/extensions/client/meta/install.png)

표시되는 구성 보기에서 다음을 제공해야 합니다 [!DNL Pixel] 확장을 계정에 연결하기 위해 이전에 복사한 ID입니다. ID를 입력에 직접 붙여넣거나 기존 데이터 요소를 대신 선택할 수 있습니다.

>[!TIP]
>
>데이터 요소를 사용하면 동적으로 변경할 수 있는 옵션이 제공됩니다 [!DNL Pixel] 빌드 환경과 같은 다른 요소에 따라 사용되는 ID입니다. 의 부록 섹션을 참조하십시오. [다른 사용 [!DNL Pixel] 다른 환경을 위한 ID](#id-data-element) 추가 정보.

원할 경우 확장과 연결할 이벤트 ID를 제공할 수도 있습니다. 이 변수는 두 이벤트 간에 동일한 이벤트를 중복 제거하는 데 사용됩니다 [!DNL Meta Pixel] 그리고 [!DNL Meta Conversions API]. 자세한 내용은 [이벤트 중복 제거](../../server/meta/overview.md#event-deduplication) 개요 [!DNL Conversions API] 확장.

완료되면 을 선택합니다 **[!UICONTROL 저장]**

![다음 [!DNL Pixel] 확장 구성 보기에서 데이터 요소로 제공된 ID입니다.](../../../images/extensions/client/meta/configure.png)

확장이 설치되었으며 이제 태그 규칙에서 다양한 작업을 사용할 수 있습니다.

## 태그 규칙 구성 {#rule}

[!DNL Meta Pixel] 는 사전 정의된 일련의 를 허용합니다 [표준 이벤트](https://www.facebook.com/business/help/402791146561655)각각 컨텍스트 및 허용된 속성을 보유한 URL입니다. 에서 제공하는 규칙 작업 [!DNL Pixel] 확장은 이러한 이벤트 유형과 관련이 있으므로 로 전송되는 이벤트를 쉽게 분류하고 구성할 수 있습니다 [!DNL Meta] 유형에 따라 다릅니다.

데모 목적으로 이 섹션에서는 페이지 보기 이벤트를 보내는 규칙을 만드는 방법을 보여줍니다 [!DNL Meta].

새 태그 규칙 만들기를 시작하고 원하는 대로 해당 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 **[!UICONTROL 메타 픽셀]** 확장을 위해 를 선택한 다음 **[!UICONTROL 페이지 보기 보내기]** 를 사용 중입니다.

![다음 [!UICONTROL 페이지 보기 보내기] 데이터 수집 UI에서 규칙에 대해 선택되는 작업 유형입니다.](../../../images/extensions/client/meta/select-action.png)

에 더 이상 구성이 필요하지 않습니다 [!UICONTROL 페이지 보기 보내기] 작업. 선택 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다. 규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**.

마지막으로 새 태그를 게시합니다 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 확인 [!DNL Meta] 데이터를 수신하고 있습니다.

업데이트된 빌드가 웹 사이트에 배포되면 브라우저에서 일부 전환 이벤트를 생성하고 해당 이벤트가 웹 사이트에 표시되는지 확인함으로써 데이터가 예상대로 전송되는지 확인할 수 있습니다. [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## 다음 단계

이 안내서에서는 로 데이터를 전송하는 방법을 다룹니다 [!DNL Meta] 사용 [!DNL Meta Pixel] 태그 확장. 서버측 이벤트도 [!DNL Meta]를 눌러 설치 및 구성 작업을 진행할 수 있습니다. [[!DNL Conversions API] 이벤트 전달 확장](../../server/meta/overview.md).

Experience Platform의 태그에 대한 자세한 내용은 [태그 개요](../../../home.md).

## 부록: 다른 항목 사용 [!DNL Pixel] 다른 환경을 위한 ID {#id-data-element}

프로덕션 상태를 유지하면서 개발 또는 스테이징 환경에서 구현을 테스트하려는 경우 [!DNL Meta Pixel] analytics가 손상되지 않은 경우 데이터 요소를 사용하여 적절하게 [!DNL Pixel] 사용 중인 환경에 따른 ID.

다음을 사용하여 이 작업을 수행할 수 있습니다 [!UICONTROL 사용자 지정 코드] 데이터 요소(에서 제공) [[!UICONTROL 코어] 확장](../core/overview.md))을 조합하여 사용할 수 있습니다 [`turbine` 자유 변수](../../../extension-dev/turbine.md). 데이터 요소의 JavaScript 코드에서 `turbine` 개체를 사용하여 현재 환경 스테이지를 찾은 다음 적절한 [!DNL Pixel] 결과 기반 ID.

다음 예는 가짜 프로덕션 ID를 반환합니다 `exampleProductionKey` 프로덕션 환경에서 사용하는 경우 및 다른 ID에서 사용할 수 없습니다 `exampleTestKey` 를 설정하는 것이 좋습니다. 이 코드를 구현할 때 각 값을 실제 프로덕션 및 테스트로 바꿉니다 [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
