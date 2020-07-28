---
title: Adobe Analytics으로 데이터 보내기
seo-title: Adobe Experience Platform 웹 SDK를 사용하여 Adobe Analytics으로 데이터 보내기
description: Experience Platform 웹 SDK를 사용하여 데이터를 Adobe Analytics으로 전송하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK를 사용하여 데이터를 Adobe Analytics으로 전송하는 방법 살펴보기
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Adobe Analytics으로 데이터 보내기

Adobe Experience Platform은 Adobe Analytics으로 데이터를 보낼 [!DNL Web SDK] 수 있습니다. 이것은 Adobe Analytics이 사용할 수 있는 형식 `xdm` 으로 번역하는 것이다.

## 설정

고객 구성 UI에 매핑된 보고서 세트가 있는 경우 Adobe Analytics은 전송하려는 데이터를 자동으로 선택합니다. 여기에서 하나 이상의 보고서를 지정된 구성에 매핑할 수 있습니다. 보고서 세트가 매핑되면 데이터가 자동으로 이동하기 시작합니다.

## 자동으로 매핑된 데이터

Adobe Experience Platform은 많은 XDM 변수를 자동으로 [!DNL Edge Network] 매핑합니다. 자동으로 매핑된 변수의 전체 목록은 [여기에 나와 있습니다](../analytics/automatically-mapped-vars.md).

## 수동으로 매핑된 데이터

Edge Network에서 수집한 모든 데이터는 처리 규칙을 통해 액세스할 수 있습니다. 데이터는 점 표기법을 사용하여 분리되고 contextData로 사용할 수 있습니다.

이렇게 생긴 스키마가 있다면

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

그런 다음 컨텍스트 데이터 키를 사용할 수 있습니다.

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

![처리 규칙 인터페이스](../../../assets/edge_analytics_processing_rules.png)
