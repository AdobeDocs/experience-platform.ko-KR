---
title: DNL The Weather Channel의 날씨 데이터 사용
description: DNL 날씨 채널의 날씨 데이터를 사용하여 데이터 저장소를 통해 수집하는 데이터를 향상시킵니다.
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# 의 날씨 데이터 사용 [!DNL The Weather Channel]

Adobe이 [!DNL [The Weather Company]](https://www.ibm.com/weather) 미국의 추가적인 날씨 상황을 데이터 저장소를 통해 수집된 데이터로 가져오기. 이 데이터를 Experience Platform에서 분석, 타깃팅 및 세그먼트 만들기에 사용할 수 있습니다.

사용할 수 있는 데이터에는 3가지 유형이 있습니다 [!DNL The Weather Channel]:

* **[!UICONTROL 현재 날씨]**: 사용자의 위치를 기반으로 하는 사용자의 현재 날씨 조건입니다. 여기에는 현재 온도, 후두부, 구름 범위 등이 포함됩니다.
* **[!UICONTROL 예측 날씨]**: 수요예측에는 사용자 위치에 대한 1,2,3,5,7 및 10일 예측이 포함됩니다.
* **[!UICONTROL Triggers]**: 트리거는 다양한 시맨틱 날씨 조건에 매핑되는 특정 조합입니다. 3가지 다른 유형의 날씨 트리거가 있습니다.

   * **[!UICONTROL 날씨 트리거]**: 추위나 장마와 같은 의미상 의미 있는 상황. 이것들은 다양한 기후들 사이의 그들의 정의에서 다를 수 있습니다.
   * **[!UICONTROL 제품 트리거]**: 여러 유형의 제품을 구매하는 원인이 되는 조건. 예: 혹한기 예보는 우천 구입이 더 가능성이 높다는 것을 의미할 수 있다.
   * **[!UICONTROL 악천후]**: 겨울 폭풍이나 허리케인 경고와 같은 심각한 기상 경보.

## 전제 조건 {#prerequisites}

날씨 데이터를 사용하기 전에 다음 사전 요구 사항을 충족하는지 확인하십시오.

* 사용할 날씨 데이터에 대한 라이선스를 받아야 합니다. [!DNL The Weather Channel]. 그러면 계정에서 사용하도록 설정됩니다.
* 날씨 데이터는 데이터 저장소를 통해서만 사용할 수 있습니다. 날씨 데이터를 사용하려면 다음을 사용해야 합니다 [!DNL Web SDK], [!DNL Mobile Edge Extension] 또는 [서버 API](../../../server-api/overview.md) 을 눌러 이 데이터를 활용합니다.
* 데이터 스트림에 [[!UICONTROL 지리적 위치]](../configure.md#advanced-options) 활성화되었습니다.
* 추가 [기상 단체](#schema-configuration) 를 사용 중인 스키마에 추가합니다.

## 프로비저닝 {#provisioning}

데이터 라이센스를 얻은 후 [!DNL The Weather Channel]로 설정되면 계정이 데이터에 액세스할 수 있게 됩니다. 다음으로, 데이터 스트림에 데이터를 활성화하려면 고객 지원 센터 Adobe에 문의해야 합니다. 활성화되면 데이터가 자동으로 추가됩니다.

디버거를 사용하여 Edge Trace를 실행하거나 Assurance를 사용하여 를 통해 히트를 추적하여 추가 중인지 확인할 수 있습니다. [!DNL Edge Network].

### 스키마 구성 {#schema-configuration}

데이터 스트림에서 사용하는 이벤트 데이터 세트에 해당하는 Experience Platform 스키마에 날씨 필드 그룹을 추가해야 합니다. 사용할 수 있는 필드 그룹은 5개입니다.

* [!UICONTROL 예측 날씨]
* [!UICONTROL 현재 날씨]
* [!UICONTROL 제품 트리거]
* [!UICONTROL 상대 트리거]
* [!UICONTROL 악천후]

## 날씨 데이터 액세스 {#access-weather-data}

데이터의 라이센스가 있고 사용 가능해지면 Adobe 서비스 전체에서 다양한 방법으로 데이터에 액세스할 수 있습니다.

### Adobe Analytics {#analytics}

in [!DNL Adobe Analytics]을 설정하는 경우 날씨 데이터를 나머지 데이터와 함께 처리 규칙을 통해 매핑할 수 있습니다 [!DNL XDM] 스키마.

여기에서 매핑할 수 있는 필드 목록을 찾을 수 있습니다 [날씨 참조](weather-reference.md) 페이지. 모든 경우의 [!DNL XDM] 스키마에는 키 접두사가 추가됩니다. `a.x`. 예를 들어 이름이 인 필드 `weather.current.temperature.farenheit` 이 경우 [!DNL Analytics] 로서의 `a.x.weather.current.temperature.farenheit`.

![처리 규칙 인터페이스](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

in [!DNL Adobe Customer Journey Analytics]를 설정하는 경우 날씨 데이터는 데이터 스트림에 지정된 데이터 세트에서 사용할 수 있습니다. 날씨 속성이 [스키마에 추가](#prerequisites-prerequisites), 다음 위치에서 사용할 수 있습니다. [데이터 보기에 추가](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

날씨 데이터는 [Real-time Customer Data Platform](../../../rtcdp/overview.md): 세그먼트에서 사용할 수 있습니다. 날씨 데이터가 이벤트에 첨부됩니다.

![날씨 이벤트를 보여주는 세그먼트 빌더](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

날씨 조건이 자주 변경되므로 위의 예와 같이 세그먼트에 시간 제한을 설정하는 것이 좋습니다. 6개월 전에 추운 날을 보내는 것보다 마지막 이틀 동안 추운 날을 갖는 것이 훨씬 더 효과적입니다.

자세한 내용은 [날씨 참조](weather-reference.md) 을 참조하십시오.

### Adobe Target {#target}

in [!DNL Adobe Target]을 사용하면 날씨 데이터를 사용하여 실시간으로 개인화를 유도할 수 있습니다. 날씨 데이터가 [!DNL Target] 로서의 [!UICONTROL mBox] 매개 변수 및 사용자 지정 [!UICONTROL mBox] 매개 변수.

![Target Audience Builder](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

매개 변수는 [!DNL XDM] 특정 필드의 경로입니다. 자세한 내용은 [날씨 참조](weather-reference.md) 사용 가능한 필드 및 해당 경로에 대해 설명합니다.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 다양한 Adobe 솔루션에서 날씨 데이터를 사용하는 방법을 더 잘 이해할 수 있습니다. 날씨 데이터 필드 매핑에 대한 자세한 내용은 [필드 매핑 참조](weather-reference.md).