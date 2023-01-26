---
title: Platform Web SDK에서 Adobe Journey Optimizer 사용
description: Adobe Journey Optimizer을 사용하여 Experience Platform Web SDK로 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다
keywords: ajo;ajo 웹;adobe 여정 최적화 프로그램;렌더링 결정;표면;결정;제안;범위;스키마
exl-id: e608952c-9598-11ed-b382-d72064651cac
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 사용 [!DNL Adobe Journey Optimizer] 사용 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 에서 관리하는 개인화된 경험을 제공하고 렌더링할 수 있습니다. [!DNL Adobe Journey Optimizer] 참조하십시오. WYSIWYG 편집기를 사용할 수 있습니다. [!DNL Adobe Journey Optimizer] [웹 캠페인 UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), 을(를) 생성, 활성화 및 전달하는 데 사용됩니다. [!DNL Journey Optimizer Web] 캠페인 및 개인화 경험.

>[!IMPORTANT]
>
>다음 문서를 참조하십시오. [Adobe Journey Optimizer 웹 채널 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) 시작하기 [!DNL Journey Optimizer Web] 경험 작성 및 보고.

## 용어 {#terminology}

**[!UICONTROL 서피스]**: 웹 서피스는 [!DNL Adobe Journey Optimizer] 경험 콘텐츠가 전달됩니다.

**[!UICONTROL Proposition]**: in [!DNL Adobe Journey Optimizer], 포지션은 [!DNL Journey Optimizer Campaign].

## 활성화 [!DNL Adobe Journey Optimizer] {#enable-ajo}

사용을 시작하려면 [!DNL Adobe Journey Optimizer]를 채우기 위해 아래의 단계를 수행하십시오.

1. 를 통해 [전제 조건](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) 에서 [!DNL Adobe Journey Optimizer] [웹 경험 안내서](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)특히
   * 설정 [!DNL Adobe Experience Cloud Visual Editing Helper].
   * 활성화 [!DNL Adobe Journey Optimizer] 다음 위치에서 [데이터 스트림](../../datastreams/overview.md).
   * 를 활성화합니다 [!UICONTROL Active-On-Edge 병합 정책] 선택 사항입니다.

2. 추가 `renderDecisions` 선택 사항을 이벤트에 추가합니다. 설정 `renderDecisions` to `true` 배달된 Journey Optimizer 컨텐츠 proposition을 웹 페이지 표면에 자동으로 렌더링하기 위해.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. 이벤트에 추가 서피스를 지정할 수도 있습니다. 기본적으로 웹 SDK는 현재 웹 페이지의 웹 서피스를 자동으로 생성하여 Edge Network에 대한 요청에 포함합니다. 필요한 경우 요청에서 추가 서피스를 지정하여 요청에 추가할 수 있습니다 `personalization.surfaces` 옵션 `sendEvent` 명령 또는 **[!UICONTROL 서피스]** [[!UICONTROL 이벤트 보내기] 작업](../../extension/action-types.md#send-event) 웹 SDK 확장의 구성.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![확장 추가 면](./assets/extension-add-surface.png)

   이벤트 서피스는 `query.personalization.surfaces` 요청 필드:

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. 다른 개인화 기능과 유사하게 **[코드 조각 숨기기](../manage-flicker.md)** 경험을 가져오는 동안 페이지의 특정 부분만 숨기려면

## Adobe Journey Optimizer 웹 경험 만들기 {#create-ajo-web-experiences}

다음을 수행합니다 [웹 캠페인 작성](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) 의 지침 [!DNL Adobe Journey Optimizer] [웹 경험 안내서](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 만들기 [!DNL Journey Optimizer Web] 캠페인 및 경험.

## 개인화된 콘텐츠 렌더링 {#rendering-personalized-content}

다음 문서를 참조하십시오. [개인화 콘텐츠 렌더링](../rendering-personalization-content.md) 추가 정보.

웹 서피스에 대한 Adobe Journey Optimizer Proposition은 `__view__` 결정 범위 제안 특히 `renderDecisions` 옵션이 `true` 에서 `sendEvent` 명령은 웹 SDK에 의해 자동으로 렌더링됩니다.

샘플 Journey Optimizer 컨텐츠 제안:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## 디버깅 {#debugging}

Adobe Journey Optimizer 개인화 구현을 디버깅하려면 [[!DNL Web SDK] 디버깅](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] 디버그 추적은 [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). 를 사용하여 이벤트 확인 `AJO:` 접두사를 사용합니다.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)


