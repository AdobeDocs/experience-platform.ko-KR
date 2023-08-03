---
title: The Weather Channel의 날씨 데이터 사용
description: The Weather Channel의 날씨 데이터를 사용하여 데이터스트림을 통해 수집한 데이터를 보강할 수 있습니다.
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 4c9abcefb279c6e8a90744b692d86746a4896d0a
workflow-type: ht
source-wordcount: '672'
ht-degree: 100%

---

# [!DNL The Weather Channel]의 날씨 데이터 사용

Adobe는 데이터스트림을 통해 수집한 데이터에 미국 날씨에 대한 컨텍스트를 추가 제공하기 위해 [!DNL [The Weather Company]](https://www.ibm.com/weather)와(과) 파트너 관계를 맺고 있습니다. 이 데이터를 사용하여 Experience Platform에서 분석, 타겟팅 및 세그먼트 생성을 수행할 수 있습니다.

[!DNL The Weather Channel]에서 사용할 수 있는 3가지 유형의 데이터가 있습니다.

* **[!UICONTROL 현재 날씨]**: 해당 위치를 기준으로 한 사용자의 현재 기상 조건. 여기에는 현재 온도, 강수량, 전운량 등이 포함됩니다.
* **[!UICONTROL 날씨 예보]**: 날씨 예보에는 사용자 위치에 따라 1, 2, 3, 5, 7 및 10일차 예보가 있습니다.
* **[!UICONTROL 트리거]**: 트리거는 다양하고 유의미한 기상 조건에 매핑하는 특정 조합입니다. 날씨 트리거에는 세 가지 유형이 있습니다.

   * **[!UICONTROL 날씨 트리거]**: 날씨가 춥거나 비가 오는 날 등 유의미한 조건. 이는 기후에 따라 정의가 달라질 수 있습니다.
   * **[!UICONTROL 제품 트리거]**: 다양한 제품 구매로 연결될 수 있는 조건. 예: 추운 날씨가 예보되면서 우비를 구매할 가능성이 높아질 수 있습니다.
   * **[!UICONTROL 악천후 기상 트리거]**: 겨울 폭풍이나 태풍 경고 등 악천후 기상 경고.

## 전제 조건 {#prerequisites}

날씨 데이터를 사용하기 전에 다음 전제 조건을 충족하는지 확인합니다.

* [!DNL The Weather Channel]에서 사용할 날씨 데이터에 라이선스를 부여해야 합니다. 그러면 계정에서 활성화됩니다.
* 날씨 데이터는 데이터스트림을 통해서만 사용할 수 있습니다. 날씨 데이터를 사용하려면 [!DNL Web SDK], [!DNL Mobile Edge Extension] 또는 [서버 API](../../server-api/overview.md)를 사용하여 이 데이터를 활용해야 합니다.
* 데이터스트림에서 [[!UICONTROL 지리적 위치]](../configure.md#advanced-options)를 활성화해야 합니다.
* 사용 중인 스키마에 [날씨 필드 그룹](#schema-configuration)을 추가합니다.

## 프로비저닝 {#provisioning}

[!DNL The Weather Channel]에서 데이터에 라이선스가 부여되면 계정을 활성화하여 데이터에 액세스할 수 있습니다. 다음으로 데이터스트림에서 데이터를 활성화하려면 Adobe 고객 지원 센터에 문의하십시오. 활성화되면 데이터가 자동으로 추가됩니다.

[!DNL Edge Network]를 통해 히트를 추적하기 위해 디버거로 에지 추적을 실행하거나 Assurance를 사용하여 데이터가 추가되고 있는지 확인할 수 있습니다.

### 스키마 구성 {#schema-configuration}

데이터스트림에서 사용 중인 이벤트 데이터 세트에 해당하는 Experience Platform 스키마에 날씨 필드 그룹을 추가해야 합니다. 다섯 가지 필드 그룹을 사용할 수 있습니다.

* [!UICONTROL 날씨 예보]
* [!UICONTROL 현재 날씨]
* [!UICONTROL 제품 트리거]
* [!UICONTROL 상대적 트리거]
* [!UICONTROL 악천후 기상 트리거]

## 날씨 데이터에 액세스 {#access-weather-data}

데이터에 라이선스가 부여되고 데이터를 사용할 수 있으면 Adobe 서비스 전반에 걸쳐 다양한 방식으로 데이터에 액세스할 수 있습니다.

### Adobe Analytics {#analytics}

[!DNL Adobe Analytics]에서 날씨 데이터를 사용하여 처리 규칙을 통해 나머지 [!DNL XDM] 스키마와 함께 매핑할 수 있습니다.

[날씨 참조](weather-reference.md) 페이지에서 매핑할 수 있는 필드의 목록을 찾을 수 있습니다. 모두 [!DNL XDM] 스키마와 마찬가지로 키는 앞에 `a.x`가 붙습니다. 예: `weather.current.temperature.farenheit`라는 필드가 `a.x.weather.current.temperature.farenheit`로 [!DNL Analytics]에 표시됩니다.

![처리 규칙 인터페이스](../assets/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

데이터스트림에 지정된 데이터 세트의 [!DNL Adobe Customer Journey Analytics]에서 날씨 데이터를 사용할 수 있습니다. 날씨 속성이 [스키마에 추가](#prerequisites-prerequisites)되기만 하면 속성을 사용하여 [!DNL Customer Journey Analytics]의 [데이터 보기에 추가](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html)할 수 있습니다.

### Real-Time Customer Data Platform {#rtcdp}

날씨 데이터는 세그먼트에 사용할 [Real-Time Customer Data Platform](../../rtcdp/overview.md)에서 사용할 수 있습니다. 날씨 데이터는 이벤트에 첨부됩니다.

![날씨 이벤트를 표시하는 세그먼트 빌더](../assets/data-enrichment/weather/schema-builder.png)

기상 조건이 자주 변경되므로 위 예와 같이 세그먼트에 시간 제한을 설정하는 것이 좋습니다. 6개월 전 추운 날씨보다는 전날 또는 이틀 전 추운 날씨에 의해 휠씬 더 큰 영향을 받을 수 있습니다.

사용 가능한 필드는 [날씨 참조](weather-reference.md)를 참조하십시오.

### Adobe Target {#target}

[!DNL Adobe Target]에서 날씨 데이터를 사용하여 개인화를 실시간으로 추진할 수 있습니다. 날씨 데이터가 [!UICONTROL mbox] 매개변수로 [!DNL Target]에 전달되면 사용자 정의 [!UICONTROL mbox] 매개변수를 통해 액세스할 수 있습니다.

![타깃 대상자 빌더](../assets/data-enrichment/weather/target-audience-builder.png)

매개변수는 특정 필드에 대한 [!DNL XDM] 경로입니다. 사용 가능한 필드 및 해당 경로는 [날씨 참조](weather-reference.md)를 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 다양한 Adobe 솔루션에서 날씨 데이터를 사용하는 방법을 더 잘 이해할 수 있습니다. 날씨 데이터 필드 매핑에 대해 자세히 알아보려면 [필드 매핑 참조](weather-reference.md)를 참조하십시오.
