---
title: Platform Web SDK에서 Adobe Analytics 사용
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics으로 데이터를 전송하는 방법을 알아봅니다.
keywords: adobe analytics;analytics;매핑된 데이터;매핑된 vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 836fa7814a6966903639e871bfaea0563847f363
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Platform Web SDK에서 Adobe Analytics 사용

Adobe Experience Platform [!DNL Web SDK] Adobe Analytics으로 데이터를 전송할 수 있습니다. 번역을 통해 작동됩니다 `xdm` 형식에서 Adobe Analytics에서 사용할 수 있습니다.

## 설정

Adobe Analytics에서는 고객 구성 UI에 매핑된 보고서 세트가 있는 경우 보내고 있는 데이터를 자동으로 선택합니다. 여기에서 하나 이상의 보고서를 주어진 구성에 매핑할 수 있습니다. 보고서 세트가 매핑되면 데이터 흐름이 자동으로 시작됩니다.

## XDM 필드 그룹

가장 일반적인 Adobe Analytics 지표를 더 쉽게 캡처할 수 있도록 하기 위해 Adobe에서는 사용할 수 있는 Analytics 필드 그룹을 제공합니다. 이 스키마에 대한 자세한 내용은 [Adobe Analytics ExperienceEvent 전체 확장 스키마 필드 그룹](../../../xdm/field-groups/event/analytics-full-extension.md)

## 자동으로 매핑된 데이터

Adobe Experience Platform [!DNL Edge Network] 는 여러 XDM 변수를 자동으로 매핑합니다. 이러한 변수의 전체 목록이 표시됩니다 [여기](automatically-mapped-vars.md).

## 수동으로 매핑된 데이터

에 의해 자동으로 매핑되지 않는 모든 데이터 [!DNL Edge Network] 는 처리 규칙을 통해 액세스할 수 있습니다. 데이터는 점 표기법을 사용하여 변환되고 contextData로 사용할 수 있습니다.

스키마는 다음과 같습니다.

```javascript
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

컨텍스트 데이터 키가 여기에 해당합니다.

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

다음은 이 데이터를 사용하는 처리 규칙의 예입니다.

![처리 규칙 인터페이스](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>Experience Edge 컬렉션을 사용하면 모든 이벤트가 Analytics와 데이터 스트림에 대해 구성한 다른 서비스로 전송됩니다. 예를 들어, Analytics와 Target이 모두 서비스로 구성되어 있고 개인화와 Analytics에 대해 별도의 호출을 하는 경우 두 이벤트가 모두 Target과 Analytics로 전송됩니다. 이러한 이벤트는 Analytics 보고에 기록되며 바운스 비율 등의 지표에 영향을 줄 수 있습니다.
