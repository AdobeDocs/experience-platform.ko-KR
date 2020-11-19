---
title: Adobe Analytics에서 수동으로 변수 매핑
seo-title: 웹 SDK를 사용하여 Adobe Analytics의 변수 수동 매핑
description: 처리 규칙을 사용하여 변수를 수동으로 Adobe Analytics에 매핑하는 방법
seo-description: 웹 SDK에서 처리 규칙을 사용하여 변수를 Adobe Analytics에 수동으로 매핑
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 35%

---


# Adobe Analytics에서 수동으로 변수 매핑

Adobe Experience Platform은 특정 변수를 자동으로 매핑할 [!DNL Web SDK] 수 있지만 사용자 지정 변수는 수동으로 매핑해야 합니다.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/ko-KR/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/ko-KR/experience-platform/xdm/schema/composition.html). 그런 다음 [!DNL Analytics] 처리 규칙 [을 사용하여](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) [!DNL Analytics] 변수에 매핑할 수 있습니다.

또한 기본 작업 및 제품 목록을 사용하여 Adobe Experience Platform 웹 SDK를 사용하여 데이터를 전송 또는 검색할 수 있습니다. 이렇게 하려면 [제품](https://docs.adobe.com/content/help/ko-KR/experience-platform/edge/implement/commerce.html)을 참조하십시오.

## 컨텍스트 데이터

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. 다음 값 쌍 목록은 `context data`의 예를 보여줍니다.

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## 처리 규칙

에지 네트워크에서 수집한 모든 데이터는 [처리 규칙](https://docs.adobe.com/content/help/ko-KR/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)을 통해 액세스할 수 있습니다. In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

For example, in the following rule, Adobe Analytics is set to populate **Internal Search terms (eVar2)** with the data associated with **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM 스키마

Adobe Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터를 통해 가치를 창출할 수 있습니다. [!DNL Analytics] 컨텍스트 데이터는 스키마에 의해 정의된 구조와 함께 작동합니다.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/ko-KR/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with Adobe Experience Platform Web SDK. 이 예에서 `event` 명령은 productListItems `name` 및 `SKU` 값을 추적하도록 [ExperienceEvent Commerce Details 스키마](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)와 일치합니다.


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Adobe Experience Platform의 이벤트 추적에 대한 자세한 내용 [!DNL Web SDK]은 이벤트 [추적을 참조하십시오](https://docs.adobe.com/content/help/ko-KR/experience-platform/edge/fundamentals/tracking-events.html).
