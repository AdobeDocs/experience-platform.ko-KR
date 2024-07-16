---
title: 메타 픽셀 확장 개요
description: Adobe Experience Platform의 메타 픽셀 태그 확장에 대해 알아봅니다.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# [!DNL Meta Pixel] 확장 개요

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/)은(는) 웹 사이트에서 방문자 활동을 추적할 수 있는 JavaScript 기반 분석 도구입니다. 추적하는 방문자 작업(전환이라고 함)은 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager)(으)로 전송되며, 여기서 광고, 캠페인, 전환 단계 등의 효과를 측정하는 데 사용할 수 있습니다.

[!DNL Meta Pixel] 태그 확장을 사용하면 클라이언트측 태그 라이브러리에서 [!DNL Pixel] 기능을 활용할 수 있습니다. 이 문서에서는 [규칙](../../../ui/managing-resources/rules.md)에서 확장을 설치하고 기능을 사용하는 방법을 다룹니다.

## 전제 조건

확장을 사용하려면 [!DNL Ads Manager]에 대한 액세스 권한이 있는 올바른 [!DNL Meta] 계정이 있어야 합니다. 특히, 확장을 계정에 구성할 수 있도록 [새로 만들기 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755)하고 해당 [!DNL Pixel ID]을(를) 복사해야 합니다. 기존 [!DNL Meta Pixel]이(가) 이미 있는 경우 해당 ID를 대신 사용할 수 있습니다.

[!DNL Meta Pixel]을(를) [!DNL Meta Conversions API]과(와) 함께 사용하여 클라이언트측과 서버측에서 각각 동일한 이벤트를 공유하고 전송하는 것이 좋습니다. [!DNL Meta Pixel]에서 선택하지 않은 이벤트를 복구하는 데 도움이 될 수 있기 때문입니다. 서버측 구현에 통합하는 방법에 대한 단계는 [[!DNL Meta Conversions API] 이벤트 전달을 위한 확장](../../client/meta/overview.md)의 안내서를 참조하십시오. 서버측 확장을 사용하려면 조직에 [이벤트 전달](../../../ui/event-forwarding/overview.md)에 대한 액세스 권한이 있어야 합니다.

## 확장 설치

[!DNL Meta Pixel] 확장을 설치하려면 데이터 수집 UI 또는 Experience Platform UI로 이동한 다음 왼쪽 탐색에서 **[!UICONTROL 태그]**&#x200B;를 선택합니다. 여기에서 확장을 추가할 속성을 선택하거나 새 속성을 대신 만듭니다.

원하는 속성을 선택하거나 만든 후에는 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. [!UICONTROL 메타 픽셀] 카드를 검색한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![데이터 수집 UI에서 [!UICONTROL Meta Pixel] 확장에 대해 [!UICONTROL 설치] 단추가 선택되어 있습니다.](../../../images/extensions/client/meta/install.png)

표시되는 구성 보기에서 확장을 계정에 연결하려면 이전에 복사한 [!DNL Pixel] ID를 제공해야 합니다. ID를 입력에 직접 붙여넣거나 대신 기존 데이터 요소를 선택할 수 있습니다.

>[!TIP]
>
>데이터 요소를 사용하면 빌드 환경과 같은 다른 요소에 따라 사용되는 [!DNL Pixel] ID를 동적으로 변경할 수 있는 옵션이 제공됩니다. 자세한 내용은 [다른 환경에 대해 다른 ID 사용 [!DNL Pixel] 2}에 대한 부록 섹션을 참조하십시오.](#id-data-element)

선택적으로 확장과 연결할 이벤트 ID를 제공할 수도 있습니다. [!DNL Meta Pixel]과(와) [!DNL Meta Conversions API] 사이의 동일한 이벤트를 중복 제거하는 데 사용됩니다. 자세한 내용은 [!DNL Conversions API] 확장에 대한 개요에서 [이벤트 중복 제거](../../server/meta/overview.md#event-deduplication)에 대한 섹션을 참조하십시오.

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![확장 구성 보기에서 데이터 요소로 제공된 [!DNL Pixel] ID입니다.](../../../images/extensions/client/meta/configure.png)

확장이 설치되었으며 이제 태그 규칙에서 다양한 작업을 사용할 수 있습니다.

## 태그 규칙 구성 {#rule}

[!DNL Meta Pixel]은(는) 각각 고유한 컨텍스트와 허용되는 속성을 가진 미리 정의된 [표준 이벤트](https://www.facebook.com/business/help/402791146561655) 집합을 허용합니다. [!DNL Pixel] 확장에서 제공하는 규칙 작업은 이러한 이벤트 유형과 상호 관련되어 있으므로 해당 유형에 따라 [!DNL Meta]에 전송되는 이벤트를 쉽게 분류하고 구성할 수 있습니다.

이 섹션에서는 데모용으로 [!DNL Meta]에 페이지 보기 이벤트를 보내는 규칙을 만드는 방법을 보여줍니다.

새 태그 규칙 만들기를 시작하고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 확장에 대해 **[!UICONTROL 메타 픽셀]**&#x200B;을(를) 선택한 다음 작업 유형에 대해 **[!UICONTROL 페이지 보기 보내기]**&#x200B;를 선택합니다.

![데이터 수집 UI에서 규칙에 대해 [!UICONTROL 페이지 보기 보내기] 작업 유형을 선택하고 있습니다.](../../../images/extensions/client/meta/select-action.png)

[!UICONTROL 페이지 보기 보내기] 작업에 필요한 구성이 없습니다. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 규칙 구성에 작업을 추가합니다. 규칙에 만족하면 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다.

마지막으로 새 태그 [build](../../../ui/publishing/builds.md)을(를) 게시하여 라이브러리에 대한 변경 내용을 활성화하십시오.

## [!DNL Meta]이(가) 데이터를 받고 있는지 확인

업데이트된 빌드가 웹 사이트에 배포된 후 브라우저에서 일부 전환 이벤트를 생성하고 이러한 이벤트가 [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180)에 표시되는지 확인하여 데이터가 예상대로 전송되는지 여부를 확인할 수 있습니다.

## 다음 단계

이 안내서에서는 [!DNL Meta Pixel] 태그 확장을 사용하여 데이터를 [!DNL Meta]에 보내는 방법을 다룹니다. [!DNL Meta]에도 서버측 이벤트를 보낼 계획이라면 [[!DNL Conversions API] 이벤트 전달 확장](../../server/meta/overview.md)을 설치하고 구성할 수 있습니다.

Experience Platform의 태그에 대한 자세한 내용은 [태그 개요](../../../home.md)를 참조하세요.

## 부록: 다른 환경에 대해 다른 [!DNL Pixel] ID 사용 {#id-data-element}

프로덕션 [!DNL Meta Pixel] 분석을 그대로 유지하면서 개발 또는 스테이징 환경에서 구현을 테스트하려는 경우 데이터 요소를 사용하여 사용 중인 환경에 따라 적절한 [!DNL Pixel] ID를 동적으로 선택할 수 있습니다.

[`turbine` 사용 가능한 변수](../../../extension-dev/turbine.md)과(와) 함께 [!UICONTROL 사용자 지정 코드] 데이터 요소([[!UICONTROL Core] 확장](../core/overview.md)에서 제공)를 사용하여 이를 수행할 수 있습니다. 데이터 요소의 JavaScript 코드에서 `turbine` 개체를 사용하여 현재 환경 단계를 찾은 다음 결과에 따라 적절한 [!DNL Pixel] ID를 반환합니다.

다음 예제에서는 프로덕션 환경에서 사용할 경우 가짜 프로덕션 ID `exampleProductionKey`을(를) 반환하고 다른 환경을 사용할 경우 다른 ID `exampleTestKey`을(를) 반환합니다. 이 코드를 구현할 때 각 값을 실제 프로덕션으로 바꾸고 [!DNL Pixel] ID를 테스트하십시오.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
