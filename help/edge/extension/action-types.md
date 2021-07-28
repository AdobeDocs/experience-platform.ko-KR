---
title: Adobe Experience Platform Web SDK 확장의 작업 유형
description: Adobe Experience Platform 웹 SDK 태그 확장에서 제공하는 다양한 작업 유형에 대해 알아봅니다.
solution: Experience Platform
feature: 웹 SDK
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 4%

---

# 작업 유형

[Adobe Experience Platform 웹 SDK 태그 확장 프로그램](web-sdk-extension-configuration.md)을 구성한 후 작업 유형을 구성합니다.

이 페이지에서는 사용 가능한 작업 유형을 설명합니다.

## 이벤트 보내기

사용자가 전송하는 데이터를 수집하고 해당 정보에 대해 조치를 취할 수 있도록 Adobe Experience Platform이 Adobe [!DNL Experience Platform]에 이벤트를 보냅니다. 인스턴스를 선택합니다(인스턴스가 두 개 이상인 경우). 전송하려는 모든 데이터는 **[!UICONTROL XDM 데이터]** 필드에서 전송할 수 있습니다. XDM 스키마의 구조를 준수하는 JSON 개체를 사용합니다. 이 개체는 페이지 또는 **[!UICONTROL 사용자 지정 코드]** **[!UICONTROL 데이터 요소]**&#x200B;를 통해 만들 수 있습니다.

이벤트 보내기 작업 유형에는 구현에 따라 유용할 수 있는 몇 가지 다른 필드가 있습니다. 이러한 필드는 모두 선택 사항입니다.

- **유형:** 이 필드에서는 XDM 스키마에 기록할 이벤트 유형을 지정할 수 있습니다. 기본 이벤트 유형에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)를 참조하십시오.
- **데이터:** XDM 스키마와 일치하지 않는 데이터는 이 필드를 사용하여 전송할 수 있습니다. 이 필드는 Adobe Target 프로필을 업데이트하거나 Target Recommendations 속성을 전송하려고 하는 경우 유용합니다. 예를 보려면 [설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en)를 참조하십시오.
- **병합 ID:** 이벤트에 대한 병합 ID를 지정하려면 이 필드에서 지정할 수 있습니다. 현재 다운스트림 솔루션은 이벤트 데이터를 병합할 수 없습니다.
- **데이터 세트 ID:**  데이터 스트림에 지정한 데이터 세트 이외의 데이터 세트에 데이터를 보내야 하는 경우 여기에서 해당 데이터 세트 ID를 지정할 수 있습니다.
- **문서가 언로드됨:**  사용자가 페이지에서 멀리 탐색하더라도 이벤트가 서버에 도달하는지 확인하려면 문서  **[!UICONTROL 언로드 확인란을]** 선택합니다. 이를 통해 이벤트가 서버에 도달할 수 있지만 응답은 무시됩니다.
- **시각적 개인화 결정 렌더링:**  페이지에서 개인화된 콘텐츠를 렌더링하려면 시각적 개인화 결정  **[!UICONTROL 렌더링 확인란을]** 선택합니다. 필요한 경우 결정 범위를 지정할 수도 있습니다. 개인화된 콘텐츠 렌더링에 대한 자세한 내용은 [개인화 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content)를 참조하십시오.

## 동의 설정

사용자로부터 동의를 받은 후 &quot;동의 설정&quot; 작업 유형을 사용하여 이 동의를 Adobe Experience Platform Web SDK에 전달해야 합니다. 현재 &quot;Adobe&quot; 및 &quot;IAB TCF&quot;, 2가지 유형의 표준이 지원됩니다. [고객 동의 기본 설정 지원](../consent/supporting-consent.md)을 참조하십시오. Adobe 버전 2.0을 사용하는 경우 데이터 요소 값만 지원됩니다. 동의 개체로 확인되는 데이터 요소를 만들어야 합니다.

이 작업에서는 동의를 받으면 ID를 동기화할 수 있도록 ID 맵을 포함하는 선택적 필드도 제공됩니다. 동기화는 동의 호출이 첫 번째 호출을 실행할 가능성이 높으므로 동의가 &quot;보류 중&quot; 또는 &quot;종료&quot;로 구성되는 경우 유용합니다.

## 이벤트 병합 ID 재설정

페이지에서 이벤트 병합 ID를 재설정하려면 이 작업을 통해 이 작업을 수행할 수 있습니다. ID를 재설정하려면 재설정할 병합 ID를 선택하고 필요에 따라 작업을 실행합니다.

## 다음은 무엇입니까

작업을 설정한 후 [데이터 요소 유형](data-element-types.md)을 구성합니다.
