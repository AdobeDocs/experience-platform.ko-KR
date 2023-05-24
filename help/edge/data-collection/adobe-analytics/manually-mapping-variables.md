---
title: Adobe Experience Platform Web SDK에서 Adobe Analytics 변수 수동 매핑
description: Experience Platform Web SDK의 처리 규칙을 사용하여 변수를 수동으로 Adobe Analytics에 매핑하는 방법에 대해 알아봅니다.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;변수;변수 매핑;변수 매핑;컨텍스트 데이터;컨텍스트 데이터;처리 규칙;규칙;xdm;스키마;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 9392a90b70699b79949095e178ea77dd34d313a3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 25%

---

# Adobe Analytics에서 수동으로 변수 매핑

Adobe Experience Platform [!DNL Web SDK] 은 특정 변수를 자동으로 매핑할 수 있지만 사용자 지정 변수는 수동으로 매핑해야 합니다.

자동으로 매핑되지 않는 XDM 데이터의 경우 [!DNL Analytics], 다음을 사용할 수 있습니다 [컨텍스트 데이터](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=ko-KR) 을(를) 일치시키려면 [스키마](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko). 그런 다음 로 매핑할 수 있습니다. [!DNL Analytics] 사용 [처리 규칙](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=ko-KR) 채우려면 [!DNL Analytics] 변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다.

또한 기본 작업 세트 및 제품 목록을 사용하여 Adobe Experience Platform Web SDK로 데이터를 전송하거나 검색할 수 있습니다. 이렇게 하려면 다음을 참조하십시오. [상거래 및 제품 정보 수집](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## 컨텍스트 데이터

사용 대상 [!DNL Analytics], XDM 데이터는 점 표기법을 사용하여 변환되고 다음과 같이 사용할 수 있습니다. `contextData`. 다음 값 쌍 목록은 `context data` 평면화되면 다음과 같습니다.

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

에지 네트워크에서 수집한 모든 데이터는 [처리 규칙](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=ko-KR)을 통해 액세스할 수 있습니다. 위치 [!DNL Analytics], 처리 규칙 을 사용하여 컨텍스트 데이터를 [!DNL Analytics] 변수를 채우는 방법에 따라 페이지를 순서대로 표시합니다.

예를 들어 다음 규칙에서 Adobe Analytics은 을 채우도록 설정됩니다 **내부 검색어(eVar2)** 와 연계된 데이터 **a.x._atag.search.term(컨텍스트 데이터)**.

![](assets/examplerule.png)


## XDM 스키마

Adobe Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다. [!DNL Analytics] 컨텍스트 데이터는 스키마에 의해 정의된 구조와 함께 작동합니다.

다음 예제는 [`event` 명령](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=ko-KR) 과 함께 사용할 수 있습니다. `xdm` Adobe Experience Platform Web SDK를 사용하여 데이터를 전송하고 검색하는 옵션입니다. 이 예에서 `event` 명령은 productListItems `name` 및 `SKU` 값을 추적하도록 [ExperienceEvent Commerce Details 스키마](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)와 일치합니다.


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

Adobe Experience Platform을 사용한 이벤트 추적에 대한 자세한 정보 [!DNL Web SDK], 참조 [이벤트 추적](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=ko-KR).
