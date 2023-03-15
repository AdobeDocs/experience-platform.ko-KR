---
title: 광고 세부 정보 스키마 필드 그룹
description: 이 문서에서는 광고 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 8%

---

# [!UICONTROL 광고 세부 정보] 스키마 필드 그룹

[!UICONTROL 광고 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `advertising` 광고 노출, 클릭스루 및 기여도 관련 정보를 캡처하는 스키마 오브젝트.

![필드 그룹 구조](../../images/field-groups/advertising-details/structure.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `adAssetReference` | 오브젝트 | 광고에 대한 자산 정보를 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#adAssetReference) 개체 구조에 대한 자세한 내용을 보려면. |
| `adAssetViewDetails` | 오브젝트 | 광고 재생에 대한 보기 세부 사항을 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#adAssetViewDetails) 개체 구조에 대한 자세한 내용을 보려면. |
| `adViewability` | 오브젝트 | 플레이어 볼륨, 라이브러리 버전, 창 상태 및 광고 뷰포트 차원과 같이 최종 사용자가 볼 수 있는 노출 횟수를 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#adViewability) 개체 구조에 대한 자세한 내용을 보려면. |
| `clicks` | [[!UICONTROL 측정]](../../data-types/measure.md) | 광고에 대한 클릭 동작 수입니다. |
| `completes` | [[!UICONTROL 측정]](../../data-types/measure.md) | 시간 미디어 에셋이 완료될 때까지 관찰된 횟수입니다. 이것은 최종 사용자가 앞서서 건너뛰었을 수도 있기 때문에 반드시 전체 비디오를 시청했다는 것을 의미하지는 않는다. |
| `conversions` | [[!UICONTROL 측정]](../../data-types/measure.md) | 사전 정의된 작업(또는 작업)이 성능 평가를 위해 이벤트를 트리거한 횟수입니다. |
| `federated` | [[!UICONTROL 측정]](../../data-types/measure.md) | 고객 간 데이터 공유와 같은 데이터 페더레이션을 통해 경험 이벤트가 생성되었는지 보여 줍니다. |
| `firstQuartiles` | [[!UICONTROL 측정]](../../data-types/measure.md) | 정상 속도로 재생이 25% 완료된 디지털 비디오 광고 횟수입니다. |
| `impressions` | [[!UICONTROL 측정]](../../data-types/measure.md) | 조회할 가능성이 있는 최종 사용자에게 전송된 광고 노출 횟수. |
| `midpoints` | [[!UICONTROL 측정]](../../data-types/measure.md) | 정상 속도로 재생이 50% 완료된 디지털 비디오 광고 횟수입니다. |
| `starts` | [[!UICONTROL 측정]](../../data-types/measure.md) | 디지털 비디오 광고 재생이 시작된 횟수입니다. |
| `thirdQuartiles` | [[!UICONTROL 측정]](../../data-types/measure.md) | 정상 속도로 재생이 75% 완료된 디지털 비디오 광고 횟수입니다. |
| `timePlayed` | [[!UICONTROL 측정]](../../data-types/measure.md) | 최종 사용자가 특정 시간 미디어 에셋에서 보낸 시간입니다. |
| `downloadedPlayback` | 부울 | 로 설정된 경우 `true`: 다운로드한 광고 세션 재생으로 인해 히트가 생성되었음을 나타냅니다. |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

다음 `adAssetReference` 오브젝트가 광고에 대한 자산 정보를 캡처합니다.

![adAssetReference 구조](../../images/field-groups/advertising-details/adAssetReference.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_dc.title` | 문자열 | 사람이 인식할 수 있는 알기 쉬운 광고 에셋 이름. |
| `_xmpDM.duration` | 정수 | 에셋의 길이 또는 기간(초)입니다. |
| `_id` | 문자열 | 다음 광고 자산의 고유 식별자. [Ad-ID standard](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | 문자열 | 광고에서 다루고 있는 제품의 회사 또는 브랜드입니다. |
| `campaign` | 문자열 | 광고 캠페인의 ID. |
| `creativeID` | 문자열 | 광고 문안 ID. |
| `creativeURL` | 문자열 | 광고 문안 URL. |
| `placementID` | 문자열 | 광고 배치 ID. |
| `siteID` | 문자열 | 광고 사이트의 ID. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

다음 `adAssetViewDetails` 오브젝트가 광고 재생에 대한 세부 정보 보기를 캡처합니다.

![adAssetViewDetails 구조](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 광고 브레이크]](../../data-types/ad-break.md) | 시간 광고를 시간 미디어에 삽입하는 방법을 설명합니다. |
| `index` | 정수 | 상위 광고 브레이크 내에 있는 광고의 색인입니다. 예를 들어 첫 번째 광고에는 색인이 있습니다 `0` 두 번째 광고에는 색인이 있습니다. `1`. |
| `playerName` | 문자열 | 광고를 렌더링하는 플레이어의 이름. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

다음 `adViewability` object 는 플레이어 볼륨, 라이브러리 버전, 창 상태 및 광고 뷰포트 차원과 같은 최종 사용자가 볼 수 있는 노출 횟수를 캡처합니다.

![adViewability 구조](../../images/field-groups/advertising-details/adViewability.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 구현 세부 사항]](../../data-types/implementation-details.md) | 조회 지표를 측정하기 위한 라이브러리 이름 및 버전 계측. |
| `measuredAdNotVisible` | [[!UICONTROL 측정]](../../data-types/measure.md) | 노출 시간대에 조회 라이브러리로 측정한 결과 광고가 표시되지 않음을 나타냅니다. |
| `measuredMuted` | [[!UICONTROL 측정]](../../data-types/measure.md) | 노출 시간대에 조회 라이브러리로 측정한 대로 광고가 음소거됨을 나타냅니다. |
| `unmeasurableIframe` | [[!UICONTROL 측정]](../../data-types/measure.md) | 노출 시간대에 조회 라이브러리로 측정한 결과 광고가 비활성 창에 표시되는지 보여 줍니다. |
| `unmeasurableOther` | [[!UICONTROL 측정]](../../data-types/measure.md) | 광고가 iframe 내부에 표시되기 때문에 조회 라이브러리가 측정을 제대로 수행할 수 없음을 나타냅니다. |
| `viewabilityEligibleImpressions` | [[!UICONTROL 측정]](../../data-types/measure.md) | 조회 라이브러리 계측 완료 후 최종 사용자 광고 노출 횟수. |
| `viewabilityCompletes` | [[!UICONTROL 측정]](../../data-types/measure.md) | 완료 시간에 조회 라이브러리에서 조회가 가능한 것으로 간주되는 최종 사용자 광고 완료. |
| `viewableFirstQuartiles` | [[!UICONTROL 측정]](../../data-types/measure.md) | 재생 1분위에 조회 라이브러리에서 조회가 가능한 것으로 간주되는 최종 사용자 광고 1분위. |
| `viewableImpressions` | [[!UICONTROL 측정]](../../data-types/measure.md) | 재생 2초 후 조회 라이브러리에서 조회가 가능한 것으로 간주되는 최종 사용자 광고 노출 횟수. |
| `viewableMidpoints` | [[!UICONTROL 측정]](../../data-types/measure.md) | 재생 중간점에 조회 라이브러리에서 조회가 가능한 것으로 간주되는 최종 사용자 광고 중간점. |
| `viewableThirdQuartiles` | [[!UICONTROL 측정]](../../data-types/measure.md) | 재생 3분위에 조회 라이브러리에서 조회가 가능한 것으로 간주되는 최종 사용자 광고 3분위. |
| `activeWindow` | 부울 | 광고가 사용자 디바이스의 활성 창에 표시되었는지 여부를 나타냅니다. |
| `adHeight` | 정수 | 런타임으로 측정한 플레이어의 세로 픽셀 수. 플레이어에 추가 컨트롤 또는 썸네일이 있는 경우 광고 크기보다 클 수 있습니다. |
| `adUnitDepth` | 정수 | 게시자는 광고 액세스를 전적으로 페이지 코드로 제한하기 위해 광고 단위를 컨테이너(iFrame) 내에 포함할 수 있습니다. 이 값은 내에 표시되는 광고 단위의 컨테이너 수를 설명합니다. |
| `adWidth` | 정수 | 런타임으로 측정한 플레이어의 가로 픽셀 수. 플레이어에 추가 컨트롤 또는 썸네일이 있는 경우 광고 크기보다 클 수 있습니다. |
| `measurementEligible` | 부울 | 광고가 조회 측정에 적합한지 여부. 단위에 지원되는 크리에이티브 포맷과 태그 유형이 있는 경우 광고를 사용할 수 있습니다. |
| `percentViewable` | 정수 | 측정 시간에 조회가 가능한 것으로 간주되는 광고의 픽셀 비율. |
| `playerVolume` | 정수 | 런타임으로 측정한 플레이어 볼륨 백분율. 여기서 `0` 음소거됨 및 `100` 은(는) 최대 볼륨입니다. |
| `viewable` | 부울 | 런타임 시 광고를 보았는지 여부를 나타냅니다. 디스플레이 광고는 최소 50%의 광고가 1초 이상 표시될 때 볼 수 있는 것으로 간주됩니다. 비디오가 2초 이상 연속 재생되는 동안 광고의 50% 이상이 표시되면 비디오 광고를 볼 수 있는 것으로 간주됩니다. |
| `viewportHeight` | 정수 | 런타임으로 측정한 경험이 내부로 표시되는 윈도우 (픽셀의) 세로 크기. 웹 보기 이벤트의 경우 이 값은 브라우저 뷰포트 높이를 나타냅니다. |
| `viewportWidth` | 정수 | 런타임으로 측정한 경험이 내부로 표시되는 윈도우 (픽셀의) 가로 크기. 웹 보기 이벤트의 경우 이 값은 브라우저 뷰포트 너비를 나타냅니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
