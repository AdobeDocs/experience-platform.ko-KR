---
title: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics에 데이터 보내기
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Analytics으로 데이터를 전송하는 방법을 알아봅니다.
keywords: adobe analytics;analytics;매핑된 데이터;매핑된 vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---

# Adobe Analytics에 데이터 보내기

Adobe Experience Platform [!DNL Web SDK]은(는) 데이터를 Adobe Analytics에 보낼 수 있습니다. 이 기능은 `xdm`을 Adobe Analytics에서 사용할 수 있는 형식으로 변환하여 작동합니다.

## 설정

Adobe Analytics에서는 고객 구성 UI에 매핑된 보고서 세트가 있는 경우 보내고 있는 데이터를 자동으로 선택합니다. 여기에서 하나 이상의 보고서를 주어진 구성에 매핑할 수 있습니다. 보고서 세트가 매핑되면 데이터 흐름이 자동으로 시작됩니다.

## 자동으로 매핑된 데이터

Adobe Experience Platform [!DNL Edge Network]은(는) 많은 XDM 변수를 자동으로 매핑합니다. 이러한 변수의 전체 목록이 [여기](automatically-mapped-vars.md)에 나열되어 있습니다.

## 수동으로 매핑된 데이터

에지 네트워크에서 수집한 모든 데이터는 처리 규칙을 통해 액세스할 수 있습니다. 데이터는 점 표기법을 사용하여 변환되고 contextData로 사용할 수 있습니다.

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
