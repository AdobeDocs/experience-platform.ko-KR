---
title: 날씨 데이터 필드 매핑
description: The Weather Channel 통합 기능의 일부로 제공되는 사용 가능한 날씨 데이터 필드에 대한 참조 페이지.
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '11147'
ht-degree: 99%

---

# 날씨 데이터 필드 매핑

Adobe는 데이터스트림을 통해 수집한 데이터에 미국 날씨에 대한 컨텍스트를 추가 제공하기 위해 [!DNL [The Weather Company]](https://www.ibm.com/weather)와(과) 파트너 관계를 맺고 있습니다. 이 데이터를 사용하여 Experience Platform에서 분석, 타겟팅 및 세그먼트 생성을 수행할 수 있습니다.

이 페이지에는 대상자 데이터를 보완하는 데 사용할 수 있는 모든 필드가 나열되어 있습니다.

필드는 필드 그룹에 맞춰 조정되는 세 가지 서로 다른 그룹으로 나뉩니다.

* [**[!UICONTROL Current Weather]**](#current-weather): 사용자의 위치에 따른 현재 날씨 상태입니다. 여기에는 현재 온도, 강수량, 전운량 등이 포함됩니다.
* [**[!UICONTROL Forecasted Weather]**](#forecast): 예측에는 사용자 위치에 대한 1,2,3,5,7 및 10일 예측이 포함됩니다.
* [**[!UICONTROL Triggers]**](#triggers): 트리거는 다양한 의미 기상 조건에 매핑되는 특정 조합입니다. 날씨 트리거에는 세 가지 유형이 있습니다.

   * **[!UICONTROL Relative Triggers]**: 춥거나 비가 오는 날씨와 같이 의미상 의미 있는 상태입니다. 이는 기후에 따라 정의가 달라질 수 있습니다.
   * **[!UICONTROL Product Triggers]**: 다른 유형의 제품을 구매하는 조건입니다. 예: 추운 날씨가 예보되면서 우비를 구매할 가능성이 높아질 수 있습니다.
   * **[!UICONTROL Severe Weather Triggers]**: 겨울 폭풍 또는 허리케인 경고와 같은 심각한 기상 경고입니다.

## 현재 날씨 {#current-weather}

해당 위치를 기준으로 한 사용자의 현재 기상 조건.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL Temperature Dew Point Celsius] | 일정한 압력으로 포화 상태에 도달하기 위한 공기 냉각 온도. 이슬점은 공기 습도를 간접적으로 측정하는 지표이기도 합니다. 이슬점은 온도를 초과하지 않습니다. 이슬점과 온도가 같으면 보통 구름 또는 안개가 형성됩니다. 온도 값이 이슬점 값에 가까워지면 상대 습도가 높아집니다. 범위 - -80~100(°F) 내지 -62~37(°C). 섭씨 온도 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL Temperature Dew Point Fahrenheit] | 일정한 압력으로 포화 상태에 도달하기 위한 공기 냉각 온도. 이슬점은 공기 습도를 간접적으로 측정하는 지표이기도 합니다. 이슬점은 온도를 초과하지 않습니다. 이슬점과 온도가 같으면 보통 구름 또는 안개가 형성됩니다. 온도 값이 이슬점 값에 가까워지면 상대 습도가 높아집니다. 범위 - -80~100(°F) 내지 -62~37(°C). 화씨 온도 | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL Precipitation Last Hour Inches] | 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(인치) | `weather.current.precip1Hour.inches` |
| [!UICONTROL Precipitation Last Hour Millimeters] | 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(밀리미터) | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 24시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(인치) | `weather.current.precip24Hour.inches` |
| [!UICONTROL Precipitation Last 24 Hours Millimeters] | 24시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(밀리미터) | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL Precipitation Last 6 Hours Inches] | 6시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(인치) | `weather.current.precip6Hour.inches` |
| [!UICONTROL Precipitation Last 6 Hours Millimeters] | 6시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(밀리미터) | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL Pressure Change] | 지난 3시간 동안의 기압 변화(밀리바). | `weather.current.pressureChange` |
| [!UICONTROL Pressure Mean Sea Level] | 평균 해수면 기압(밀리바). 다시 말해, 해수면의 평균 기압입니다.<br>범위 - 1/10mb(밀리바) 수준까지 정밀. | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL Relative Humidity] | 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.current.relativeHumidity` |
| [!UICONTROL Snow Last Hour Centimeters] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(센티미터) | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL Snow Last Hour Inches] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(인치) | `weather.current.snow1Hour.inches` |
| [!UICONTROL Snow 24 Hour Centimeters] | 24시간 롤링 시 강설 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(센티미터) | `weather.current.snow24Hour.centimeters` |
| 24시간 동안의 강설량(인치) | 24시간 롤링 시 강설 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(인치) | `weather.current.snow24Hour.inches` |
| [!UICONTROL Snow Last 6 Hours Centimeters] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(센티미터) | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL Snow Last 6 Hours Inches] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(인치) | `weather.current.snow6Hour.inches` |
| [!UICONTROL Sunset Time] | 일몰 시간(UTC) | `weather.current.sunsetTime` |
| [!UICONTROL Temperature Celsius] | 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.current.temperature.celsius` |
| [!UICONTROL Temperature Fahrenheit] | 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.current.temperature.fahrenheit` |
| [!UICONTROL Temperature Change 24 hour Celsius] | 24시간 전 보고서와 온도 변화 비교. 섭씨 온도 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL Temperature Change 24 hour Fahrenheit] | 24시간 전 보고서와 온도 변화 비교. 화씨 온도 | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL Temperature Feels Like Celsius] | 겉보기 온도. 겉보기 온도는 체감 온도나 열 지수 결합 효과로 인해 노출된 인체 피부에서 “체감”되는 기온을 나타냅니다.<br>온도가 65°F를 초과할 경우 체감 온도 값은 계산된 열 지수를 나타냅니다. 온도가 65°F 미만일 경우 체감 온도 값은 계산된 체감 온도를 나타냅니다.<br>범위 - 140~140. 섭씨 온도 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL Temperature Feels Like Fahrenheit] | 겉보기 온도. 겉보기 온도는 체감 온도나 열 지수 결합 효과로 인해 노출된 인체 피부에서 “체감”되는 기온을 나타냅니다.<br>온도가 65°F를 초과할 경우 체감 온도 값은 계산된 열 지수를 나타냅니다. 온도가 65°F 미만일 경우 체감 온도 값은 계산된 체감 온도를 나타냅니다.<br>범위 - 140~140. 화씨 온도 | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL Temperature Max Since 7 AM Celsius] | 오전 7시 이후 최대 온도(현지 시간). 섭씨 온도 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL Temperature Max Since 7 AM Fahrenheit] | 오전 7시 이후 최대 온도(현지 시간). 화씨 온도 | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL Temperature Min Last 24 Hours Celsius] | 지난 24시간 동안의 최저 온도. 24시간은 요청 기간(현재)을 기준으로 합니다. 섭씨 온도 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL Temperature Min Last 24 Hours Fahrenheit] | 지난 24시간 동안의 최저 온도. 24시간은 요청 기간(현재)을 기준으로 합니다. 화씨 온도 | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL Wind Direction] | 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.current.windDirection` |
| [!UICONTROL Wind Gust Kilometers per Hour] | 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL Wind Gust Miles per Hour] | 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.current.windGust.`시속 마일 |
| [!UICONTROL Wind Speed Kilometers per Hour] | 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL Wind Speed Miles per Hour] | 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.current.windSpeed.milesPerHour` |

## 날씨 예보 {#forecast}

특정 시점의 위치를 &#x200B;&#x200B;기준으로 사용자에게 제공되는 날씨 예보입니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 1일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 1일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 1일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 1일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 1일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 1일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 1일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 1일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 1일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 1일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 1일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 1일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 1일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 1일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 1일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 1일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 1일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 1일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 1일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 1일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 1일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 1일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 1일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 1일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 1일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 1일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 1일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 1일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 1일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 1 Forecast Night Precipitation Chance] | 1일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 1일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 1일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 1일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 1일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 1일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 1일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 1일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 1 Forecast Night Temperature Wind Chill Fahrenheit] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 1 Forecast Night Thunder Index] | 1일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL Day 1 Forecast Night UV Index] | 1일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL Day 1 Forecast Night Wind Direction] | 1일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL Day 1 Forecast Night Wind Gust Kilometers per Hour] | 1일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 1 Forecast Night Wind Gust Miles per Hour] | 1일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 1 Forecast Night Wind Speed Kilometers per Hour] | 1일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 1 Forecast Night Wind Speed Miles per Hour] | 1일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 1 Forecast QPF Inches] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL Day 1 Forecast QPF Millimeters] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL Day 1 Forecast QPF Snow Centimeters] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 1 Forecast QPF Snow Inches] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Max Celsius] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Max Fahrenheit] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Min Celsius] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Min Fahrenheit] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Cloud Cover Miles] | 2일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL Day 2 Forecast Day Cloud Cover Kilometers] | 2일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL Day 2 Forecast Day Precipitation Chance] | 2일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL Day 2 Forecast Day Precipitation Type] | 2일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL Day 2 Forecast Day QPF Inches] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL Day 2 Forecast Day QPF Millimeters] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL Day 2 Forecast Day QPF Snow Centimeters] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL Day 2 Forecast Day QPF Snow Inches] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL Day 2 Forecast Day Relative Humidity] | 2일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL Day 2 Forecast Day Snow Range] | 2일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL Day 2 Forecast Day Temperature Celsius] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL Day 2 Forecast Day Temperature Fahrenheit] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Temperature Heat Index Celsius] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 2 Forecast Day Temperature Heat Index Fahrenheit] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Temperature Wind Chill Celsius] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL Day 2 Forecast Day Temperature Wind Chill Fahrenheit] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Thunder Index] | 2일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL Day 2 Forecast Day UV Index] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL Day 2 Forecast Day Wind Direction] | 2일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL Day 2 Forecast Day Wind Gust Kilometers per Hour] | 2일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Day Wind Gust Miles per Hour] | 2일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL Day 2 Forecast Day Wind Speed Kilometers per Hour] | 2일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Day Wind Speed Miles per Hour] | 2일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL Day 2 Forecast Night Cloud Cover Miles] | 2일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL Day 2 Forecast Night Cloud Cover Kilometers] | 2일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 2 Forecast Night Precipitation Chance] | 2일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL Day 2 Forecast Night Precipitation Type] | 2일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL Day 2 Forecast Night QPF Inches] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL Day 2 Forecast Night QPF Millimeters] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL Day 2 Forecast Night QPF Snow Centimeters] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL Day 2 Forecast Night QPF Snow Inches] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL Day 2 Forecast Night Relative Humidity] | 2일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL Day 2 Forecast Night Snow Range] | 2일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL Day 2 Forecast Night Temperature Celsius] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL Day 2 Forecast Night Temperature Fahrenheit] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL Day 2 Forecast Night Temperature Heat Index Celsius] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 2 Forecast Night Temperature Heat Index Fahrenheit] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 2 Forecast Night Temperature Wind Chill Celsius] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 2 Forecast Night Temperature Wind Chill Fahrenheit] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 2 Forecast Night Thunder Index] | 2일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL Day 2 Forecast Night UV Index] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL Day 2 Forecast Night Wind Direction] | 2일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL Day 2 Forecast Night Wind Gust Kilometers per Hour] | 2일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Night Wind Gust Miles per Hour] | 2일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 2 Forecast Night Wind Speed Kilometers per Hour] | 2일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Night Wind Speed Miles per Hour] | 2일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 2 Forecast QPF Inches] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL Day 2 Forecast QPF Millimeters] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL Day 2 Forecast QPF Snow Centimeters] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 2 Forecast QPF Snow Inches] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Max Celsius] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Max Fahrenheit] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Min Celsius] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Min Fahrenheit] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Cloud Cover Miles] | 3일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL Day 3 Forecast Day Cloud Cover Kilometers] | 3일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL Day 3 Forecast Day Precipitation Chance] | 3일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL Day 3 Forecast Day Precipitation Type] | 3일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL Day 3 Forecast Day QPF Inches] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL Day 3 Forecast Day QPF Millimeters] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL Day 3 Forecast Day QPF Snow Centimeters] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL Day 3 Forecast Day QPF Snow Inches] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL Day 3 Forecast Day Relative Humidity] | 3일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL Day 3 Forecast Day Snow Range] | 3일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL Day 3 Forecast Day Temperature Celsius] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL Day 3 Forecast Day Temperature Fahrenheit] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Temperature Heat Index Celsius] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 3 Forecast Day Temperature Heat Index Fahrenheit] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Temperature Wind Chill Celsius] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL Day 3 Forecast Day Temperature Wind Chill Fahrenheit] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Thunder Index] | 3일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL Day 3 Forecast Day UV Index] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL Day 3 Forecast Day Wind Direction] | 3일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL Day 3 Forecast Day Wind Gust Kilometers per Hour] | 3일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Day Wind Gust Miles per Hour] | 3일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL Day 3 Forecast Day Wind Speed Kilometers per Hour] | 3일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Day Wind Speed Miles per Hour] | 3일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL Day 3 Forecast Night Cloud Cover Miles] | 3일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL Day 3 Forecast Night Cloud Cover Kilometers] | 3일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 3 Forecast Night Precipitation Chance] | 3일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL Day 3 Forecast Night Precipitation Type] | 3일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL Day 3 Forecast Night QPF Inches] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL Day 3 Forecast Night QPF Millimeters] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL Day 3 Forecast Night QPF Snow Centimeters] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL Day 3 Forecast Night QPF Snow Inches] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL Day 3 Forecast Night Relative Humidity] | 3일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL Day 3 Forecast Night Snow Range] | 3일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL Day 3 Forecast Night Temperature Celsius] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL Day 3 Forecast Night Temperature Fahrenheit] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL Day 3 Forecast Night Temperature Heat Index Celsius] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 3 Forecast Night Temperature Heat Index Fahrenheit] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 3 Forecast Night Temperature Wind Chill Celsius] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 3 Forecast Night Temperature Wind Chill Fahrenheit] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 3 Forecast Night Thunder Index] | 3일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL Day 3 Forecast Night UV Index] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL Day 3 Forecast Night Wind Direction] | 3일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL Day 3 Forecast Night Wind Gust Kilometers per Hour] | 3일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Night Wind Gust Miles per Hour] | 3일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 3 Forecast Night Wind Speed Kilometers per Hour] | 3일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Night Wind Speed Miles per Hour] | 3일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 3 Forecast QPF Inches] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL Day 3 Forecast QPF Millimeters] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL Day 3 Forecast QPF Snow Centimeters] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 3 Forecast QPF Snow Inches] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Max Celsius] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Max Fahrenheit] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Min Celsius] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Min Fahrenheit] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Cloud Cover Miles] | 5일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL Day 5 Forecast Day Cloud Cover Kilometers] | 5일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL Day 5 Forecast Day Precipitation Chance] | 5일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL Day 5 Forecast Day Precipitation Type] | 5일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL Day 5 Forecast Day QPF Inches] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL Day 5 Forecast Day QPF Millimeters] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL Day 5 Forecast Day QPF Snow Centimeters] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL Day 5 Forecast Day QPF Snow Inches] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL Day 5 Forecast Day Relative Humidity] | 5일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL Day 5 Forecast Day Snow Range] | 5일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL Day 5 Forecast Day Temperature Celsius] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL Day 5 Forecast Day Temperature Fahrenheit] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Temperature Heat Index Celsius] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 5 Forecast Day Temperature Heat Index Fahrenheit] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Temperature Wind Chill Celsius] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL Day 5 Forecast Day Temperature Wind Chill Fahrenheit] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Thunder Index] | 5일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL Day 5 Forecast Day UV Index] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL Day 5 Forecast Day Wind Direction] | 5일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL Day 5 Forecast Day Wind Gust Kilometers per Hour] | 5일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Day Wind Gust Miles per Hour] | 5일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL Day 5 Forecast Day Wind Speed Kilometers per Hour] | 5일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Day Wind Speed Miles per Hour] | 5일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL Day 5 Forecast Night Cloud Cover Miles] | 5일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL Day 5 Forecast Night Cloud Cover Kilometers] | 5일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 5 Forecast Night Precipitation Chance] | 5일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL Day 5 Forecast Night Precipitation Type] | 5일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL Day 5 Forecast Night QPF Inches] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL Day 5 Forecast Night QPF Millimeters] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL Day 5 Forecast Night QPF Snow Centimeters] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL Day 5 Forecast Night QPF Snow Inches] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL Day 5 Forecast Night Relative Humidity] | 5일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL Day 5 Forecast Night Snow Range] | 5일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL Day 5 Forecast Night Temperature Celsius] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL Day 5 Forecast Night Temperature Fahrenheit] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL Day 5 Forecast Night Temperature Heat Index Celsius] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 5 Forecast Night Temperature Heat Index Fahrenheit] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 5 Forecast Night Temperature Wind Chill Celsius] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 5 Forecast Night Temperature Wind Chill Fahrenheit] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 5 Forecast Night Thunder Index] | 5일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL Day 5 Forecast Night UV Index] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL Day 5 Forecast Night Wind Direction] | 5일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL Day 5 Forecast Night Wind Gust Kilometers per Hour] | 5일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Night Wind Gust Miles per Hour] | 5일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 5 Forecast Night Wind Speed Kilometers per Hour] | 5일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Night Wind Speed Miles per Hour] | 5일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 5 Forecast QPF Inches] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL Day 5 Forecast QPF Millimeters] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL Day 5 Forecast QPF Snow Centimeters] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 5 Forecast QPF Snow Inches] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Max Celsius] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Max Fahrenheit] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Min Celsius] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Min Fahrenheit] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 7 Forecast Cloud Cover Miles] | 7일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL Day 7 Forecast Cloud Cover Kilometers] | 7일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL Day 7 Forecast QPF Inches] | 7일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(인치) | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL Day 7 Forecast QPF Millimeters] | 7일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(밀리미터) | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL Day 7 Forecast QPF Snow Centimeters] | 7일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 7 Forecast QPF Snow Inches] | 7일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL Day 7 Forecast UV Index] | 7일간 날씨 예보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL Day 7 Forecast Wind Direction] | 7일간 날씨 예보. 평균 풍향(자기장 표기). | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL Day 7 Forecast Wind Speed Kilometers per Hour] | 7일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 7 Forecast Wind Speed Miles per Hour] | 7일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Max Celsius] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Max Fahrenheit] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Min Celsius] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Min Fahrenheit] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 10 Forecast Cloud Cover Miles] | 10일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL Day 10 Forecast Cloud Cover Kilometers] | 10일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL Day 10 Forecast QPF Inches] | 10일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(인치) | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL Day 10 Forecast QPF Millimeters] | 10일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(밀리미터) | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL Day 10 Forecast QPF Snow Centimeters] | 10일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 10 Forecast QPF Snow Inches] | 10일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL Day 10 Forecast UV Index] | 10일간 날씨 예보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL Day 10 Forecast Wind Direction] | 10일간 날씨 예보. 평균 풍향(자기장 표기). | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL Day 10 Forecast Wind Speed Kilometers per Hour] | 10일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 10 Forecast Wind Speed Miles per Hour] | 10일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Max Celsius] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Max Fahrenheit] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Min Celsius] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Min Fahrenheit] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 14 Forecast Cloud Cover Miles] | 14일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL Day 14 Forecast Cloud Cover Kilometers] | 14일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 14일차 예측 QPF(인치) | 14일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(인치) | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL Day 14 Forecast QPF Millimeters] | 14일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(밀리미터) | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL Day 14 Forecast QPF Snow Centimeters] | 14일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 14 Forecast QPF Snow Inches] | 14일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL Day 14 Forecast UV Index] | 14일간 날씨 예보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day14Forecast.uvIndex` |
| 14일차 풍향 예측 | 14일간 날씨 예보. 평균 풍향(자기장 표기). | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL Day 14 Forecast Wind Speed Kilometers per Hour] | 14일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 14 Forecast Wind Speed Miles per Hour] | 14일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 트리거 {#triggers}

트리거는 여러 입력을 기반으로 유의미한 기상 조건을 정의합니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL Product Triggers] | 특정 범주의 제품을 판매 유도하는 데 적합한 조건이 언제인지 보여 줍니다. 정수 ID에 매핑됩니다. 전체 목록은 IBM에서 가져올 수 있습니다. | `weather.productTriggers` |
| [!UICONTROL Relative Triggers] | 인간 인식에 기반한 상대적 조건. 뜨겁거나 차갑다는 인식. 정수 ID에 매핑됩니다. 전체 목록은 IBM에서 가져올 수 있습니다. | `weather.relativeTriggers` |
| [!UICONTROL Severe Weather Triggers] | 태풍이나 폭우 등 다양한 악천후 기상 조건을 나타냅니다. | `weather.severeTriggers` |
