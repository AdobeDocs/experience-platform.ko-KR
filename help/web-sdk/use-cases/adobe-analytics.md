---
title: Web SDK를 사용하여 Adobe Analytics에 데이터 보내기
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics에 데이터를 전송하는 방법에 대해 알아봅니다.
keywords: adobe analytics;analytics;매핑된 데이터;매핑된 변수;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# 웹 SDK를 사용하여 Adobe Analytics에 데이터 보내기

Adobe Experience Platform Web SDK는 Adobe Experience Platform Edge Network를 통해 Adobe Analytics으로 데이터를 전송할 수 있습니다. 데이터가 Edge Network에 도달하면 XDM 개체를 Adobe Analytics이 인식하는 형식으로 변환합니다.

## XDM 필드 그룹

가장 일반적인 Adobe Analytics 지표를 더 쉽게 캡처할 수 있도록 Adobe은 사용할 수 있는 Adobe Analytics에 초점을 맞춘 필드 그룹을 제공합니다. 이 스키마에 대한 자세한 내용은 [Adobe Analytics ExperienceEvent 전체 확장 스키마 필드 그룹](/help/xdm/field-groups/event/analytics-full-extension.md).

## 변수 매핑

Edge Network는 자동으로 많은 XDM 변수를 매핑합니다. 다음을 참조하십시오 [Edge Network의 Analytics 변수 매핑](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=ko-KR) 자동으로 매핑된 변수의 포괄적인 변수 목록에 대해서는 Adobe Analytics 구현 안내서에서 확인할 수 있습니다.

자동으로 매핑되지 않는 모든 변수는 [컨텍스트 데이터 변수](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=ko-KR). 그런 다음 을 사용할 수 있습니다. [처리 규칙](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) 컨텍스트 데이터 변수를 Analytics 변수에 매핑합니다. 예를 들어 다음과 같은 사용자 지정 XDM 스키마가 있는 경우:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

그런 다음 처리 규칙 인터페이스에서 사용할 수 있는 컨텍스트 데이터 키가 됩니다.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Edge Network 컬렉션을 사용하면 모든 이벤트가 Analytics 및 데이터스트림에 대해 구성한 다른 서비스로 전송됩니다. 예를 들어 Analytics와 Target이 모두 서비스로 구성되어 있고 개인화 및 Analytics에 대해 별도의 호출을 하는 경우 두 이벤트가 모두 Analytics 및 Target으로 전송됩니다. 이러한 이벤트는 Analytics 보고에 기록되며 바운스 비율과 같은 지표에 영향을 줄 수 있습니다.

## 페이지 보기 및 링크 추적 호출

Adobe Analytics의 AppMeasurement은 페이지 보기에 대해 별도의 메서드 호출을 사용합니다([`t()` 방법](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) 및 링크 추적 호출([`tl()` 방법](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). Web SDK는 대신 [`sendEvent`](../commands/sendevent/overview.md) 페이지 보기와 링크 추적을 모두 전송하는 명령입니다. 이벤트에 포함하는 데이터에 따라 이벤트인지 여부가 결정됩니다. [페이지 보기](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html) 또는 [페이지 이벤트](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) Adobe Analytics.

기본적으로 모든 이벤트는 Adobe Analytics의 페이지 보기로 간주됩니다. 웹 SDK 이벤트를 Adobe Analytics 링크 추적 호출로 설정하려면 다음 XDM 필드를 설정합니다.

* **`web.webInteraction.URL`**: 링크 URL입니다.
* **`web.webInteraction.name`**: 의 값에 따라 사용자 지정 링크, 다운로드 링크 또는 종료 링크 차원 이름입니다 `web.webInteraction.type`
* **`web.webInteraction.type`**: 클릭한 링크의 유형을 결정합니다. 유효한 값에는 `other`(사용자 정의 링크), `download`(다운로드 링크) 및 `exit`(종료 링크)가 포함됩니다.

을 활성화한 경우 [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) 다음에서 `configure` 명령을 실행하면 이러한 XDM 필드가 채워집니다.
