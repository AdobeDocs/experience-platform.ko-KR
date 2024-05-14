---
title: Web SDK를 사용하여 Adobe Analytics에 데이터 보내기
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics에 데이터를 전송하는 방법에 대해 알아봅니다.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 웹 SDK를 사용하여 Adobe Analytics에 데이터 보내기

Experience Platform Web SDK는 Experience Platform Edge Network을 통해 Adobe Analytics에 데이터를 전송할 수 있습니다. Adobe은 웹 SDK를 사용하여 Adobe Analytics으로 데이터를 전송하는 몇 가지 옵션을 제공합니다.

* 추가 [**[!UICONTROL Adobe Analytics ExperienceEvent 필드 그룹]**](../../xdm/field-groups/event/analytics-full-extension.md) 스키마에 연결한 다음 [`XDM` 오브젝트](../commands/sendevent/xdm.md).
* 사용 [`data` 오브젝트](../commands/sendevent/data.md) XDM 스키마 없이 Adobe Analytics으로 데이터를 전송합니다.
* 자동으로 생성된 사용 [컨텍스트 데이터 변수](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) 및 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## 사용 `XDM` 오브젝트 {#use-xdm-object}

Adobe Analytics과 관련된 사전 정의된 스키마를 사용하려면 다음을 추가할 수 있습니다. [Adobe Analytics ExperienceEvent 스키마 필드 그룹](../../xdm/field-groups/event/analytics-full-extension.md) 을 스키마에 추가합니다. 추가되면 다음을 사용하여 이 스키마를 채울 수 있습니다. `xdm` 보고서 세트로 데이터를 보낼 Web SDK의 개체입니다. 데이터가 Edge Network에 도달하면 XDM 개체를 Adobe Analytics이 인식하는 형식으로 변환합니다.

Web SDK를 통해 Adobe Analytics으로 데이터를 전송하는 방법에는 두 가지가 있습니다.

* [Web SDK 태그 확장을 사용하여 Adobe Analytics에 데이터 보내기](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [웹 SDK JavaScript 라이브러리를 사용하여 Adobe Analytics에 데이터 보내기](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

다음을 참조하십시오 [Adobe Analytics에 대한 XDM 개체 변수 매핑](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping) XDM 필드 및 Analytics 변수에 매핑되는 방법에 대한 전체 참조는 Adobe Analytics 구현 안내서에서 확인할 수 있습니다.

## 사용 `data` 오브젝트 {#use-data-object}

XDM 개체를 사용하는 대신 데이터 개체를 사용할 수 있습니다. 데이터 개체는 현재 AppMeasurement을 사용하는 구현에 맞게 디자인되어 웹 SDK로의 업그레이드가 훨씬 쉬워집니다.

AppMeasurement 또는 Analytics 태그 확장을 사용하는지에 따라 Web SDK로 마이그레이션하는 방법에 대한 자세한 내용은 다음 안내서를 참조하십시오.

* [Adobe Analytics 태그 확장에서 웹 SDK 태그 확장으로 마이그레이션](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [AppMeasurement에서 웹 SDK로 마이그레이션](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

다음에서 설명서를 참조하십시오. [Adobe Analytics에 대한 데이터 개체 변수 매핑](https://experienceleague.adobe.com/ko/docs/analytics/implementation/aep-edge/data-var-mapping) 데이터 개체 필드에 대한 전체 참조 및 이 필드가 Analytics 변수에 매핑되는 방법에 대해서는 Adobe Analytics 구현 안내서에서 확인할 수 있습니다.

## 컨텍스트 데이터 변수 사용 {#use-context-data-variables}

자동으로 매핑되지 않는 모든 변수는 [컨텍스트 데이터 변수](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata). 그런 다음 을 사용할 수 있습니다. [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) 컨텍스트 데이터 변수를 Analytics 변수에 매핑합니다. 예를 들어 다음과 같은 사용자 지정 XDM 스키마가 있는 경우:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

그런 다음 이러한 필드는 처리 규칙 인터페이스에서 사용할 수 있는 컨텍스트 데이터 키가 됩니다.

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## FAQ

+++웹 SDK에서 페이지 보기 호출을 링크 추적 호출과 어떻게 구별합니까?

Adobe Analytics의 AppMeasurement은 페이지 보기에 대해 별도의 메서드 호출을 사용합니다([`t()` 방법](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)) 및 링크 추적 호출([`tl()` 방법](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)). Web SDK는 대신 [`sendEvent`](../commands/sendevent/overview.md) 페이지 보기와 링크 추적을 모두 전송하는 명령입니다. 이벤트에 포함하는 데이터에 따라 이벤트인지 여부가 결정됩니다. [페이지 보기](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views) 또는 [페이지 이벤트](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events) Adobe Analytics.

기본적으로 모든 이벤트는 Adobe Analytics의 페이지 보기로 간주됩니다. 웹 SDK 이벤트를 Adobe Analytics 링크 추적 호출로 설정하려면 다음 필드를 설정하십시오.

* **XDM 개체**: `xdm.web.webInteraction.name`, `web.webInteraction.type`, 및 `web.webInteraction.URL`
* **데이터 개체**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType`, 및 `data.__adobe.analytics.linkURL`
* **컨텍스트 데이터**: 지원되지 않음

다음을 참조하십시오. [`tl()` 방법](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method) 자세한 내용은 Adobe Analytics 구현 안내서 를 참조하십시오.

을 활성화한 경우 [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) 다음에서 `configure` 명령을 실행하면 필드가 채워집니다.

+++

+++데이터 스트림은 Adobe Analytics에 사용되는 데이터를 사용하여 데이터를 다른 서비스와 어떻게 구별합니까?

데이터스트림으로 전송된 모든 이벤트는 구성된 모든 서비스에 전달됩니다. 예를 들어, 개인화 및 Analytics에 대해 별도의 호출을 수행하면 두 이벤트가 모두 Analytics 및 Target으로 전송됩니다. 이러한 이벤트는 Analytics 보고에 기록되며 바운스 비율과 같은 지표에 영향을 줄 수 있습니다.

웹 SDK를 사용하는 경우 이러한 호출은 일반적으로 [`sendEvent`](../commands/sendevent/overview.md) 명령입니다.

+++
