---
title: Adobe Experience Platform Web SDK Extension의 작업 유형
description: Adobe Experience Platform Launch의 Adobe Experience Platform Web SDK 익스텐션에서 제공하는 다양한 작업 유형에 대해 알아보십시오.
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 6%

---


# 작업 유형

[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)에 대해 [Adobe Experience Platform 웹 SDK 확장](web-sdk-extension.md)을 구성한 후 작업 유형을 구성합니다.

이 페이지에서는 사용 가능한 작업 유형에 대해 설명합니다.

## 이벤트 보내기

사용자가 전송하는 데이터를 수집하고 해당 정보에 대해 조치를 취할 수 있도록 Adobe Experience Platform이 Adobe [!DNL Experience Platform]에 이벤트를 전송합니다. 인스턴스를 선택합니다(인스턴스가 두 개 이상인 경우). 페이지가 로드될 때 또는 단일 페이지 응용 프로그램에서 보기 변경 중에 이벤트가 발생하는 경우 보기 시작 시 **[!UICONTROL 발생]**&#x200B;을 선택합니다.

보내려는 모든 데이터는 **[!UICONTROL XDM 데이터]** 필드에 보낼 수 있습니다. XDM 스키마 구조를 준수하는 JSON 개체를 사용합니다. 이 개체는 페이지에서 또는 **[!UICONTROL 사용자 지정 코드]** **[!UICONTROL 데이터 요소]**&#x200B;를 통해 만들 수 있습니다.

## 동의 설정

사용자의 동의를 받은 후에는 &quot;동의 설정&quot; 작업 유형을 사용하여 이 동의를 Adobe Experience Platform 웹 SDK에 전달해야 합니다. 현재 &quot;Adobe&quot; 및 &quot;IAB TCF&quot;, 2가지 유형의 표준이 지원됩니다. [고객 동의 기본 설정 지원](../consent/supporting-consent.md)을 참조하십시오. Adobe 버전 2.0을 사용하는 경우 데이터 요소 값만 지원됩니다. 동의 개체로 확인되는 데이터 요소를 만들어야 합니다.

이 작업에서는 동의를 받으면 ID를 동기화할 수 있도록 ID 맵을 포함할 선택 필드도 제공됩니다. 동기화는 동의 호출이 &quot;보류 중&quot; 또는 &quot;종료&quot;로 구성된 경우 동의 호출이 처음 실행되도록 할 수 있으므로 유용합니다.

## 이벤트 병합 ID 재설정

페이지에서 이벤트 병합 ID를 재설정하려면 이 작업으로 할 수 있습니다. ID를 재설정하려면 재설정할 병합 ID를 선택하고 필요에 따라 작업을 실행합니다.

## 다음 단계

작업 유형을 설정한 후 [데이터 요소 유형](data-element-types.md)을 구성합니다.