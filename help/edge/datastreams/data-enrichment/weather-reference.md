---
title: 날씨 데이터 필드 매핑
description: 날씨 채널 통합의 일부로 사용할 수 있는 사용 가능한 날씨 데이터 필드에 대한 참조 페이지입니다.
source-git-commit: 3e5ca8fe67e5ad9ce0fe70d0c9f1e2fbc20cee17
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---


# 날씨 데이터 필드 매핑

Adobe이 [!DNL [The Weather Company]](https://www.ibm.com/weather) 미국의 추가적인 날씨 상황을 데이터 저장소를 통해 수집된 데이터로 가져오기. 이 데이터를 Experience Platform에서 분석, 타깃팅 및 세그먼트 만들기에 사용할 수 있습니다.

이 페이지에는 대상 데이터를 보강하는 데 사용할 수 있는 모든 필드가 나와 있습니다.

필드는 필드 그룹에 맞게 세 개의 서로 다른 그룹으로 분할됩니다.

* [**[!UICONTROL 현재 날씨]**](#current-weather): 사용자의 위치를 기반으로 하는 사용자의 현재 날씨 조건입니다. 여기에는 현재 온도, 후두부, 구름 범위 등이 포함됩니다.
* [**[!UICONTROL 예측 날씨]**](#forecast): 수요예측에는 사용자 위치에 대한 1,2,3,5,7 및 10일 예측이 포함됩니다.
* [**[!UICONTROL Triggers]**](#triggers): 트리거는 다양한 시맨틱 날씨 조건에 매핑되는 특정 조합입니다. 3가지 다른 유형의 날씨 트리거가 있습니다.

   * **[!UICONTROL 상대 트리거]**: 추위나 장마와 같은 의미상 의미 있는 상황. 이것들은 다양한 기후들 사이의 그들의 정의에서 다를 수 있습니다.
   * **[!UICONTROL 제품 트리거]**: 여러 유형의 제품을 구매하는 원인이 되는 조건. 예: 혹한기 예보는 우천 구입이 더 가능성이 높다는 것을 의미할 수 있다.
   * **[!UICONTROL 악천후]**: 겨울 폭풍이나 허리케인 경고와 같은 심각한 기상 경보.

## 현재 날씨 {#current-weather}

사용자의 위치를 기반으로 하는 사용자의 현재 날씨 조건입니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL 온도 이슬점 섭씨] | 공기가 일정한 압력으로 냉각되어야 포화상태에 도달한다. 이슬점은 또한 공기의 습도를 간접적으로 측정하는 것입니다. 이슬점은 온도를 절대 초과할 수 없다. 기온과 온도가 같으면 보통 구름이나 안개가 형성됩니다. 온도 및 이슬점 값이 가까울수록 상대 습도가 높아집니다. 범위 - -80~100(°F) 또는 -62~37(°C). 섭씨 온도 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 화씨 온도 이슬점] | 공기가 일정한 압력으로 냉각되어야 포화상태에 도달한다. 이슬점은 또한 공기의 습도를 간접적으로 측정하는 것입니다. 이슬점은 온도를 절대 초과할 수 없다. 기온과 온도가 같으면 보통 구름이나 안개가 형성됩니다. 온도 및 이슬점 값이 가까울수록 상대 습도가 높아집니다. 범위 - -80~100(°F) 또는 -62~37(°C). 화씨 온도 | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 지난 1시간 강수량] | 1시간 동안의 강수량. 제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 인치 강수량 | `weather.current.precip1Hour.inches` |
| [!UICONTROL 지난 한 시간 동안의 강수량] | 1시간 동안의 강수량. 제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 밀리미터 강수량 | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 24시간 동안의 강수량. 제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 인치 강수량 | `weather.current.precip24Hour.inches` |
| [!UICONTROL 지난 24시간 밀리미터 강수량] | 24시간 동안의 강수량. 제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 밀리미터 강수량 | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 지난 6시간 동안의 강수량] | 6시간 동안의 강수량. 제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 인치 강수량 | `weather.current.precip6Hour.inches` |
| [!UICONTROL 지난 6시간 동안의 강수량] | 6시간 동안의 강수량. 제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 밀리미터 강수량 | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 압력 변경] | 지난 3시간 동안의 밀리바 압력 변화. | `weather.current.pressureChange` |
| [!UICONTROL 압력 평균 해수면] | 해수면 압력(밀리바)을 의미합니다.  즉, 해수면의 평균 기압입니다.<br>범위 - 정확히 1/10번째 mb입니다. | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 상대 습도] | 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.current.relativeHumidity` |
| [!UICONTROL 지난 1시간 동안의 눈] | 1시간의 강설량입니다  제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 적설량 1cm | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 지난 1시간 동안의 눈] | 1시간의 강설량입니다  제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 적설량 | `weather.current.snow1Hour.inches` |
| [!UICONTROL 24시간 눈] | 24시간 강설량입니다  제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 적설량 1cm | `weather.current.snow24Hour.centimeters` |
| 24시간 눈 | 24시간 강설량입니다  제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 적설량 | `weather.current.snow24Hour.inches` |
| [!UICONTROL 지난 6시간 동안의 눈] | 1시간의 강설량입니다  제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 적설량 1cm | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 지난 6시간 동안의 눈] | 1시간의 강설량입니다  제공된 금액은 요청 시간(현재)을 경과하는 롤링 시간입니다. 적설량 | `weather.current.snow6Hour.inches` |
| [!UICONTROL 일몰 시간] | UTC의 석양 시간입니다. | `weather.current.sunsetTime` |
| [!UICONTROL 온도 섭씨] | 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.current.temperature.celsius` |
| [!UICONTROL 화씨 온도] | 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 섭씨 24시간 온도 변화] | 24시간 전 보고서와 비교하여 온도 변화. 섭씨 온도 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 화씨 24시간 온도 변화] | 24시간 전 보고서와 비교하여 온도 변화. 화씨 온도 | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 온도가 섭씨 같다] | 외관상 온도. 찬 바람이나 열 지수의 결합효과에 의해 노출된 피부에서 대기온도가 어떻게 느껴지는지를 나타내는 것이다.<br>온도가 65°F 이상이면 Feel Like 값은 계산된 열 지수를 나타냅니다.  온도가 65°F보다 낮을 때 Feel Like 값은 계산된 Fill 을 나타냅니다.<br>범위 -140~140. 섭씨 온도 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 온도가 화씨 같다] | 외관상 온도. 찬 바람이나 열 지수의 결합효과에 의해 노출된 피부에서 대기온도가 어떻게 느껴지는지를 나타내는 것이다.<br>온도가 65°F 이상이면 Feel Like 값은 계산된 열 지수를 나타냅니다.  온도가 65°F보다 낮을 때 Feel Like 값은 계산된 Fill 을 나타냅니다.<br>범위 -140~140. 화씨 온도 | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 섭씨 7시부터 최대 온도] | 현지 시간으로 오전 7시 이후의 최대 온도. 섭씨 온도 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 화씨 7시 이후 최대 온도] | 현지 시간으로 오전 7시 이후의 최대 온도. 화씨 온도 | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 최근 24시간 온도 최소값] | 지난 24시간 동안의 최소 온도.  24시간 기간은 요청 시간(지금)을 참조합니다.  섭씨 온도 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 지난 24시간 화씨 온도 최소] | 지난 24시간 동안의 최소 온도.  24시간 기간은 요청 시간(지금)을 참조합니다.  화씨 온도 | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 풍향] | 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.current.windDirection` |
| [!UICONTROL 시속 돌풍] | 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 시속 돌풍 마일] | 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 시속 풍속 킬로미터] | 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 시속 풍속 마일즈] | 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.current.windSpeed.milesPerHour` |

## 예측 날씨 {#forecast}

특정 시점의 위치를 기반으로 사용자에 대한 예측 기상입니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 일기예보는 하루. 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 일기예보는 하루. 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 일기예보는 하루. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 일기예보는 하루. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 일기예보는 하루. 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 일기예보는 하루. 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 일기예보는 하루. 낮 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 일기예보는 하루. 낮 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 일기예보는 하루. 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 일기예보는 하루. 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 일기예보는 하루. 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 일기예보는 하루. 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 일기예보는 하루. 낮 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 일기예보는 하루. 낮 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 일기예보는 하루. 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 일기예보는 하루. 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 일기예보는 하루. 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 일기예보는 하루. 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 일기예보는 하루. 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 일기예보는 하루. 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 일기예보는 하루. 낮 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 일기예보는 하루. 낮 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 일기예보는 하루. 낮 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 일기예보는 하루. 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 일기예보는 하루. 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 일기예보는 하루. 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 일기예보는 하루. 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 일기예보는 하루. 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 일기예보는 하루. 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 1일 예상 야간 강수 가능성] | 일기예보는 하루. 한밤 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 일기예보는 하루. 한밤 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 일기예보는 하루. 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 일기예보는 하루. 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 일기예보는 하루. 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 일기예보는 하루. 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 일기예보는 하루. 한밤 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 일기예보는 하루. 한밤 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 일기예보는 하루. 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 일기예보는 하루. 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 일기예보는 하루. 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 일기예보는 하루. 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 일기예보는 하루. 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 1일 예측 야간 온도 풍속 추위 화씨] | 일기예보는 하루. 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 1일 수요예측 야간 천둥지수] | 일기예보는 하루. 한밤 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 1일 예측 야간 UV 색인] | 일기예보는 하루. 한밤 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 1일 예측 야간 바람 방향] | 일기예보는 하루. 한밤 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 1일날 저녁 돌풍 시속] | 일기예보는 하루. 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 1일 예상 시속 돌풍] | 일기예보는 하루. 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 1일 예상 풍속 시속 킬로미터] | 일기예보는 하루. 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 1일 예상 야간 풍속 시속 마일] | 일기예보는 하루. 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 1일 예측 QPF 인치] | 일기예보는 하루. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 1일 예측 QPF 밀리미터] | 일기예보는 하루. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 1일 예측 QPF 눈길 센티미터] | 일기예보는 하루. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 1일 예측 QPF 눈 인치] | 일기예보는 하루. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 2일 예측 달력 일별 온도 최대 섭씨] | 일기예보는 이틀 정도. 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 2일 예측 달력 일 온도 최대 화씨] | 일기예보는 이틀 정도. 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 2일 예측 달력 일 온도 최소값] | 일기예보는 이틀 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 2일 예측 달력 일 온도 최소 화씨] | 일기예보는 이틀 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 2일 수요예측 일일 클라우드 덮개 마일] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 2일 수요예측 일일 클라우드 커버 킬로미터] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 2일 예상 강수량 기회] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 2일 예측 강수량 유형] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 2일 수요예측 일자 QPF 인치] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 2일 수요예측 일자 QPF 밀리미터] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 2일 예측 일자 QPF 눈 센티미터] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 2일 수요예측 일자 QPF 눈 인치] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 2일 예측 일수 상대 습도] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 2일 수요예측 일일 눈 범위] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 2일 예측 일 온도 섭씨] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 2일 예측 일별 온도 화씨] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 2일 수요예측 일일 온도 열 지수 섭씨] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 2일 수요예측 일별 온도 열 지수 화씨] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 2일 예측 일온풍속 냉각] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 2일 예측 일 온도 풍속 냉각 화씨] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 2일 수요예측 일일 천둥지수] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 2일 수요예측 일자 UV 색인] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 2일 수요예측 일일 바람 방향] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 2일 예보 일일 돌풍 시속] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 2일 수요예측 일일 돌풍 시속 마일] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 2일 예상 일별 풍속 킬로미터] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 2일 수요예측 일일 풍속 시속 마일] | 일기예보는 이틀 정도. 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 2일 Forecast Night Cloud Cover Miles] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 2일 수요예측 야간 클라우드 커버 킬로미터] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 2일 예상 야간 강수량 기회] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 2일 예측 야간 강수량 유형] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 2일 수요예측 야간 QPF 인치] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 2일 예상 야간 QPF 밀리미터] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 2일 예상 야간 QPF 눈 센티미터] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 2일 예상 야간 QPF 눈 인치] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 2일 예측 야간 상대 습도] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 2일 예상 야간 눈 범위] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 2일 예상 야간 온도 섭씨] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 2일 예측 야간 온도 화씨] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 2일 예측 야간 온도 열 지수] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 2일 예측 야간 온도 열 지수 화씨] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 2일 예상 저녁 온도 풍속 냉각] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 2일 예측 야간 온도 풍속 추위 화씨] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 2일 수요예측 야간 천둥지수] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 2일 예측 야간 UV 지수] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 2일 예측 야간 바람 방향] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 2일 예측 시속 돌풍] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 2일 예상 시속 강풍] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 2일 예상 시속 풍속 킬로미터] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 2일 예상 야간 풍속 시속 마일] | 일기예보는 이틀 정도. 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 2일 예측 QPF 인치] | 일기예보는 이틀 정도. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 2일 예측 QPF 밀리미터] | 일기예보는 이틀 정도. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 2일 예측 QPF 눈길 센티미터] | 일기예보는 이틀 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 2일 예측 QPF 눈 인치] | 일기예보는 이틀 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 3일 예측 달력 일별 온도 최대 섭씨] | 3일 동안 일기예보가 있습니다 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 3일 예측 달력 일 온도 최대 화씨] | 3일 동안 일기예보가 있습니다 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 3일 예측 달력 일 온도 최소값] | 3일 동안 일기예보가 있습니다 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 3일 예측 달력 일별 온도 최소 화씨] | 3일 동안 일기예보가 있습니다 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 3일 수요예측 일일 클라우드 덮개 마일] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 3일 수요예측 일일 클라우드 커버 킬로미터] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 3일 예상 강수량 기회] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 3일 예측 강수량 유형] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 3일 수요예측 일자 QPF 인치] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 3일 수요예측 일자 QPF 밀리미터] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 3일 예측 일자 QPF 눈 센티미터] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 3일 수요예측 일자 QPF 눈 인치] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 3일 예측 일수 상대 습도] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 3일 수요예측 일일 눈 범위] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 3일 예측 근무일 온도 섭씨] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 3일 예측 일별 온도 화씨] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 3일 수요예측 일일 온도 열 지수] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 3일 수요예측 일별 온도 열 지수 화씨] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 3일 예측 일온풍속 냉각] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 3일 예측 일 온도 풍속 냉각 화씨] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 3일 수요예측 일일 천둥지수] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 3일 수요예측 일자 UV 색인] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 3일 수요예측 일일 바람 방향] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 3일 예보 강풍 시속] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 3일 수요예측 일일 돌풍 시속 마일] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 3일 수요예측 일일 풍속 시속 킬로미터] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 3일 수요예측 일일 풍속 시속 마일] | 3일 동안 일기예보가 있습니다 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 3일 Forecast Night Cloud Cover Miles] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 3일 수요예측 야간 구름 덮개 킬로미터] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 3일 예상 야간 강수 가능성] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 3일 예측 야간 강수량 유형] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 3일 수요예측 야간 QPF 인치] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 3일 예상 야간 QPF 밀리미터] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 3일 예상 야간 QPF 눈 센티미터] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 3일 예상 야간 QPF 눈 인치] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 3일 예측 야간 상대 습도] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 3일 예측 야간 눈 범위] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 3일 예상 야간 온도] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 3일 예측 야간 온도 화씨] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 3일 수요예측 야간 온도 열지수] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 3일 예측 야간 온도 열 지수 화씨] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 3일 예상 야간 기온 풍속 냉각] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 3일 예측 야간 온도 풍속 추위 화씨] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 3일 수요예측 야간 천둥지수] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 3일 예측 야간 UV 지수] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 3일 예측 야간 바람 방향] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 3일 예상 시속 강풍] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 3일 예상 시속 돌풍] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 3일 예상 시속 풍속 킬로미터] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 3일 예상 야간 풍속 시속 마일] | 3일 동안 일기예보가 있습니다 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 3일 예측 QPF 인치] | 3일 동안 일기예보가 있습니다 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 3일 예측 QPF 밀리미터] | 3일 동안 일기예보가 있습니다 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 3일 예측 QPF 눈길 센티미터] | 3일 동안 일기예보가 있습니다 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 3일 예측 QPF 눈 인치] | 3일 동안 일기예보가 있습니다 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 5일 예측 달력 일별 온도 최대 섭씨] | 일기예보는 5일 정도. 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 5일 예측 달력 일 온도 최대 화씨] | 일기예보는 5일 정도. 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 5일 예측 달력 일 온도 최소값] | 일기예보는 5일 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 5일 예측 달력 일 온도 최소 화씨] | 일기예보는 5일 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 5일 수요예측 일일 클라우드 덮개 마일] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 5일 수요예측 일일 클라우드 덮개 킬로미터] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 5일 예상 강수량 기회] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 5일 예측 강수량 유형] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 5일 수요예측 일자 QPF 인치] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 근무일 5 수요예측 일자 QPF 밀리미터] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 5일 예측 일자 QPF 눈 센티미터] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 근무일 5 수요예측 일자 QPF 눈 인치] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 5일 예측 일수 상대 습도] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 5일 수요예측 일일 눈 범위] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 5일 예측 근무일 온도 섭씨] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 5일 예측 일별 온도 화씨] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 5일 수요예측 일일 온도 열 지수 섭씨] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 5일 수요예측 일일 온도 열 지수 화씨] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 5일 예상 일온풍속 냉각] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 5일 예측 일 온도 풍속 냉각 화씨] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 5일 수요예측 일일 천둥지수] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 5일 수요예측 일자 UV 색인] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 5일 수요예측 일일 바람 방향] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 5일 예보 일일 돌풍 시속] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 5일 예상 일별 돌풍 시속] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 5일 수요예측 일일 풍속 시속 킬로미터] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 5일 수요예측 일일 풍속 시속 마일] | 일기예보는 5일 정도. 낮 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 5일 예측 야간 구름 덮개 마일] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 5일 수요예측 야간 클라우드 커버 킬로미터] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 5일 예상 야간 강수 가능성] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 강수량이 있을 가능성(퍼센트). | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 5일 예측 야간 강수량 유형] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 떨어질 수 있는 강수량(비, 눈, 진눈깨비 등). | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 5일 수요예측 야간 QPF 인치] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 5일 예상 야간 QPF 밀리미터] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 5일 예상 야간 QPF 눈 센티미터] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 5일 예상 야간 QPF 눈 인치] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 5일 예측 야간 상대 습도] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 공기의 상대습도는 공기의 수증기 양과 일정한 온도에서 공기의 포화를 위하여 필요한 수증기의 양의 비율로 정의된다. 상대 습도는 항상 백분율로 표시됩니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 5일 예상 야간 눈 범위] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 잠재적 적설량(1-3형, 3-6형 등) 버킷 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 5일 예상 야간 온도] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 5일 예측 야간 온도 화씨] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 정의된 측정 단위 온도. 범위 -140~140. 화씨 온도 | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 5일 예측 야간 온도 열 지수] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 5일 예측 야간 온도 열 지수 화씨] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 사람이 체감하는 온도와 습도에 따라 체온을 재는 것이다. 화씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 5일 예상 저녁 온도 풍속 냉각] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 화씨 5일 예상 야간온도 풍속] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 온도와 풍속에 따라 노출된 사람에게 느낄 수 있는 온도. 화씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 5일 수요예측 야간 천둥지수] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 뇌우가 한 지역에 영향을 줄 가능성에 대한 지표입니다. 0(천둥 없음 - 5(심한 뇌우 발생 위험) | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 5일 예측 야간 UV 지수] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 5일 예상 야간 풍향] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 바람이 불었던 자성 풍향은 각도로 표시된다. 자기장 방향은 0도에서 359도이고, 여기서 0°은 북한, 동쪽은 90°, 남쪽은 180°, 서쪽은 270°.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10도 간격. | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 5일 예상 풍광은 시속] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 시속 몇 km의 풍속 | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 5일 예상 시속 돌풍] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 이 데이터 필드에는 평균 풍속의 갑작스런 및 일시적인 변화에 대한 정보가 포함되어 있습니다. 이 보고는 항상 관측 기간 동안 기록된 최대 돌풍 속도를 보여줍니다. 풍속이 표시되는 경우 필수 표시 필드입니다. 돌풍 속도는 시속 몇 마일이나 시속 몇 km로 표시된다. 풍속(시속 마일) | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 5일 예상 풍속 시속 킬로미터] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 5일 예상 야간 풍속 시속 마일] | 일기예보는 5일 정도. 한밤 동안의 기상 정보. 바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 현재 상황에서 보고된 바람 정보는 지속 풍속이라고 불리는 10분 평균에 해당합니다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 5일 예측 QPF 인치] | 일기예보는 5일 정도. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 인치 강수량 | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 5일 예측 QPF 밀리미터] | 일기예보는 5일 정도. 12시간 또는 24시간 동안 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 단위로 측정되었습니다. 밀리미터 강수량 | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 5일 예상 QPF 눈길 센티미터] | 일기예보는 5일 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 5일 예측 QPF 눈 인치] | 일기예보는 5일 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 7일 예측 달력 일별 온도 최대 섭씨] | 일기예보는 7일 정도. 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 7일 예측 달력 일 온도 최대 화씨] | 일기예보는 7일 정도. 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 7일 예측 달력 일 온도 최소값] | 일기예보는 7일 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 7일 예측 달력 일 온도 최소 화씨] | 일기예보는 7일 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 7일 Forecast Cloud Cover Miles] | 일기예보는 7일 정도. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 7일 예측 클라우드 커버 킬로미터] | 일기예보는 7일 정도. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 7일 예측 QPF 인치] | 일기예보는 7일 정도. 24시간 동안의 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 인치 강수량 | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 7일 예측 QPF 밀리미터] | 일기예보는 7일 정도. 24시간 동안의 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 강수량 | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 7일 예상 QPF 눈길 센티미터] | 일기예보는 7일 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 7일 예측 QPF 눈 인치] | 일기예보는 7일 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 7일 예측 UV 색인] | 일기예보는 7일 정도. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 7일 예측 풍향] | 일기예보는 7일 정도. 자성 표기법의 평균 바람 방향. | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 7일 예상 시속 풍속 킬로미터] | 일기예보는 7일 정도. 12시간 예측 기간 동안 최대 지속 풍속의 예측.<br>바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 일기예보에서 보고된 바람 정보는 10분간의 평균치에 해당하는 지속 풍속이라고 한다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 7일 예상 풍속 시속 마일] | 일기예보는 7일 정도. 12시간 예측 기간 동안 최대 지속 풍속의 예측.<br>바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 일기예보에서 보고된 바람 정보는 10분간의 평균치에 해당하는 지속 풍속이라고 한다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 10일 예측 달력 일 온도 최대 섭씨] | 일기예보는 10일 정도. 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 10일 예측 달력 일 온도 최대 화씨] | 일기예보는 10일 정도. 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 10일 예측 달력 일 온도 최소값] | 일기예보는 10일 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 10일 예측 달력 일별 온도 최소 화씨] | 일기예보는 10일 정도. 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 10일 Forecast Cloud Cover Miles] | 일기예보는 10일 정도. 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 10일 예측 클라우드 커버 킬로미터] | 일기예보는 10일 정도. 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 10일 예측 QPF 인치] | 일기예보는 10일 정도. 24시간 동안의 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 인치 강수량 | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 10일 예측 QPF 밀리미터] | 일기예보는 10일 정도. 24시간 동안의 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 강수량 | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 10일 예상 QPF 눈길 센티미터] | 일기예보는 10일 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 10일 예측 QPF 눈 인치] | 일기예보는 10일 정도. 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 10일 예측 UV 색인] | 일기예보는 10일 정도. 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 10일 예측 풍향] | 일기예보는 10일 정도. 자성 표기법의 평균 바람 방향. | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 10일 예상 시속 풍속 킬로미터] | 일기예보는 10일 정도. 12시간 예측 기간 동안 최대 지속 풍속의 예측.<br>바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 일기예보에서 보고된 바람 정보는 10분간의 평균치에 해당하는 지속 풍속이라고 한다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 10일 예상 풍속 시속 마일] | 일기예보는 10일 정도. 12시간 예측 기간 동안 최대 지속 풍속의 예측.<br>바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 일기예보에서 보고된 바람 정보는 10분간의 평균치에 해당하는 지속 풍속이라고 한다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 14일 예측 달력 일 온도 최대 섭씨] | 14일 동안 일기예보가 있습니다 자정~자정, 지정된 날의 최대 온도. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 14일 예측 달력 일 온도 최대 화씨] | 14일 동안 일기예보가 있습니다 자정~자정, 지정된 날의 최대 온도. 화씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 14일 예측 달력 일 온도 최소값] | 14일 동안 일기예보가 있습니다 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 14일 예측 달력 일별 온도 최소 화씨] | 14일 동안 일기예보가 있습니다 자정부터 자정까지가 지정된 날의 매일 최소 기온입니다. 화씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 14일 Forecast Cloud Cover Miles] | 14일 동안 일기예보가 있습니다 백분율로 표현된 낮 평균 클라우드 커버. 거리(마일). | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 14일 예측 클라우드 커버 킬로미터] | 14일 동안 일기예보가 있습니다 백분율로 표현된 낮 평균 클라우드 커버. 거리. | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 14일 예측 QPF 인치 | 14일 동안 일기예보가 있습니다 24시간 동안의 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 인치 강수량 | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 14일 예측 QPF 밀리미터] | 14일 동안 일기예보가 있습니다 24시간 동안의 측정 가능한 강수량(액체 또는 이에 상응하는 액체)이 예측되었습니다. 밀리미터 강수량 | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 14일 예상 QPF 눈 센티미터] | 14일 동안 일기예보가 있습니다 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 1cm | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 14일 예측 QPF 눈 인치] | 14일 동안 일기예보가 있습니다 12시간 또는 24시간 예측 기간 동안 측정 가능한 강수량이 눈으로 예측되었다. 센티미터 단위로 측정됩니다. 적설량 | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 14일 예측 UV 색인] | 14일 동안 일기예보가 있습니다 12시간 예측 기간의 최대 UV 인덱스입니다. | `weather.forecast.day14Forecast.uvIndex` |
| 14일 예측 풍향 | 14일 동안 일기예보가 있습니다 자성 표기법의 평균 바람 방향. | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 14일 예상 시속 풍속 킬로미터] | 14일 동안 일기예보가 있습니다 12시간 예측 기간 동안 최대 지속 풍속의 예측.<br>바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 일기예보에서 보고된 바람 정보는 10분간의 평균치에 해당하는 지속 풍속이라고 한다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 시속 몇 km의 풍속 | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 14일 예상 시속 풍속 마일즈] | 14일 동안 일기예보가 있습니다 12시간 예측 기간 동안 최대 지속 풍속의 예측.<br>바람은 벡터로 처리된다. 따라서 바람은 방향과 강도(속도)가 있어야 한다. 일기예보에서 보고된 바람 정보는 10분간의 평균치에 해당하는 지속 풍속이라고 한다. 풍속의 갑작스런 또는 짧은 변형은 &quot;돌풍&quot;이라고 알려져 있으며 별도의 데이터 필드에 보고됩니다. 풍향은 늘 북풍이 불기 때문에 풍향으로 표현돼 있다. 북풍이 불 때 북쪽을 바라보면 바람이 얼굴에 분다. 남쪽으로 향하면 북풍이 등 있어요 풍속(시속 마일) | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 트리거 {#triggers}

트리거는 다양한 입력을 기반으로 시맨틱 날씨 조건을 정의합니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL 제품 트리거] | 특정 제품 카테고리에 대한 판매 촉진을 위한 조건이 적합한 시기를 나타냅니다.  정수 항목에 매핑됩니다. 전체 목록은 IBM에서 확인할 수 있습니다. | `weather.productTriggers` |
| [!UICONTROL 상대 트리거] | 인간의 인식에 따른 상대적인 조건. 뜨겁거나 차갑거나 정수 항목에 매핑됩니다. 전체 목록은 IBM에서 확인할 수 있습니다. | `weather.relativeTriggers` |
| [!UICONTROL 악천후] | 허리케인이나 과도한 비와 같은 다양한 악천후 상태를 나타냅니다. | `weather.severeTriggers` |