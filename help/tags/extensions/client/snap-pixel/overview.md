---
title: 스냅 픽셀 확장 개요
description: 스냅 픽셀 태그 확장 기능을 사용하여 Adobe Experience Platform에서 중요한 사용자 상호 작용을 캡처하는 방법을 알아봅니다.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# [!DNL Snap Pixel] 확장 개요

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about)은(는) 웹 사이트에서 중요한 사용자 상호 작용을 캡처할 수 있는 JavaScript 기반 분석 도구입니다. 구매, 등록 또는 기타 전환과 같은 중요한 방문자 작업은 [광고 관리자](http://ads.snapchat.com/)에게 자동으로 전송되므로 광고, 캠페인, 전환 경로 등의 성능을 측정하고 최적화할 수 있습니다.

[!DNL Snap Pixel] 태그 확장을 사용하면 [!DNL Snap Pixel] 기능을 클라이언트측 태그 라이브러리에 직접 통합할 수 있습니다. 이 설명서에서는 태그 관리 규칙 내에서 확장을 설치하고 기능을 구현하는 방법을 간략하게 설명합니다.

[!DNL Snap Pixel] 태그 확장을 사용하면 [!DNL Snap Pixel] 기능을 기존 클라이언트측 태그 라이브러리에 효율적으로 통합할 수 있습니다. 이 설명서는 태그 관리 [규칙](../../../ui/managing-resources/rules.md) 내에서 확장을 설치하고 기능을 구성하는 방법에 대해 간략하게 설명합니다.

## 전제 조건 {#prerequisites}

확장을 사용하려면 [!DNL Snap]에 액세스할 수 있는 올바른 [!DNL Ads Manager] 계정이 필요합니다. 계정에 대한 확장을 구성하려면 [새로 만들기 [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about)와(과) 해당 Pixel ID를 복사해야 합니다. 기존 [!DNL Snap Pixel]이(가) 있는 경우 해당 ID를 사용하면 됩니다.

[!DNL Snap Pixel]을(를) [!DNL Snap Conversions API]과(와) 함께 사용하여 클라이언트측과 서버측에서 동일한 이벤트를 전송하는 것이 좋습니다. 이 방법을 사용하면 [!DNL Snap Pixel]에서만 캡처할 수 없는 이벤트를 복구하는 데 도움이 됩니다. 서버측 구현에 이를 통합하는 방법에 대한 단계는 [[!DNL Snap] 이벤트 전달을 위한 전환 API 확장](../../server/snap/overview.md)을 참조하세요. 서버측 확장을 사용하려면 조직에 [이벤트 전달](../../../ui/event-forwarding/overview.md)에 대한 액세스 권한이 있어야 합니다.

## 확장 설치 {#install}

[!DNL Snap Pixel] 확장을 설치하려면 데이터 수집 UI 또는 Experience Platform UI로 이동한 다음 왼쪽 탐색에서 **[!UICONTROL 태그]**&#x200B;를 선택합니다. 여기에서 확장을 추가할 속성을 선택하거나 새 속성을 대신 만듭니다.

원하는 속성을 선택하거나 만든 후에는 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. [!UICONTROL Snap Pixel] 카드를 검색한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![데이터 수집 UI에서 [!UICONTROL Snap Pixel] 확장에 대해 [!UICONTROL 설치] 단추가 선택되어 있습니다.](./images/install.png)

표시되는 구성 보기에서 확장을 계정에 연결하려면 이전에 복사한 픽셀 ID를 제공해야 합니다. ID를 입력에 직접 붙여넣거나 대신 기존 데이터 요소를 선택할 수 있습니다.

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![확장 구성 보기에서 데이터 요소로 제공된 [!DNL Pixel] ID입니다.](./images/configure.png)

확장이 설치되었으며 이제 태그 규칙에서 다양한 작업을 사용할 수 있습니다.

## 태그 규칙 구성 {#rule}

[!DNL Snap Pixel]은(는) 사전 정의된 표준 이벤트 집합을 지원하며 각 이벤트에는 특정 컨텍스트 및 허용되는 매개 변수가 있습니다. [!DNL Snap Pixel] 확장에서 사용할 수 있는 규칙 작업은 이러한 이벤트 유형에 맞게 조정되므로 해당 유형에 따라 [!DNL Snap]&#x200B;(으)로 전송되는 이벤트를 간단하게 분류하고 구성할 수 있습니다.

이 단원에서는 데모용으로 [!DNL Snap]에 구매 이벤트를 보내는 규칙을 만드는 방법을 보여 줍니다.

시작하려면 새 태그 규칙을 만들고 필요에 따라 조건을 정의합니다. 규칙의 작업을 설정할 때 확장으로 [!DNL Snap Pixel]을(를) 선택한 다음 작업 유형으로 **[!UICONTROL 구매 이벤트 보내기]**&#x200B;를 선택합니다.

[!UICONTROL 구매 이벤트 보내기] 작업 구성을 마치면 **[!UICONTROL 변경 유지]**&#x200B;를 선택하여 규칙 설정에 추가하십시오.

![데이터 수집 UI에서 규칙에 대해 [!UICONTROL 구매 이벤트 보내기] 작업 유형을 선택했습니다.](./images/action-type.png)

전체 규칙 구성에 만족하면 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다.

업데이트를 적용하려면 새 태그 [build](../../../ui/publishing/builds.md)를 게시하여 라이브러리에 대한 변경 내용을 활성화하십시오.

## [!DNL Snap]이(가) 데이터를 받고 있는지 확인 {#confirm}

업데이트된 빌드가 웹 사이트에 배포되면 브라우저에서 전환 이벤트를 트리거하고 [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager)에 표시되는지 확인하여 데이터가 예상대로 전송되는지 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이 안내서에서는 [!DNL Snap] 태그 확장을 사용하여 데이터를 [!DNL Snap Pixel]에 보내는 방법을 다룹니다. 서버측 이벤트도 [!DNL Snap]에 보낼 계획이라면 [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md)을(를) 설치 및 구성하십시오.
