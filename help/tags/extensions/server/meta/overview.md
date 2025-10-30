---
title: Meta 전환 API 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 Meta 전환 API 확장에 대해 알아봅니다.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 확장 개요

[[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/)을(를) 사용하면 광고 타깃팅을 최적화하고, 작업당 비용을 줄이고, 결과를 측정하기 위해 서버측 마케팅 데이터를 [!DNL Meta] 기술에 연결할 수 있습니다. 이벤트는 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID에 연결되어 있으며 클라이언트측 이벤트와 유사한 방식으로 처리됩니다.

[!DNL Meta Conversions API] 확장을 사용하면 [이벤트 전달](../../../ui/event-forwarding/overview.md) 규칙에서 API 기능을 활용하여 Adobe Experience Platform Edge Network에서 [!DNL Meta]&#x200B;(으)로 데이터를 보낼 수 있습니다. 이 문서에서는 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)에서 확장을 설치하고 기능을 사용하는 방법을 다룹니다.

## 데모

다음 비디오는 [!DNL Meta Conversions API]에 대한 이해를 돕기 위한 것입니다.

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## 전제 조건

[!DNL Meta Pixel]에서 선택하지 않은 이벤트를 복구하는 데 도움이 될 수 있으므로 [!DNL Conversions API]과(와) [!DNL Meta Pixel]을(를) 사용하여 클라이언트측과 서버측에서 각각 동일한 이벤트를 공유하고 전송하는 것이 좋습니다. [!DNL Conversions API] 확장을 설치하기 전에 클라이언트측 태그 구현에 통합하는 방법에 대한 단계를 보려면 [[!DNL Meta Pixel] extension](../../client/meta/overview.md)의 안내서를 참조하십시오.

>[!NOTE]
>
>이 문서의 뒷부분에서 [이벤트 중복 제거](#deduplication)에 대한 섹션은 동일한 이벤트가 브라우저와 서버 모두에서 수신될 수 있으므로 두 번 사용되지 않도록 하는 단계를 다룹니다.

[!DNL Conversions API] 확장을 사용하려면 이벤트 전달에 대한 액세스 권한이 있어야 하며 [!DNL Meta] 및 [!DNL Ad Manager]에 대한 액세스 권한이 있는 올바른 [!DNL Event Manager] 계정이 있어야 합니다. 특히, 기존 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142)의 ID를 복사해야(또는 [새로 만들기 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) 대신) 계정에 확장을 구성할 수 있습니다.

>[!INFO]
>
>모바일 앱 데이터로 이 확장을 사용할 계획이거나 [!DNL Meta] 캠페인에서 오프라인 이벤트 데이터로도 작업하는 경우 기존 앱을 통해 데이터 세트를 만들고 메시지가 표시되면 **픽셀 ID에서 만들기**&#x200B;를 선택해야 합니다. 자세한 내용은 문서 [비즈니스에 적합한 데이터 세트 만들기 옵션 결정](https://www.facebook.com/business/help/5270377362999582?id=490360542427371)을 참조하십시오. 필수 및 선택적 앱 추적 매개 변수에 대한 모든 정보는 [앱 이벤트에 대한 전환 API](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) 문서를 참조하십시오.

## 확장 설치

[!DNL Meta Conversions API] 확장을 설치하려면 데이터 수집 UI 또는 Experience Platform UI로 이동한 다음 왼쪽 탐색에서 **[!UICONTROL Event Forwarding]**&#x200B;을(를) 선택합니다. 여기에서 확장을 추가할 속성을 선택하거나 새 속성을 대신 만듭니다.

원하는 속성을 선택하거나 만들었으면 왼쪽 탐색에서 **[!UICONTROL Extensions]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Catalog]** 탭을 선택합니다. [!UICONTROL Meta Conversions API] 카드를 검색한 다음 **[!UICONTROL Install]**&#x200B;을(를) 선택합니다.

![데이터 수집 UI에서 [!UICONTROL Install] 확장에 대해 [!UICONTROL Meta Conversions API] 옵션을 선택하고 있습니다.](../../../images/extensions/server/meta/install.png)

표시되는 구성 보기에서 확장을 계정에 연결하려면 이전에 복사한 [!DNL Pixel] ID를 제공해야 합니다. ID를 입력에 직접 붙여넣거나 데이터 요소를 대신 사용할 수 있습니다.

[!DNL Conversions API]을(를) 사용하려면 액세스 토큰도 제공해야 합니다. 이 값을 얻는 방법에 대한 단계는 [!DNL Conversions API]액세스 토큰 생성[에 대한 ](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 설명서를 참조하십시오.

완료되면 **[!UICONTROL Save]** 선택

![확장 구성 보기에서 데이터 요소로 제공된 [!DNL Pixel] ID입니다.](../../../images/extensions/server/meta/configure.png)

확장이 설치되었으며 이제 이벤트 전달 규칙에 해당 기능을 사용할 수 있습니다.

## Facebook 및 Instagram 확장 기능과 통합 {#facebook}

Facebook 및 Instagram 확장을 사용하는 통합을 사용하면 Meta 비즈니스 계정을 빠르게 인증할 수 있습니다. 그러면 [!UICONTROL Pixel ID] 및 Meta 전환 API [!UICONTROL Access Token]이(가) 자동으로 채워지므로 Meta 전환 API를 더 쉽게 설치하고 구성할 수 있습니다.

[!UICONTROL Meta Conversions API] 확장을 설치할 때 Facebook 및 Instagram에서 인증하라는 대화 상자가 나타납니다.

![설치 페이지 [!UICONTROL Meta Conversions API Extension]이(가) [!UICONTROL Connect to Meta]을(를) 강조 표시합니다.](../../../images/extensions/server/meta/mbe-extension-install.png)

Facebook 및 Instagram에서 인증하라는 대화 상자 프롬프트가 이벤트 전달 내 빠른 시작 워크플로우 UI에도 표시됩니다.

![빠른 시작 워크플로 UI가 [!UICONTROL Connect to Meta]을(를) 강조 표시합니다.](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## 이벤트 품질 일치 점수(EMQ)와 통합 {#emq}

이벤트 품질 일치 점수(EMQ)와 통합하면 EMQ 점수를 표시하여 구현의 효과를 쉽게 볼 수 있습니다. 이 통합은 컨텍스트 전환을 최소화하고 Meta 전환 API 구현의 성공을 개선하는 데 도움이 됩니다. 이러한 이벤트 점수는 [!UICONTROL Meta Conversions API extension] 구성 화면에 표시됩니다.

![[!UICONTROL Meta Conversions API Extension]을(를) 강조 표시하는 [!UICONTROL View EMQ Score] 구성 페이지입니다.](../../../images/extensions/server/meta/emq-score.png)

## LiveRamp와 통합(Alpha) {#alpha}

사이트에 [!DNL LiveRamp]의 ATS(인증된 트래픽 솔루션)를 배포한 [!DNL LiveRamp] 고객은 RampID를 고객 정보 매개 변수로 공유하도록 선택할 수 있습니다. 이 기능을 사용하려면 [!DNL Meta] 계정 팀과 함께 Alpha 프로그램에 참여하십시오.

![Meta 이벤트 전달 [!UICONTROL Rule] 구성 페이지에서 [!UICONTROL Partner Name (alpha)] 및 [!UICONTROL Partner ID (alpha)]을(를) 강조 표시합니다.](../../../images/extensions/server/meta/live-ramp.png)

## 이벤트 전달 규칙 구성 {#rule}

이 섹션에서는 일반 이벤트 전달 규칙에서 [!DNL Conversions API] 확장을 사용하는 방법을 다룹니다. 실제로 [ 및 ](https://developers.facebook.com/docs/meta-pixel/reference)을(를) 통해 허용된 모든 [!DNL Meta Pixel]표준 이벤트[!DNL Conversions API]를 보내려면 여러 규칙을 구성해야 합니다. 모바일 앱 데이터의 경우 필수 필드, 앱 데이터 필드, 고객 정보 매개 변수 및 사용자 지정 데이터 세부 정보 [여기](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events)를 참조하세요.

>[!NOTE]
>
>더 나은 광고 캠페인 최적화를 위해 이벤트는 [실시간으로 전송](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 또는 가능한 한 실시간에 가깝게 전송되어야 합니다.

새 이벤트 전달 규칙 만들기를 시작하고 원하는 대로 해당 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 확장에 대해 **[!UICONTROL Meta Conversions API Extension]**&#x200B;을(를) 선택한 다음 작업 유형에 대해 **[!UICONTROL Send Conversions API Event]**&#x200B;을(를) 선택합니다.

![데이터 수집 UI에서 규칙에 대해 [!UICONTROL Send Page View] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/meta/select-action.png)

[!DNL Meta]을(를) 통해 [!DNL Conversions API]&#x200B;(으)로 전송되는 이벤트 데이터를 구성할 수 있는 컨트롤이 나타납니다. 이러한 옵션은 제공된 입력에 직접 입력할 수도 있고, 대신 값을 나타낼 기존 데이터 요소를 선택할 수도 있습니다. 구성 옵션은 아래에 설명된 대로 4개의 기본 섹션으로 나뉘어 있습니다.

| 구성 섹션 | 설명 |
| --- | --- |
| [!UICONTROL Server Event Parameters] | 발생한 시간 및 이벤트를 트리거한 소스 작업을 포함한 이벤트에 대한 일반 정보입니다. [!DNL Meta]에서 수락한 [표준 이벤트 매개 변수](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event)에 대한 자세한 내용은 [!DNL Conversions API] 개발자 설명서를 참조하십시오.<br><br>이벤트를 보내는 데 [!DNL Meta Pixel]과(와) [!DNL Conversions API]을(를) 모두 사용하는 경우 모든 이벤트에 **[!UICONTROL Event Name]**(`event_name`)과(와) **[!UICONTROL Event ID]**(`event_id`)을(를) 모두 포함해야 합니다. [이벤트 중복 제거](#deduplication)에 이 값이 사용되기 때문입니다.<br><br>고객 옵트아웃을 준수하도록 **[!UICONTROL Enable Limited Data Use]**&#x200B;할 수 있는 옵션도 있습니다. 이 기능에 대한 자세한 내용은 [!DNL Conversions API]데이터 처리 옵션[에서 ](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 설명서를 참조하십시오. |
| [!UICONTROL Customer Information Parameters] | 이벤트를 고객에게 연결하는 데 사용되는 사용자 ID 데이터입니다. 이러한 값 중 일부는 API로 전송되기 전에 해시해야 합니다.<br><br>양호한 일반 API 연결과 높은 이벤트 일치 품질(EMQ)을 보장하려면 서버 이벤트와 함께 모든 [허용된 고객 정보 매개 변수](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters)를 보내는 것이 좋습니다. 이러한 매개 변수는 [중요도와 EMQ에 미치는 영향에 따라 우선 순위가 지정되어야 합니다](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Custom Data] | 광고 게재 최적화에 사용할 추가 데이터로서, JSON 오브젝트 형태로 제공됩니다. 이 개체에 대해 허용되는 속성에 대한 자세한 내용은 [[!DNL Conversions API] 설명서](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data)를 참조하세요.<br><br>구매 이벤트를 보내는 경우 이 섹션을 사용하여 필수 특성 `currency` 및 `value`을(를) 제공해야 합니다. |
| [!UICONTROL Test Event] | 이 옵션은 구성이 서버 이벤트를 예상대로 [!DNL Meta]에서 수신하는지 확인하는 데 사용됩니다. 이 기능을 사용하려면 **[!UICONTROL Send as Test Event]** 확인란을 선택한 다음 아래 입력에 원하는 테스트 이벤트 코드를 입력하십시오. 이벤트 전달 규칙이 배포되면 확장과 작업을 올바르게 구성한 경우 **[!DNL Test Events]**&#x200B;의 [!DNL Meta Events Manager] 보기 내에 나타나는 활동이 표시됩니다. |

{style="table-layout:auto"}

완료되면 **[!UICONTROL Keep Changes]**&#x200B;을(를) 선택하여 작업을 규칙 구성에 추가합니다.

작업 구성에 대해 ![[!UICONTROL Keep Changes]을(를) 선택하고 있습니다.](../../../images/extensions/server/meta/keep-changes.png)

규칙에 만족하면 **[!UICONTROL Save to Library]**&#x200B;을(를) 선택합니다. 마지막으로 새 이벤트 전달 [build](../../../ui/publishing/builds.md)을(를) 게시하여 라이브러리에 대한 변경 사항을 활성화하십시오.

## 이벤트 중복 제거 {#deduplication}

[필수 구성 요소 섹션](#prerequisites)에서 언급한 대로 [!DNL Meta Pixel] 태그 확장 및 [!DNL Conversions API] 이벤트 전달 확장 기능을 모두 사용하여 중복 설정에서 클라이언트와 서버에서 동일한 이벤트를 전송하는 것이 좋습니다. 이렇게 하면 한 확장이나 다른 확장에서 선택하지 않은 이벤트를 복구하는 데 도움이 될 수 있습니다.

클라이언트와 서버 간에 중복되지 않은 상태로 서로 다른 이벤트 유형을 보내는 경우 중복 제거가 필요하지 않습니다. 그러나 단일 이벤트가 [!DNL Meta Pixel]과(와) [!DNL Conversions API] 모두에서 공유되는 경우 이러한 중복 이벤트가 중복 제거되어 보고에 부정적인 영향을 주지 않도록 해야 합니다.

공유 이벤트를 보낼 때 클라이언트와 서버 모두에서 보내는 모든 이벤트와 함께 이벤트 ID와 이름을 포함해야 합니다. ID와 이름이 같은 여러 이벤트가 수신되면 [!DNL Meta]은(는) 자동으로 여러 전략을 사용하여 중복을 제거하고 가장 관련성이 높은 데이터를 유지합니다. 이 프로세스에 대한 자세한 내용은 [!DNL Meta]중복 제거 대상[및 [!DNL Meta Pixel] 이벤트 [!DNL Conversions API] 에 대한 ](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 설명서를 참조하십시오.

## 빠른 시작 워크플로우: Meta 전환 API 확장(Beta) {#quick-start}

>[!IMPORTANT]
>
>* 빠른 시작 기능은 Real-Time CDP Prime 및 Ultimate 패키지를 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.
>* 이 기능은 새로운 구현을 위한 것이며 현재 기존 태그 및 이벤트 전달 속성에 확장 및 구성을 자동으로 설치하는 것을 지원하지 않습니다.

>[!NOTE]
>
>기존 클라이언트는 빠른 시작 워크플로우를 사용하여 다음에 사용할 수 있는 참조 구현을 만들 수 있습니다.
>
>* 완전히 새로운 구현의 시작으로 사용하십시오.
>* 이를 참조 구현으로 활용하여 구성 방법을 확인한 다음 현재 프로덕션 구현에서 복제할 수 있습니다.

빠른 시작 기능을 사용하면 Meta 전환 API 및 Meta Pixel 확장을 사용하여 쉽고 효율적으로 설정할 수 있습니다. 이 도구는 Adobe 태그 및 이벤트 전달에서 수행되는 여러 단계를 자동화하여 설정 시간을 크게 줄입니다.

이 기능은 필요한 규칙 및 데이터 요소와 함께 새로 자동 생성된 태그 및 이벤트 전달 속성에 Meta 전환 API 및 Meta 픽셀 확장 기능을 자동으로 설치하고 구성합니다. 또한 Experience Platform Web SDK 및 데이터 스트림을 자동으로 설치 및 구성합니다. 마지막으로, 빠른 시작 기능은 이벤트 전달 및 Experience Platform Edge Network을 통해 클라이언트측 데이터 수집 및 서버측 이벤트 전달을 실시간으로 사용할 수 있도록 개발 환경의 지정된 URL에 라이브러리를 자동으로 게시합니다.

다음 비디오에서는 빠른 시작 기능에 대해 소개합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### 빠른 시작 기능 설치

>[!NOTE]
>
>이 기능은 이벤트 전달 구현을 시작하는 데 도움이 되도록 설계되었습니다. 모든 사용 사례를 수용하는 완전한 기능의 엔드 투 엔드 구현을 제공하지 않습니다.

이 설치 프로그램은 Meta 전환 API 및 Meta Pixel 확장을 모두 자동으로 설치합니다. 이 하이브리드 구현은 이벤트 전환 서버측을 수집 및 전달하기 위해 Meta에서 권장합니다.
빠른 설정 기능은 고객이 이벤트 전달 구현을 시작할 수 있도록 고안된 것으로, 모든 사용 사례를 수용하는 완전한 기능의 엔드 투 엔드 구현을 제공하기 위한 것이 아닙니다.

기능을 설치하려면 Adobe Experience Platform 데이터 컬렉션 **[!UICONTROL Get Started]** 페이지에서 **[!DNL Send Conversions Data to Meta]**&#x200B;에 대해 **[!UICONTROL Home]**&#x200B;을(를) 선택하십시오.

메타에 대한 전환 데이터를 표시하는 ![데이터 수집 홈 페이지](../../../images/extensions/server/meta/conversion-data-to-meta.png)

**[!UICONTROL Domain]**&#x200B;을(를) 입력한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다. 이 도메인은 자동 생성된 태그 및 이벤트 전달 속성, 규칙, 데이터 요소, 데이터스트림 등에 대한 명명 규칙으로 사용됩니다.

![도메인 이름을 요청하는 시작 화면](../../../images/extensions/server/meta/welcome.png)

**[!UICONTROL Initial Setup]** 대화 상자에서 **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta Conversion API Access Token]** 및 **[!UICONTROL Data Layer Path]**&#x200B;을(를) 입력한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![초기 설정 대화 상자](../../../images/extensions/server/meta/initial-setup.png)

초기 설정 프로세스가 완료될 때까지 잠시 기다린 후 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

![초기 설정 완료 확인 화면](../../../images/extensions/server/meta/setup-complete.png)

**[!UICONTROL Add Code on Your Site]** 대화 상자에서 복사 ![Copy](/help/images/icons/copy.png) 함수를 사용하여 제공된 코드를 복사하여 원본 웹 사이트의 `<head>`에 붙여넣습니다. 구현되면 **[!UICONTROL Start Validation]** 선택

![사이트 대화 상자에 코드 추가](../../../images/extensions/server/meta/add-code-on-your-site.png)

[!UICONTROL Validation Results] 대화 상자에 Meta 확장 구현 결과가 표시됩니다. **[!UICONTROL Next]**&#x200B;을(를) 선택합니다. **[!UICONTROL Assurance]** 링크를 선택하여 추가 유효성 검사 결과를 볼 수도 있습니다.

![구현 결과를 표시하는 테스트 결과 대화 상자](../../../images/extensions/server/meta/test-results.png)

**[!UICONTROL Next Steps]** 화면 표시에 설치 완료가 확인됩니다. 다음 섹션에 표시된 새 이벤트를 추가하여 구현을 최적화할 수 있는 옵션이 있습니다.

이벤트를 더 추가하지 않으려면 **[!UICONTROL Close]**&#x200B;을(를) 선택하십시오.

![다음 단계 대화 상자](../../../images/extensions/server/meta/next-steps.png)

#### 추가 이벤트 추가

새 이벤트를 추가하려면 **[!UICONTROL Edit Your Tags Web Property]**&#x200B;을(를) 선택하십시오.

![태그 웹 속성을 편집하는 다음 단계 대화 상자](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

편집할 메타 이벤트에 해당하는 규칙을 선택합니다. 예: **MetaConversion_AddToCart**.

>[!NOTE]
>
>이벤트가 없는 경우 이 규칙은 실행되지 않습니다. **MetaConversion_PageView** 규칙이 예외인 경우 모든 규칙에 대해 적용됩니다.

이벤트를 추가하려면 **[!UICONTROL Add]** 제목 아래의 [!UICONTROL Events]을(를) 선택하십시오.

![이벤트를 표시하지 않는 태그 속성 페이지](../../../images/extensions/server/meta/edit-rule.png)

[!UICONTROL Event Type]을(를) 선택합니다. 이 예제에서는 [!UICONTROL Click] 이벤트를 선택하고 **.add-to-cart-button**&#x200B;이 선택될 때 트리거되도록 구성했습니다. **[!UICONTROL Keep Changes]**&#x200B;를 선택합니다.

클릭 이벤트를 표시하는 ![이벤트 구성 화면](../../../images/extensions/server/meta/event-configuration.png)

새 이벤트가 저장되었습니다. **[!UICONTROL Select a working library]**&#x200B;을(를) 선택하고 빌드할 라이브러리를 선택합니다.

![작업 라이브러리 드롭다운 선택](../../../images/extensions/server/meta/working-library.png)

그런 다음 **[!UICONTROL Save to Library]** 옆의 드롭다운을 선택하고 **[!UICONTROL Save to Library and Build]**&#x200B;을(를) 선택합니다. 이렇게 하면 변경 사항이 라이브러리에 게시됩니다.

![라이브러리 및 빌드에 저장 선택](../../../images/extensions/server/meta/save-and-build.png)

구성할 다른 메타 전환 이벤트에 대해 이 단계를 반복합니다.

#### 데이터 레이어 구성 {#configuration}

>[!IMPORTANT]
>
>이 글로벌 데이터 레이어를 업데이트하는 방법은 웹 사이트 아키텍처에 따라 다릅니다. 단일 페이지 애플리케이션은 서버측 렌더링 앱과 다릅니다. 또한 Tags 제품 내에서 이 데이터를 만들고 업데이트하는 일을 전적으로 귀하가 담당하게 될 가능성도 있습니다. 모든 인스턴스에서 각 `MetaConversion_* rules`을(를) 실행하는 사이에 데이터 계층을 업데이트해야 합니다. 규칙 간 데이터를 업데이트하지 않으면 현재 `MetaConversion_* rule`의 마지막 `MetaConversion_* rule`에서 오래된 데이터를 보내는 경우도 발생할 수 있습니다.

구성 중에 데이터 계층이 있는 위치를 묻는 메시지가 표시됩니다. 기본적으로 `window.dataLayer.meta`이(가) 되며 `meta` 개체 내에서는 아래와 같이 데이터가 필요합니다.

![데이터 계층 메타 정보](../../../images/extensions/server/meta/data-layer-meta.png)

모든 `MetaConversion_*` 규칙에서 이 데이터 구조를 사용하여 관련 데이터를 [!DNL Meta Pixel] 확장 및 [!DNL Meta Conversions API]에 전달하므로 이 점을 이해하는 것이 중요합니다. 다양한 메타 이벤트에 필요한 데이터에 대한 자세한 내용은 [표준 이벤트](https://developers.facebook.com/docs/meta-pixel/reference#standard-events)에 대한 설명서를 참조하십시오.

예를 들어 `MetaConversion_Subscribe` 규칙을 사용하려면 `window.dataLayer.meta.currency`표준 이벤트`window.dataLayer.meta.predicted_ltv`에 대한 설명서에 설명된 개체 속성에 따라 `window.dataLayer.meta.value`, [ 및 ](https://developers.facebook.com/docs/meta-pixel/reference#standard-events)을(를) 업데이트해야 합니다.

다음은 규칙을 실행하기 전에 데이터 레이어를 업데이트하기 위해 웹 사이트에서 실행해야 하는 예입니다.

![데이터 레이어 메타 정보 업데이트](../../../images/extensions/server/meta/update-data-layer-meta.png)

기본적으로 `<datalayerpath>.conversionData.eventId`은(는) `MetaConversion_* rules`에서 &quot;새 이벤트 ID 생성&quot; 작업에 의해 임의로 생성됩니다.

데이터 레이어의 모습에 대한 로컬 참조를 위해 속성의 `MetaConversion_DataLayer` 데이터 요소에서 사용자 지정 코드 편집기를 열 수 있습니다.

## 다음 단계

이 안내서에서는 [!DNL Meta] 확장을 사용하여 서버측 이벤트 데이터를 [!DNL Meta Conversions API]에 보내는 방법을 다룹니다. 적용 가능한 경우 더 많은 [!DNL Pixels]을(를) 연결하고 더 많은 이벤트를 공유하여 통합을 확장하는 것이 좋습니다. 다음 중 하나를 수행하면 광고 성능을 더욱 향상시킬 수 있습니다.

* 아직 [!DNL Pixels] 통합에 연결되지 않은 다른 [!DNL Conversions API]을(를) 연결합니다.
* 클라이언트측에서 [!DNL Meta Pixel]을(를) 통해서만 특정 이벤트를 보낼 경우 서버측에서도 동일한 이벤트를 [!DNL Conversions API]에 보냅니다.

통합을 효과적으로 구현하는 방법에 대한 자세한 지침은 [!DNL Meta]의 모범 사례[ [!DNL Conversions API]에 대한 ](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 설명서를 참조하십시오. Adobe Experience Cloud의 태그 및 이벤트 전달에 대한 자세한 내용은 [태그 개요](../../../home.md)를 참조하세요.
