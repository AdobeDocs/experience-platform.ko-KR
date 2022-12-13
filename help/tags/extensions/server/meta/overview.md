---
title: 메타 전환 API 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 메타 전환 API 확장에 대해 알아봅니다.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 확장 개요

다음 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 에 서버측 마케팅 데이터를 연결할 수 있습니다. [!DNL Meta] 광고 타겟팅을 최적화하고, 작업 당 비용을 절감하고, 결과를 측정하기 위한 기술. 이벤트는 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID 및 는 클라이언트측 이벤트와 유사한 방식으로 처리됩니다.

사용 [!DNL Meta Conversions API] 확장 프로그램에서 API 기능을 활용할 수 있습니다 [이벤트 전달](../../../ui/event-forwarding/overview.md) 데이터를 로 보내는 규칙 [!DNL Meta] Adobe Experience Platform Edge Network에서 지원됩니다. 이 문서에서는 이벤트 전달에서 확장을 설치하고 기능을 사용하는 방법을 설명합니다 [규칙](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>이벤트를 [!DNL Meta] 서버 쪽이 아니라 클라이언트 측에서 [[!DNL Meta Pixiel] 태그 확장](../../client/meta/overview.md) 을 가리키도록 업데이트하는 것이 좋습니다.

## 전제 조건

확장을 사용하려면 이벤트 전달에 액세스하고 유효한 가 있어야 합니다 [!DNL Meta] 액세스 권한이 있는 계정 [!DNL Ad Manager] 및 [!DNL Event Manager]. 특히 기존 ID를 복사해야 합니다 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) 또는 [새로 만들기 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) 대신)로 확장 프로그램을 사용자 계정에 구성할 수 있습니다.

## 확장 설치

를 설치하려면 [!DNL Meta Conversions API] 확장, 데이터 수집 UI 또는 Experience Platform UI로 이동하고 다음을 선택합니다 **[!UICONTROL 이벤트 전달]** 왼쪽 탐색에서 를 클릭합니다. 여기에서 확장을 추가할 속성을 선택하거나 대신 새 속성을 만듭니다.

원하는 속성을 선택하거나 만들었으면 을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색에서 **[!UICONTROL 카탈로그]** 탭. 을 검색합니다. [!UICONTROL 메타 전환 API] 카드를 선택한 다음 **[!UICONTROL 설치]**.

![다음 [!UICONTROL 설치] 버튼 선택 중 [!UICONTROL 메타 전환 API] 확장)을 클릭하여 제품에서 사용할 수 있습니다.](../../../images/extensions/server/meta/install.png)

표시되는 구성 보기에서 다음을 제공해야 합니다 [!DNL Pixel] 확장을 계정에 연결하기 위해 이전에 복사한 ID입니다. ID를 입력에 직접 붙여넣거나 데이터 요소를 대신 사용할 수 있습니다.

또한 액세스 토큰을 제공하여 [!DNL Conversions API] 특히, 자세한 내용은 [!DNL Conversions API] 설명서 [액세스 토큰 생성](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 을 참조하십시오.

완료되면 을 선택합니다 **[!UICONTROL 저장]**

![다음 [!DNL Pixel] 확장 구성 보기에서 데이터 요소로 제공된 ID입니다.](../../../images/extensions/server/meta/configure.png)

확장이 설치되었으며 이제 태그 규칙에서 해당 기능을 사용할 수 있습니다.

## 이벤트 전달 규칙 구성 {#rule}

새 이벤트 전달 규칙 만들기를 시작하고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 **[!UICONTROL 메타 전환 API 확장]** 확장을 위해 를 선택한 다음 **[!UICONTROL 전환 API 이벤트 보내기]** 를 사용 중입니다.

![다음 [!UICONTROL 페이지 보기 보내기] 데이터 수집 UI에서 규칙에 대해 선택되는 작업 유형입니다.](../../../images/extensions/server/meta/select-action.png)

전송할 이벤트 데이터를 구성할 수 있는 컨트롤이 나타납니다 [!DNL Meta] 사용 [!DNL Conversions API]. 이러한 옵션을 제공된 입력에 직접 입력하거나 기존 데이터 요소를 선택하여 값을 대신 표시할 수 있습니다. 구성 옵션은 아래에 설명된 대로 네 개의 기본 섹션으로 나누어져 있습니다.

| 구성 섹션 | 설명 |
| --- | --- |
| [!UICONTROL 서버 이벤트 매개 변수] | 발생한 시간 및 이벤트를 트리거한 소스 작업을 포함하여 이벤트에 대한 일반 정보입니다. 자세한 내용은 [[!DNL Conversions API] 설명서](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 를 참조하십시오.<br><br>다음 작업도 수행할 수 있습니다 **[!UICONTROL 제한된 데이터 사용 활성화]** 고객 옵트아웃을 준수하기 위해 자세한 내용은 [!DNL Conversions API] 설명서 [데이터 처리 옵션](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 이 기능에 대한 자세한 내용은 |
| [!UICONTROL 고객 정보 매개 변수] | 이벤트를 고객에 지정하는 데 사용되는 사용자 ID 데이터입니다. 이러한 값 중 일부는 API로 전송되기 전에 해시해야 합니다. 자세한 내용은 [[!DNL Conversions API] 설명서](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 를 참조하십시오. |
| [!UICONTROL 사용자 지정 데이터] | JSON 개체 형태로 제공되는 광고 게재 최적화에 사용할 추가 데이터입니다. 자세한 내용은 [[!DNL Conversions API] 설명서](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) 를 참조하십시오.<br><br>구매 이벤트를 전송하는 경우 이 섹션을 사용하여 필수 속성을 제공해야 합니다 `currency` 및 `value`. |
| [!UICONTROL 테스트 이벤트] | 이 옵션은 구성으로 인해 서버 이벤트를 수신하는지 여부를 확인하는 데 사용됩니다 [!DNL Meta] 예상대로요 이 기능을 사용하려면 **[!UICONTROL 테스트 이벤트로 보내기]** 확인란을 선택한 다음 아래 입력에 원하는 테스트 이벤트 코드를 제공합니다. 이벤트 전달 규칙이 배포되면 확장 및 작업을 올바르게 구성한 경우 페이지에 표시되는 활동이 표시됩니다 **[!DNL Test Events]** 에서 보기 [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

완료되면 을 선택합니다 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다.

![[!UICONTROL 변경 내용 유지] 작업 구성에 대해 선택되고 있습니다.](../../../images/extensions/server/meta/keep-changes.png)

규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**. 마지막으로 새 이벤트 전달 게시 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 다음 단계

이 안내서에서는 서버측 이벤트 데이터를 로 전송하는 방법을 다룹니다 [!DNL Meta] 사용 [!DNL Meta Conversions API] 확장. 태그 및 이벤트 전달에 대한 자세한 내용은 [태그 개요](../../../home.md).
