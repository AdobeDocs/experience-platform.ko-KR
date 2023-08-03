---
title: 날씨 데이터 필드 매핑
description: The Weather Channel 통합 기능의 일부로 제공되는 사용 가능한 날씨 데이터 필드에 대한 참조 페이지.
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: e2122008fcae1016db03d6b5f56e4fa25520f9d0
workflow-type: ht
source-wordcount: '12238'
ht-degree: 100%

---

# 날씨 데이터 필드 매핑

Adobe는 데이터스트림을 통해 수집한 데이터에 미국 날씨에 대한 컨텍스트를 추가 제공하기 위해 [!DNL [The Weather Company]](https://www.ibm.com/weather)와(과) 파트너 관계를 맺고 있습니다. 이 데이터를 사용하여 Experience Platform에서 분석, 타겟팅 및 세그먼트 생성을 수행할 수 있습니다.

이 페이지에는 대상자 데이터를 보완하는 데 사용할 수 있는 모든 필드가 나열되어 있습니다.

필드는 필드 그룹에 맞춰 조정되는 세 가지 서로 다른 그룹으로 나뉩니다.

* [**[!UICONTROL 현재 날씨]**](#current-weather): 해당 위치를 기준으로 한 사용자의 현재 기상 조건. 여기에는 현재 온도, 강수량, 전운량 등이 포함됩니다.
* [**[!UICONTROL 날씨 예보]**](#forecast): 날씨 예보에는 사용자 위치에 따라 1, 2, 3, 5, 7 및 10일차 예보가 있습니다.
* [**[!UICONTROL 트리거]**](#triggers): 트리거는 다양하고 유의미한 기상 조건에 매핑하는 특정 조합입니다. 날씨 트리거에는 세 가지 유형이 있습니다.

   * **[!UICONTROL 상대적 트리거]**: 날씨가 춥거나 비가 오는 날 등 유의미한 조건. 이는 기후에 따라 정의가 달라질 수 있습니다.
   * **[!UICONTROL 제품 트리거]**: 다양한 제품 구매로 연결될 수 있는 조건. 예: 추운 날씨가 예보되면서 우비를 구매할 가능성이 높아질 수 있습니다.
   * **[!UICONTROL 악천후 기상 트리거]**: 겨울 폭풍이나 태풍 경고 등 악천후 기상 경고.

## 현재 날씨 {#current-weather}

해당 위치를 기준으로 한 사용자의 현재 기상 조건.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL 이슬점 온도(섭씨)] | 일정한 압력으로 포화 상태에 도달하기 위한 공기 냉각 온도. 이슬점은 공기 습도를 간접적으로 측정하는 지표이기도 합니다. 이슬점은 온도를 초과하지 않습니다. 이슬점과 온도가 같으면 보통 구름 또는 안개가 형성됩니다. 온도 값이 이슬점 값에 가까워지면 상대 습도가 높아집니다. 범위 - -80~100(°F) 내지 -62~37(°C). 섭씨 온도 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 이슬점 온도(화씨)] | 일정한 압력으로 포화 상태에 도달하기 위한 공기 냉각 온도. 이슬점은 공기 습도를 간접적으로 측정하는 지표이기도 합니다. 이슬점은 온도를 초과하지 않습니다. 이슬점과 온도가 같으면 보통 구름 또는 안개가 형성됩니다. 온도 값이 이슬점 값에 가까워지면 상대 습도가 높아집니다. 범위 - -80~100(°F) 내지 -62~37(°C). 화씨 온도 | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 지난 1시간 동안의 강수량(인치)] | 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(인치) | `weather.current.precip1Hour.inches` |
| [!UICONTROL 지난 1시간 동안의 강수량(밀리미터)] | 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(밀리미터) | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 24시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(인치) | `weather.current.precip24Hour.inches` |
| [!UICONTROL 지난 24시간 동안의 강수량(밀리미터)] | 24시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(밀리미터) | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 지난 6시간 동안의 강수량(인치)] | 6시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(인치) | `weather.current.precip6Hour.inches` |
| [!UICONTROL 지난 6시간 동안의 강수량(밀리미터)] | 6시간 롤링 시 액체 강수 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강수량(밀리미터) | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 기압 변화] | 지난 3시간 동안의 기압 변화(밀리바). | `weather.current.pressureChange` |
| [!UICONTROL 평균 해수면 기압] | 평균 해수면 기압(밀리바). 다시 말해, 해수면의 평균 기압입니다.<br>범위 - 1/10mb(밀리바) 수준까지 정밀. | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 상대 습도] | 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.current.relativeHumidity` |
| [!UICONTROL 지난 1시간 동안의 강설량(센티미터)] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(센티미터) | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 지난 1시간 동안의 강설량(인치)] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(인치) | `weather.current.snow1Hour.inches` |
| [!UICONTROL 24시간 동안의 강설량(센티미터)] | 24시간 롤링 시 강설 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(센티미터) | `weather.current.snow24Hour.centimeters` |
| 24시간 동안의 강설량(인치) | 24시간 롤링 시 강설 시간. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(인치) | `weather.current.snow24Hour.inches` |
| [!UICONTROL 지난 6시간 동안의 강설량(센티미터)] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(센티미터) | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 지난 6시간 동안의 강설량(인치)] | 1시간 동안의 강설량. 제시된 시간은 요청 기간(현재)을 통과한 롤링 시간입니다. 강설량(인치) | `weather.current.snow6Hour.inches` |
| [!UICONTROL 일몰 시간] | 일몰 시간(UTC) | `weather.current.sunsetTime` |
| [!UICONTROL 온도(섭씨)] | 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.current.temperature.celsius` |
| [!UICONTROL 온도(화씨)] | 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 24시간 동안의 온도 변화(섭씨)] | 24시간 전 보고서와 온도 변화 비교. 섭씨 온도 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 24시간 동안의 온도 변화(화씨)] | 24시간 전 보고서와 온도 변화 비교. 화씨 온도 | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 겉보기 온도(섭씨)] | 겉보기 온도. 겉보기 온도는 체감 온도나 열 지수 결합 효과로 인해 노출된 인체 피부에서 “체감”되는 기온을 나타냅니다.<br>온도가 65°F를 초과할 경우 체감 온도 값은 계산된 열 지수를 나타냅니다. 온도가 65°F 미만일 경우 체감 온도 값은 계산된 체감 온도를 나타냅니다.<br>범위 - 140~140. 섭씨 온도 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 겉보기 온도(화씨)] | 겉보기 온도. 겉보기 온도는 체감 온도나 열 지수 결합 효과로 인해 노출된 인체 피부에서 “체감”되는 기온을 나타냅니다.<br>온도가 65°F를 초과할 경우 체감 온도 값은 계산된 열 지수를 나타냅니다. 온도가 65°F 미만일 경우 체감 온도 값은 계산된 체감 온도를 나타냅니다.<br>범위 - 140~140. 화씨 온도 | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 오전 7시 이후 최고 온도(섭씨)] | 오전 7시 이후 최대 온도(현지 시간). 섭씨 온도 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 오전 7시 이후 최고 온도(화씨)] | 오전 7시 이후 최대 온도(현지 시간). 화씨 온도 | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 지난 24시간 동안의 최저 온도(섭씨)] | 지난 24시간 동안의 최저 온도. 24시간은 요청 기간(현재)을 기준으로 합니다. 섭씨 온도 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 지난 24시간 동안의 최저 온도(화씨)] | 지난 24시간 동안의 최저 온도. 24시간은 요청 기간(현재)을 기준으로 합니다. 화씨 온도 | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 풍향] | 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.current.windDirection` |
| [!UICONTROL 돌풍(시속 킬로미터)] | 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 돌풍(시속 마일)] | 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.current.windGust.`시속 마일 |
| [!UICONTROL 풍속(시속 킬로미터)] | 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 풍속(시속 마일)] | 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.current.windSpeed.milesPerHour` |

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
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 1일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 1일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 1일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 1일차 야간 강수 확률 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day01Forecast.night.precipChance` |
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
| [!UICONTROL 1일차 야간 체감 온도(화씨) 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 1일차 야간 천둥 지수 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 1일차 야간 UV 인덱스 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 1일차 야간 풍향 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 1일차 야간 돌풍(시속 킬로미터) 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 1일차 야간 돌풍(시속 마일) 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 1일차 야간 풍속(시속 킬로미터) 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 1일차 야간 풍속(시속 마일) 예측] | 1일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 1일차 QPF(인치) 예측] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 1일차 QPF(밀리미터) 예측] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 1일차 QPF 강설량(센티미터) 예측] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 1일차 QPF 강설량(인치) 예측] | 1일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 2일차 날씨 예보 캘린더 일일 최고 섭씨 온도] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 2일차 날씨 예보 캘린더 일일 최고 화씨 온도] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 2일차 날씨 예보 캘린더 일일 최저 섭씨 온도] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 2일차 날씨 예보 캘린더 일일 최저 화씨 온도] | 2일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 2일차 주간 전운량(마일) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 2일차 주간 전운량(킬로미터) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 2일차 주간 강수 확률 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 2일차 주간 강수 유형 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 2일차 주간 QPF(인치) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 2일차 주간 QPF(밀리미터) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 2일차 주간 QPF 강설량(센티미터) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 2일차 주간 강설량(인치) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 2일차 주간 상대 습도 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 2일차 주간 강설량 범위 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 2일차 주간 온도(섭씨) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 2일차 주간 온도(화씨) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 2일차 주간 온도 열 지수(섭씨) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 2일차 주간 온도 열 지수(화씨) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 2일차 주간 체감 온도(섭씨) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 2일차 주간 체감 온도(화씨) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 2일차 주간 천둥 지수 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 2일차 주간 UV 인덱스 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 2일차 주간 풍향 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 2일차 주간 돌풍(시속 킬로미터) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 2일차 주간 돌풍(시속 마일) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 2일차 주간 풍속(시속 킬로미터) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 2일차 주간 풍속(시속 마일) 예측] | 2일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 2일차 야간 전운량(마일) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 2일차 야간 전운량(킬로미터) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 2일차 야간 강수 확률 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 2일차 야간 강수 유형 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 2일차 야간 QPF(인치) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 2일차 야간 QPF(밀리미터) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 2일차 야간 QPF 강설량(센티미터) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 2일차 야간 QPF 강설량(인치) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 2일차 야간 상대 습도 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 2일차 야간 강설량 범위 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 2일차 야간 온도(섭씨) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 2일차 야간 온도(화씨) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 2일차 야간 온도 열 지수(섭씨) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 2일차 야간 온도 열 지수(화씨) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 2일차 야간 체감 온도(섭씨) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 2일차 야간 체감 온도(화씨) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 2일차 야간 천둥 지수 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 2일차 야간 UV 인덱스 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 2일차 야간 풍향 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 2일차 야간 돌풍(시속 킬로미터) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 2일차 야간 돌풍(시속 마일) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 2일차 야간 풍속(시속 킬로미터) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 2일차 야간 풍속(시속 마일) 예측] | 2일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 2일차 QPF(인치) 예측] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 2일차 QPF(밀리미터) 예측] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 2일차 QPF 강설량(센티미터) 예측] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 2일차 QPF 강설량(인치) 예측] | 2일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 3일차 날씨 예보 캘린더 일일 최고 섭씨 온도] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 3일차 날씨 예보 캘린더 일일 최고 화씨 온도] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 3일차 날씨 예보 캘린더 일일 최저 섭씨 온도] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 3일차 날씨 예보 캘린더 일일 최저 화씨 온도] | 3일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 3일차 주간 전운량(마일) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 3일차 주간 전운량(킬로미터) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 3일차 주간 강수 확률 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 3일차 주간 강수 유형 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 3일차 주간 QPF(인치) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 3일차 주간 QPF(밀리미터) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 3일차 주간 QPF 강설량(센티미터) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 3일차 주간 강설량(인치) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 3일차 주간 상대 습도 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 3일차 주간 강설량 범위 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 3일차 주간 온도(섭씨) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 3일차 주간 온도(화씨) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 3일차 주간 온도 열 지수(섭씨) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 3일차 주간 온도 열 지수(화씨) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 3일차 주간 체감 온도(섭씨) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 3일차 주간 체감 온도(화씨) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 3일차 주간 천둥 지수 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 3일차 주간 UV 인덱스 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 3일차 주간 풍향 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 3일차 주간 돌풍(시속 킬로미터) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 3일차 주간 돌풍(시속 마일) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 3일차 주간 풍속(시속 킬로미터) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 3일차 주간 풍속(시속 마일) 예측] | 3일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 3일간 야간 전운량(마일) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 3일차 야간 전운량(킬로미터) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 3일차 야간 강수 확률 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 3일차 야간 강수 유형 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 3일차 야간 QPF(인치) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 3일차 야간 QPF(밀리미터) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 3일차 야간 QPF 강설량(센티미터) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 3일차 야간 QPF 강설량(인치) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 3일차 야간 상대 습도 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 3일차 야간 강설량 범위 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 3일차 야간 온도(섭씨) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 3일차 야간 온도(화씨) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 3일차 야간 온도 열 지수(섭씨) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 3일차 야간 온도 열 지수(화씨) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 3일차 야간 체감 온도(섭씨) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 3일차 야간 체감 온도(화씨) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 3일차 야간 천둥 지수 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 3일차 야간 UV 인덱스 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 3일차 야간 풍향 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 3일차 야간 돌풍(시속 킬로미터) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 3일차 야간 돌풍(시속 마일) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 3일차 야간 풍속(시속 킬로미터) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 3일차 야간 풍속(시속 마일) 예측] | 3일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 3일차 QPF(인치) 예측] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 3일차 QPF(밀리미터) 예측] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 3일차 QPF 강설량(센티미터) 예측] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 3일차 QPF 강설량(인치) 예측] | 3일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 5일차 날씨 예보 캘린더 일일 최고 섭씨 온도] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 5일차 날씨 예보 캘린더 일일 최고 화씨 온도] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 5일차 날씨 예보 캘린더 일일 최저 섭씨 온도] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 5일차 날씨 예보 캘린더 일일 최저 화씨 온도] | 5일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 5일차 주간 전운량(마일) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 5일차 주간 전운량(킬로미터) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 5일차 주간 강수 확률 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 5일차 주간 강수 유형 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 5일차 주간 QPF(인치) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 5일차 주간 QPF(밀리미터) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 5일차 주간 QPF 강설량(센티미터) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 5일차 주간 강설량(인치) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 5일차 주간 상대 습도 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 5일차 주간 강설량 범위 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 5일차 주간 온도(섭씨) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 5일차 주간 온도(화씨) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 5일차 주간 온도 열 지수(섭씨) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 5일차 주간 온도 열 지수(화씨) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 5일차 주간 체감 온도(섭씨) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 5일차 주간 체감 온도(화씨) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 5일차 주간 천둥 지수 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 5일차 주간 UV 인덱스 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 5일차 주간 풍향 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 5일차 주간 돌풍(시속 킬로미터) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 5일차 주간 돌풍(시속 마일) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 5일차 주간 풍속(시속 킬로미터) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 5일차 주간 풍속(시속 마일) 예측] | 5일간 날씨 예보. 낮 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 5일차 야간 전운량(마일) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 5일차 야간 전운량(킬로미터) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 5일차 야간 강수 확률 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 강수량이 많을 확률(백분율). | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 5일차 야간 강수 유형 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 강수 형태(비, 눈, 진눈깨비 등). | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 5일차 야간 QPF(인치) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 5일차 야간 QPF(밀리미터) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 5일차 야간 QPF 강설량(센티미터) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 5일차 야간 QPF 강설량(인치) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 5일차 야간 상대 습도 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 공기의 상대 습도는 일정 온도에서 공기를 포화 상태로 만드는 데 필요한 수증기량에 대한 공기 중 수증기량의 비율로 정의됩니다. 상대 습도는 항상 백분율로 표시합니다.<br>범위 - 0~100. | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 5일차 야간 강설량 범위 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 잠재적 강설량(1~3인치, 3~6인치 등). | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 5일차 야간 온도(섭씨) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 5일차 야간 온도(화씨) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도(정의된 측정 단위). 범위 - 140~140. 화씨 온도 | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 5일차 야간 온도 열 지수(섭씨) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 5일차 야간 온도 열 지수(화씨) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 습도를 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 5일차 야간 체감 온도(섭씨) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 섭씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 5일차 야간 체감 온도(화씨) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 온도 및 풍속을 기준으로 노출된 사람이 체감하는 온도. 화씨 온도 | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 5일차 야간 천둥 지수 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 지역에 영향을 미치는 뇌우가 발생할 확률 지수. 0(천둥 없음에서 5단계(심한 뇌우가 발생할 위험 높음)). | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 5일차 야간 UV 인덱스 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 5일차 야간 풍향 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 바람이 불어오는 자기풍향은 도 단위로 표현합니다. 자기 방향은 0~359°까지 다양합니다. 0°는 북쪽을, 90°는 동쪽을, 180°는 남쪽을, 270°는 서쪽을 가리킵니다.<br>범위 - 0&lt;=wind_dire_deg&lt;=350, 10° 간격. | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 5일차 야간 돌풍(시속 킬로미터) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 5일차 야간 돌풍(시속 마일) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 이 데이터 필드에는 평균 풍속에 미치는 갑작스럽고 일시적인 변화에 대한 정보가 포함되어 있습니다. 보고서에는 관측 기간 동안 기록된 최대 돌풍 풍속이 반드시 표시됩니다. 풍속이 표시되는 경우 이는 필수 표시 필드입니다. 돌풍 속도는 시속 마일 또는 시속 킬로미터로 표현할 수 있습니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 5일차 야간 풍속(시속 킬로미터) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 5일차 야간 풍속(시속 마일) 예측] | 5일간 날씨 예보. 야간 시간 날씨 정보. 바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 현재 기상 조건에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 5일차 QPF(인치) 예측] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(인치) | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 5일차 QPF(밀리미터) 예측] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 측정 단위(밀리미터). 강수량(밀리미터) | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 5일차 QPF 강설량(센티미터) 예측] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 5일차 QPF 강설량(인치) 예측] | 5일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 7일차 날씨 예보 캘린더 일일 최고 섭씨 온도] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 7일차 날씨 예보 캘린더 일일 최고 화씨 온도] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 7일차 날씨 예보 캘린더 일일 최저 섭씨 온도] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 7일차 날씨 예보 캘린더 일일 최저 화씨 온도] | 7일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 7일차 전운량(마일) 예측] | 7일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 7일차 전운량(킬로미터) 예측] | 7일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 7일차 QPF(인치) 예측] | 7일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(인치) | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 7일차 QPF(밀리미터) 예측] | 7일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(밀리미터) | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 7일차 QPF 강설량(센티미터) 예측] | 7일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 7일차 QPF 강설량(인치) 예측] | 7일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 7일차 UV 인덱스 예측] | 7일간 날씨 예보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 7일차 풍향 예측] | 7일간 날씨 예보. 평균 풍향(자기장 표기). | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 7일차 풍속(시속 킬로미터) 예측] | 7일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 7일차 풍속(시속 마일) 예측] | 7일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 10일차 날씨 예보 캘린더 일일 최고 섭씨 온도] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 10일차 날씨 예보 캘린더 일일 최고 화씨 온도] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 10일차 날씨 예보 캘린더 일일 최저 섭씨 온도] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 10일차 날씨 예보 캘린더 일일 최저 화씨 온도] | 10일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 10일차 전운량(마일) 예측] | 10일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 10일차 전운량(킬로미터) 예측] | 10일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 10일차 QPF(인치) 예측] | 10일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(인치) | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 10일차 QPF(밀리미터) 예측] | 10일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(밀리미터) | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 10일차 QPF 강설량(센티미터) 예측] | 10일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 10일차 QPF 강설량(인치) 예측] | 10일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 10일차 UV 인덱스 예측] | 10일간 날씨 예보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 10일차 풍향 예측] | 10일간 날씨 예보. 평균 풍향(자기장 표기). | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 10일차 풍속(시속 킬로미터) 예측] | 10일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 10일차 풍속(시속 마일) 예측] | 10일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 14일차 날씨 예보 캘린더 일일 최고 섭씨 온도] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 14일차 날씨 예보 캘린더 일일 최고 화씨 온도] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최고 온도. 화씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 14일차 날씨 예보 캘린더 일일 최저 섭씨 온도] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 섭씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 14일차 날씨 예보 캘린더 일일 최저 화씨 온도] | 14일간 날씨 예보. 해당 요일의 자정에서 다음 자정까지의 일일 최저 온도. 화씨 온도 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 14일차 전운량(마일) 예측] | 14일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(마일). | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 14일차 전운량(킬로미터) 예측] | 14일간 날씨 예보. 낮 평균 전운량은 백분율로 표시함. 거리(킬로미터). | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 14일차 예측 QPF(인치) | 14일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(인치) | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 14일차 QPF(밀리미터) 예측] | 14일간 날씨 예보. 24시간 동안 측정 가능한 예상 강수량(액체 상태 또는 이에 상응하는 상태). 강수량(밀리미터) | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 14일차 QPF 강설량(센티미터) 예측] | 14일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(센티미터) | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 14일차 QPF 강설량(인치) 예측] | 14일간 날씨 예보. 12시간 또는 24시간 동안 측정 가능한 강설량 예측. 측정 단위(센티미터). 강설량(인치) | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 14일차 UV 인덱스 예측] | 14일간 날씨 예보. 12시간 동안 최대 UV 인덱스 예측. | `weather.forecast.day14Forecast.uvIndex` |
| 14일차 풍향 예측 | 14일간 날씨 예보. 평균 풍향(자기장 표기). | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 14일차 풍속(시속 킬로미터) 예측] | 14일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 킬로미터) | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 14일차 풍속(시속 마일) 예측] | 14일간 날씨 예보. 12시간 동안 지속되는 최대 풍속 예측.<br>바람은 벡터로 취급되므로 바람에는 방향과 크기(속도)가 있어야 합니다. 날씨 예보에 보고되는 풍속 정보는 평균 10분의 지속 풍속에 해당합니다. 갑작스럽거나 단시간의 풍속 변화인 “돌풍”은 별도의 데이터 필드에 보고됩니다. 풍향은 “바람이 불어오는 방향”으로서 북풍은 북쪽에서 남쪽으로 불어오는 바람을 의미합니다. 북풍이 불어 북쪽으로 향하면 북풍이 앞으로 불어옵니다. 남쪽으로 향하면 북풍이 뒤로 불어옵니다. 풍속(시속 마일) | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 트리거 {#triggers}

트리거는 여러 입력을 기반으로 유의미한 기상 조건을 정의합니다.

| 필드 | 설명 | XDM 경로 |
| --- | ---- | --- |
| [!UICONTROL 제품 트리거] | 특정 범주의 제품을 판매 유도하는 데 적합한 조건이 언제인지 보여 줍니다. 정수 ID에 매핑됩니다. 전체 목록은 IBM에서 가져올 수 있습니다. | `weather.productTriggers` |
| [!UICONTROL 상대적 트리거] | 인간 인식에 기반한 상대적 조건. 뜨겁거나 차갑다는 인식. 정수 ID에 매핑됩니다. 전체 목록은 IBM에서 가져올 수 있습니다. | `weather.relativeTriggers` |
| [!UICONTROL 악천후 기상 트리거] | 태풍이나 폭우 등 다양한 악천후 기상 조건을 나타냅니다. | `weather.severeTriggers` |
