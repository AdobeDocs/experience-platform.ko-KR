---
title: 날씨 데이터 필드 매핑
description: 날씨 채널과의 통합의 일부로 사용할 수 있는 사용 가능한 날씨 데이터 필드에 대한 참조 페이지입니다.
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: e2122008fcae1016db03d6b5f56e4fa25520f9d0
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---

# 날씨 데이터 필드 매핑

Adobe은 [!DNL [The Weather Company]](https://www.ibm.com/weather) 데이터스트림을 통해 수집된 데이터에 미국 날씨의 추가 컨텍스트를 가져옵니다. Experience Platform에서 분석, 타기팅 및 세그먼트 생성에 이 데이터를 사용할 수 있습니다.

이 페이지에는 대상 데이터를 보강하는 데 사용할 수 있는 모든 필드가 나열됩니다.

필드는 필드 그룹에 맞는 세 개의 다른 그룹으로 나뉩니다.

* [**[!UICONTROL 현재 날씨]**](#current-weather): 위치를 기반으로 한 사용자의 현재 날씨 상태입니다. 여기에는 현재 온도, 섭취, 구름 범위 등이 포함됩니다.
* [**[!UICONTROL 예보된 날씨]**](#forecast): 예측에는 사용자 위치에 대한 1,2,3,5,7 및 10일 예측이 포함됩니다.
* [**[!UICONTROL 트리거]**](#triggers): 트리거는 서로 다른 의미 있는 날씨 조건에 매핑되는 특정 조합입니다. 세 가지 유형의 날씨 유발기가 있습니다.

   * **[!UICONTROL 상대 트리거]**: 추위나 비가 오는 날씨와 같이 의미상 의미 있는 상태. 이들은 다양한 기후 간에 그 정의가 다를 수 있다.
   * **[!UICONTROL 제품 트리거]**: 다양한 유형의 제품을 구매하는 조건입니다. 예를 들어, 추운 날씨 예보는 비 코트 구입이 더 가능성이 높다는 것을 의미할 수 있습니다.
   * **[!UICONTROL 악천후 유발인자]**: 겨울 폭풍 또는 허리케인 경고와 같은 심각한 기상 경고입니다.

## 현재 날씨 {#current-weather}

해당 위치를 기반으로 한 사용자의 현재 날씨 상태입니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL 섭씨 온도 노점] | 공기를 일정한 압력으로 냉각해야 포화상태에 도달하는 온도. 노점(Dew Point)은 또한 공기의 습도를 간접적으로 측정하는 것이다. 이슬점은 절대 온도를 넘지 않을 것이다. 이슬점과 온도가 같을 때 일반적으로 구름이나 안개가 형성됩니다. Temperature와 Dew Point의 값이 가까울수록 상대습도가 높아진다. 범위 - -80~100(°F) 또는 -62~37(°C). 섭씨 온도 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 화씨 온도 노점] | 공기를 일정한 압력으로 냉각해야 포화상태에 도달하는 온도. 노점(Dew Point)은 또한 공기의 습도를 간접적으로 측정하는 것이다. 이슬점은 절대 온도를 넘지 않을 것이다. 이슬점과 온도가 같을 때 일반적으로 구름이나 안개가 형성됩니다. Temperature와 Dew Point의 값이 가까울수록 상대습도가 높아진다. 범위 - -80~100(°F) 또는 -62~37(°C). 화씨 온도(도) | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 지난 시간(인치) 강수량] | 롤링 시간 액체 침전량. 제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 인치 단위 강수량 | `weather.current.precip1Hour.inches` |
| [!UICONTROL 지난 시간 밀리미터 강수량] | 롤링 시간 액체 침전량. 제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 밀리미터 단위 강수량 | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 24시간 액체 침전량 롤링. 제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 인치 단위 강수량 | `weather.current.precip24Hour.inches` |
| [!UICONTROL 지난 24시간 밀리미터 강수량] | 24시간 액체 침전량 롤링. 제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 밀리미터 단위 강수량 | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 지난 6시간 동안의 강수량] | 6시간 동안의 액체 침전량을 롤링합니다. 제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 인치 단위 강수량 | `weather.current.precip6Hour.inches` |
| [!UICONTROL 지난 6시간 밀리미터 강수량] | 6시간 동안의 액체 침전량을 롤링합니다. 제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 밀리미터 단위 강수량 | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 압력 변화] | 지난 3시간 동안 압력의 변화 밀리바. | `weather.current.pressureChange` |
| [!UICONTROL 평균 해수면 압력] | 평균 해수면압(밀리바)  즉, 해수면에서의 평균 기압이다.<br>범위 - 1/10mb로 정확합니다. | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 상대 습도] | 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.current.relativeHumidity` |
| [!UICONTROL 마지막 시간 센티미터 눈] | 1시간 적설량입니다.  제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 센티미터 단위 적설 | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 지난 1시간 동안의 눈] | 1시간 적설량입니다.  제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 적설량(인치) | `weather.current.snow1Hour.inches` |
| [!UICONTROL 눈 24 시간 센티미터] | 24시간 적설량입니다.  제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 센티미터 단위 적설 | `weather.current.snow24Hour.centimeters` |
| Snow 24 Hour Inches | 24시간 적설량입니다.  제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 적설량(인치) | `weather.current.snow24Hour.inches` |
| [!UICONTROL 눈이 6시간 센티미터 지속됨] | 1시간 적설량입니다.  제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 센티미터 단위 적설 | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 눈이 6시간 인치 지속됨] | 1시간 적설량입니다.  제시된 금액은 요청 시간 (지금)을 통한 롤링 시간입니다. 적설량(인치) | `weather.current.snow6Hour.inches` |
| [!UICONTROL 일몰 시간] | UTC로 종료 시간. | `weather.current.sunsetTime` |
| [!UICONTROL 섭씨 온도] | 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.current.temperature.celsius` |
| [!UICONTROL 화씨 온도] | 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 섭씨 24시간 온도 변화] | 24시간 전 보고서와 비교한 온도 변화. 섭씨 온도 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 화씨 24시간 온도 변화] | 24시간 전 보고서와 비교한 온도 변화. 화씨 온도(도) | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 온도는 섭씨처럼 느껴진다] | 명백한 온도. 이것은 공기 온도가 풍속 냉각 또는 열 지수의 결합 효과로 인해 노출된 인간의 피부에 &quot;느낌&quot; 을 나타냅니다.<br>온도가 65°F 이상이면 Feels Like 값은 계산된 열 지수를 나타냅니다.  온도가 65°F 미만이면 Feels Like 값은 계산된 풍속 냉각을 나타냅니다.<br>-140 ~ 140 범위. 섭씨 온도 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 온도는 화씨 같다] | 명백한 온도. 이것은 공기 온도가 풍속 냉각 또는 열 지수의 결합 효과로 인해 노출된 인간의 피부에 &quot;느낌&quot; 을 나타냅니다.<br>온도가 65°F 이상이면 Feels Like 값은 계산된 열 지수를 나타냅니다.  온도가 65°F 미만이면 Feels Like 값은 계산된 풍속 냉각을 나타냅니다.<br>-140 ~ 140 범위. 화씨 온도(도) | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 오전 7시 이후 최대 온도] | 현지 시간으로 오전 7시 이후 최대 온도. 섭씨 온도 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 화씨 오전 7시 이후 최대 온도] | 현지 시간으로 오전 7시 이후 최대 온도. 화씨 온도(도) | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 지난 24시간 섭씨 온도] | 지난 24시간 동안의 최소 온도입니다.  24시간 기간은 요청 시간(지금)을 참조합니다.  섭씨 온도 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 최소 온도 화씨 24시간 지난 시간] | 지난 24시간 동안의 최소 온도입니다.  24시간 기간은 요청 시간(지금)을 참조합니다.  화씨 온도(도) | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 풍향] | 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.current.windDirection` |
| [!UICONTROL 시속 돌풍 킬로미터] | 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 시속 돌풍 마일] | 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 시간당 풍속 킬로미터] | 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 시속 풍속 마일] | 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.current.windSpeed.milesPerHour` |

## 예보된 날씨 {#forecast}

특정 시점에 위치를 기반으로 한 사용자의 예측된 날씨.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 하루 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 하루 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 하루 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 하루 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 하루 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 1일 예측 야간 강수량 기회] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 1일, 밤 기온 예상 바람 화씨 쌀쌀해] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 1일 예보 야간 천둥 지수] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 1일 예측 야간 UV 지수] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 1일 예상 야간 풍향] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 제1일 예보 야간 바람 시속 킬로미터] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 1일 예상 야간 돌풍 마일/시간] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 1일 예상 야간 풍속 킬로미터(시간당)] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 1일, 시간당 예상 야간 풍속 마일] | 하루 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 근무일 1 예측 QPF 인치] | 하루 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 1일 예측 QPF 밀리미터] | 하루 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 1일 예측 QPF 눈 센티미터] | 하루 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 1일 예측 QPF Snow Inches] | 하루 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 2일 예측 달력 일 온도 최대 섭씨] | 이틀 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 2일 예측 달력 일 기온 최대 화씨] | 이틀 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 2일 예측 달력 일별 온도(최소 섭씨)] | 이틀 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 2일 예측 달력 일 기온 최소 화씨] | 이틀 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 2일 예측 당일 클라우드 커버 마일] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 2일 예측 일별 클라우드 커버 킬로미터] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 근무일 2 예측 근무일 강수량 기회] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 근무일 2 예측 근무일 강수량 유형] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 근무일 2 예측 근무일 QPF 인치] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 2일 예측 일별 QPF 밀리미터] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 근무일 2 예측 근무일 QPF 눈 센티미터] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 근무일 2 예측 근무일 QPF 눈 인치] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 2일 예측 일별 상대 습도] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 근무일 2 예측 근무일 눈 범위] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 2일 예측 일 기온 섭씨] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 2일 예측 일 기온 화씨] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 2일 일기예보의 일 기온 열지수 섭씨] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 2일 일기예보의 일 기온 더위 지수 화씨] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 2일 일기예보에 따르면 일 기온 바람 쌀쌀한 섭씨] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 2일 일기 예보 일 기온 바람 화씨 온도] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 2일 예측 일광 천둥 지수] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 2일 예측 일별 UV 지수] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 2일 예측 일별 풍향] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 2일 예상 일광 돌풍 킬로미터(시간당)] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 2일 예측 일별 강풍 마일/시간] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 2일 예측 일별 풍속 킬로미터(시간당)] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 2일 예측 시간당 일별 풍속 마일] | 이틀 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 2일 예측 야간 클라우드 커버 마일] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 2일 예측 야간 구름 커버 킬로미터] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 2일 예측 야간 강수 기회] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 근무일 2 예측 야간 강수량 유형] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 2일 예측 야간 QPF 인치] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 2일 예측 밤 QPF 밀리미터] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 2일 예측 밤 QPF 눈 센티미터] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 2일 예측 밤 QPF 눈 인치] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 2일 예측 밤 상대 습도] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 2일 예상 야간 눈 범위] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 2일 예측 밤 기온 섭씨] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 2일 예상 밤 기온 화씨] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 2일 예측 밤 기온 열지수 섭씨] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 2일 예상 밤 기온 더위 지수: 화씨] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 2일 예보 밤 기온 바람 쌀쌀한 섭씨] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 2일 예보 밤 기온 바람 화씨 쌀쌀해] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 2일 예보 야간 천둥 지수] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 2일 예측 야간 UV 지수] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 2일 예보 야간 풍향] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 2일 예보 야간 바람 시속 킬로미터] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 2일 예보 야간 바람 시속 돌풍 마일] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 2일, 시간당 야간 풍속 킬로미터 예측] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 2일, 시간당 예상 야간 풍속 마일] | 이틀 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 근무일 2 예측 QPF 인치] | 이틀 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 2일 예측 QPF 밀리미터] | 이틀 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 2일 예측 QPF 눈 센티미터] | 이틀 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 근무일 2 예측 QPF Snow Inches] | 이틀 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 3일 예측 달력 일별 온도 최대 섭씨] | 3일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 3일 예측 달력 일 기온 최대 화씨] | 3일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 3일 예측 달력 일 온도(최소 섭씨)] | 3일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 3일 예측 달력 일 기온 최소 화씨] | 3일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 3일 예측 일별 클라우드 커버 마일] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 3일 예측 일별 클라우드 커버 킬로미터] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 근무일 3 예측 근무일 강수량 기회] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 근무일 3 예측 근무일 강수량 유형] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 근무일 3 예측 근무일 QPF 인치] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 3일 예측 일별 QPF 밀리미터] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 근무일 3 예측 근무일 QPF 눈 센티미터] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 근무일 3 예측 근무일 QPF 눈 인치] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 3일 예측 일별 상대 습도] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 근무일 3 예측 근무일 눈 범위] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 3일 예측 일 기온 섭씨] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 3일 예측 일 기온 화씨] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 3일 일기예보의 일 기온 열지수 섭씨] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 3일 예측 일별 기온 더위 지수 화씨] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 3일 일기예보에 따르면 일교차가 심한 날씨는 쌀쌀하다] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 3일 일기예보에 따르면 일 기온은 화씨 바람 쌀쌀해] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 제3일 예측 일광 천둥 지수] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 3일 예측 일별 UV 지수] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 3일 예측 일별 풍향] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 제3일 예측 일별 강풍 킬로미터(시간당)] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 3일 예측 일별 강풍 마일/시간] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 3일 예측 일별 풍속 킬로미터(시간당)] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 3일 예측 시간 당 일별 풍속 마일] | 3일 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 3일 예측 야간 클라우드 커버 마일] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 3일 예측 밤 구름 커버 킬로미터] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 3일 예측 야간 강수 기회] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 근무일 3 예측 야간 강수량 유형] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 3일 예측 야간 QPF 인치] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 3일 예측 밤 QPF 밀리미터] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 3일 예측 밤 QPF 눈 센티미터] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 3일 예측 밤 QPF 눈 인치] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 3일 예측 밤 상대 습도] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 3일 예상 야간 눈 범위] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 3일 예측 밤 기온 섭씨] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 3일 예상 밤 기온 화씨] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 3일 예측 밤 기온 열지수 섭씨] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 3일 예상 밤 기온 더위 지수: 화씨] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 3일 예보 밤 기온 바람 쌀쌀한 섭씨] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 3일날 밤 기온은 화씨 바람 쌀쌀을 예보한다] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 3일 예보 야간 천둥 지수] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 3일 예측 야간 UV 지수] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 3일 예보 야간 풍향] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 3일 예보 야간 바람 시속 킬로미터] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 제3일, 시간당 밤 바람 돌풍 마일 예보] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 3일 예상 야간 풍속 킬로미터(시간당)] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 3일, 시간당 예상 야간 풍속 마일] | 3일 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 근무일 3 예측 QPF 인치] | 3일 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 3일 예측 QPF 밀리미터] | 3일 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 근무일 3 예측 QPF 눈 센티미터] | 3일 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 근무일 3 예측 QPF Snow Inches] | 3일 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 5일 예측 달력 일별 온도 최대 섭씨] | 닷새 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 5일 예측 달력 일 기온 최대 화씨] | 닷새 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 5일 예측 달력 일별 온도(최소 섭씨)] | 닷새 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 5일 예측 달력 일 기온 최소 화씨] | 닷새 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 5일 예측 일별 클라우드 커버 마일] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 5일 예측 일별 클라우드 커버 킬로미터] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 근무일 5 예측 근무일 강수량 기회] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 근무일 5 예측 근무일 강수량 유형] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 근무일 5 예측 근무일 QPF 인치] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 5일 예측 일별 QPF 밀리미터] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 근무일 5 예측 근무일 QPF 눈 센티미터] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 근무일 5 예측 근무일 QPF 눈 인치] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 5일 예측 일별 상대 습도] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 근무일 5 예측 근무일 눈 범위] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 5일 예측 일 기온 섭씨] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 5일 예측 일 기온 화씨] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 5일 일기예보의 일 기온 열지수 섭씨] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 5일 일기예보의 일 기온 더위 지수 화씨] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 5일 일기예보에 따르면 일 기온은 바람 체감온도는 섭씨] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 5일 일기 예보 일 기온 바람 화씨 온도] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 5일 예측 일광 천둥 지수] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 5일 예측 일별 UV 지수] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 5일 예측 일별 풍향] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 5일 예측 일별 돌풍 킬로미터(시간당)] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 5일 예측 일별 돌풍 마일/시간] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 5일 예측 일별 풍속 킬로미터(시간당)] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 5일 예측 시간당 일별 풍속 마일] | 닷새 동안 일기 예보. 낮 시간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 5일 예측 야간 클라우드 커버 마일] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 5일 예측 야간 구름 커버 킬로미터] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 5일 예측 야간 강수 기회] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수가 있을 확률(백분율)입니다. | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 근무일 5 예측 야간 강수량 유형] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등) | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 5일 예측 야간 QPF 인치] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 5일 예측 밤 QPF 밀리미터] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 5일 예측 밤 QPF 눈 센티미터] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 5일 예측 밤 QPF 눈 인치] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 5일 예측 밤 상대 습도] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 공기의 상대 습도는 일정한 온도에서 공기를 포화시키는데 필요한 증기량에 대한 공기 중의 수증기량의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 5일 예상 야간 눈 범위] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 강설량(1-3&quot;, 3-6&quot; 등) | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 5일 예측 밤 기온 섭씨] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 5일 예상 밤 기온 화씨] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 정의된 UOM의 온도. -140 ~ 140 범위. 화씨 온도(도) | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 5일 예측 밤 기온 열지수 섭씨] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 제5일 예상 밤 기온 더위 지수: 화씨] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 습도에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 5일 예보 밤 기온 바람 쌀쌀한 섭씨] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 5일 일기 예보 밤 기온 바람 화씨 쌀쌀해] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도(도) | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 5일 예보 야간 천둥 지수] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 지역에 영향을 미치는 뇌우의 가능성 지표. 0(천둥 없음~5(심한 뇌우의 위험이 높음). | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 5일 예측 야간 UV 지수] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 5일 예보 야간 풍향] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람이 불어오는 자력 풍향은 도 단위로 표현된다. 자기적 방향은 0도에서 359도까지 다양하며, 여기서 0도는 북위, 90도는 동위, 180도는 남위, 270도는 서쪽을 가리킨다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350(10도 간격). | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 5일 예보 야간 바람 시속 킬로미터] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 5일 예보 야간 바람 시속 돌풍 마일] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 이 데이터 필드에는 평균 풍속의 갑작스럽고 일시적인 변화에 대한 정보가 포함됩니다. 이 보고서에는 관측 기간 동안 기록된 최대 풍속이 항상 표시됩니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍의 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있다. 시속 마일의 풍속 | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 제5일, 시간당 야간 풍속 킬로미터 예측] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 5일, 시간당 예상 야간 풍속 마일] | 닷새 동안 일기 예보. 야간 기간 동안의 날씨 정보. 바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 현재 조건에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 근무일 5 예측 QPF 인치] | 닷새 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 인치 단위 강수량 | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 5일 예측 QPF 밀리미터] | 닷새 동안 일기 예보. 12 또는 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위로 측정됩니다. 밀리미터 단위 강수량 | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 5일 예측 QPF 눈 센티미터] | 닷새 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 근무일 5 예측 QPF Snow Inches] | 닷새 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 7일 예측 달력 일 온도 최대 섭씨] | 7일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 근무일 7 예측 달력 근무일 기온 최대 화씨] | 7일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 7일 예측 달력 일 온도 최소 섭씨] | 7일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 근무일 7 예측 달력 근무일 기온 최소 화씨] | 7일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 7일 Forecast Cloud Cover 마일] | 7일 동안 일기 예보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 7일 예측 클라우드 커버 킬로미터] | 7일 동안 일기 예보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 근무일 7 예측 QPF 인치] | 7일 동안 일기 예보. 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 인치 단위 강수량 | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 7일 예측 QPF 밀리미터] | 7일 동안 일기 예보. 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위 강수량 | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 제7일 예보 QPF 적설센티미터] | 7일 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 근무일 7 예측 QPF 눈 인치] | 7일 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 7일 예측 UV 지수] | 7일 동안 일기 예보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 제7일 예상 풍향] | 7일 동안 일기 예보. 자기 표기법의 평균 풍향. | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 제7일 예상 풍속 킬로미터(시간당)] | 7일 동안 일기 예보. 12시간 예보 기간 동안의 최대 지속 풍속 예측.<br>바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 예보에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 제7일 예상 시속 풍속 마일] | 7일 동안 일기 예보. 12시간 예보 기간 동안의 최대 지속 풍속 예측.<br>바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 예보에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 근무일 10 예측 달력 근무일 온도 최대 섭씨] | 열흘간 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 근무일 10 예측 달력 근무일 기온 최대 화씨] | 열흘간 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 근무일 10 예측 달력 근무일 온도(최소 섭씨)] | 열흘간 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 근무일 10 예측 달력 근무일 기온 최소 화씨] | 열흘간 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 10일 예측 클라우드 적용 범위 마일] | 열흘간 일기 예보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 10일 예측 클라우드 커버 킬로미터] | 열흘간 일기 예보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 근무일 10 예측 QPF 인치] | 열흘간 일기 예보. 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 인치 단위 강수량 | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 근무일 10 예측 QPF 밀리미터] | 열흘간 일기 예보. 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위 강수량 | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 근무일 10 예측 QPF 눈 센티미터] | 열흘간 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 근무일 10 예측 QPF 눈 인치] | 열흘간 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 근무일 10 예측 UV 지수] | 열흘간 일기 예보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 10일 예상 풍향] | 열흘간 일기 예보. 자기 표기법의 평균 풍향. | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 근무일 10 예상 풍속 킬로미터(시간당)] | 열흘간 일기 예보. 12시간 예보 기간 동안의 최대 지속 풍속 예측.<br>바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 예보에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 근무일 10 시간당 예상 풍속 마일] | 열흘간 일기 예보. 12시간 예보 기간 동안의 최대 지속 풍속 예측.<br>바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 예보에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 근무일 14 예측 달력 근무일 온도 최대 섭씨] | 14일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 근무일 14 예측 달력 근무일 기온 최대 화씨] | 14일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최대 기온. 화씨 온도(도) | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 근무일 14 예측 달력 근무일 온도(최소 섭씨)] | 14일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 근무일 14 예측 달력 근무일 기온 최소 화씨] | 14일 동안 일기 예보. 지정된 날의 자정에서 자정까지의 일일 최소 기온. 화씨 온도(도) | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 14일 예측 클라우드 적용 범위 마일] | 14일 동안 일기 예보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 거리(마일). | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 제14일 수요예측 클라우드 커버 킬로미터] | 14일 동안 일기 예보. 주간 평균 클라우드 커버가 백분율로 표시됩니다. 킬로미터 단위입니다. | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 근무일 14 예측 QPF 인치 | 14일 동안 일기 예보. 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 인치 단위 강수량 | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 근무일 14 예측 QPF 밀리미터] | 14일 동안 일기 예보. 24시간 동안 예상되는 측정 가능한 강수량(액체 또는 액체와 동등). 밀리미터 단위 강수량 | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 근무일 14 예측 QPF 눈 센티미터] | 14일 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 센티미터 단위 적설 | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 근무일 14 예측 QPF Snow Inches] | 14일 동안 일기 예보. 예상 가능한 강수량은 12 또는 24시간 예보 기간 동안 눈으로 예상됩니다. 센티미터 단위로 측정됩니다. 적설량(인치) | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 근무일 14 예측 UV 지수] | 14일 동안 일기 예보. 12시간 예측 기간의 최대 UV 지수. | `weather.forecast.day14Forecast.uvIndex` |
| 14일 예상 풍향 | 14일 동안 일기 예보. 자기 표기법의 평균 풍향. | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 제14일 예상 풍속 킬로미터(시간당)] | 14일 동안 일기 예보. 12시간 예보 기간 동안의 최대 지속 풍속 예측.<br>바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 예보에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 킬로미터 단위 풍속 | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 제14일 예상 시속 풍속 마일] | 14일 동안 일기 예보. 12시간 예보 기간 동안의 최대 지속 풍속 예측.<br>바람은 벡터로 취급되므로 바람은 방향과 크기(속도)를 가져야 한다. 예보에서 보고된 바람 정보는 지속 풍속이라 불리는 10분 평균에 해당한다. 풍속의 갑작스러운 또는 짧은 변화는 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 북풍이 북쪽에서 남쪽으로 분다는 의미로 항상 &#39;바람이 부는 곳부터&#39;라고 표현한다. 북풍을 타고 북쪽을 향하면 바람이 바로 얼굴을 향한다. 남쪽을 바라보면 북풍이 등을 향해 있다. 시속 마일의 풍속 | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 트리거 {#triggers}

트리거들은 다양한 입력들에 기초하여 의미론적 기상 조건을 정의한다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL 제품 트리거] | 특정 범주의 제품에 대한 판매를 유도하는 데 적합한 조건을 나타냅니다.  이 매개 변수는 정수 값으로 매핑됩니다. IBM에서 전체 목록을 가져올 수 있습니다. | `weather.productTriggers` |
| [!UICONTROL 상대적 트리거] | 인간의 지각에 근거한 상대적 조건. 덥거나 추운 것 같아요 이 매개 변수는 정수 값으로 매핑됩니다. IBM에서 전체 목록을 가져올 수 있습니다. | `weather.relativeTriggers` |
| [!UICONTROL 악천후 유발인자] | 허리케인이나 과도한 비와 같은 다양한 악천후를 나타냅니다. | `weather.severeTriggers` |
