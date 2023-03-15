---
title: Adobe Analytics ExperienceEvent 전체 확장 스키마 필드 그룹
description: 이 문서에서는 Adobe Analytics ExperienceEvent 전체 확장 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# [!UICONTROL Adobe Analytics ExperienceEvent 전체 확장] 스키마 필드 그룹

[!UICONTROL Adobe Analytics ExperienceEvent 전체 확장] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md): Adobe Analytics에서 수집하는 일반적인 지표를 캡처합니다.

이 문서에서는 Analytics 확장 필드 그룹의 구조 및 사용 사례에 대해 설명합니다.

>[!NOTE]
>
>이 필드 그룹의 반복되는 요소 크기와 수로 인해 이 안내서에 표시되는 많은 필드가 축소되어 공간을 절약할 수 있습니다. 이 필드 그룹의 전체 구조를 살펴보려면 다음을 수행할 수 있습니다. [플랫폼 UI에서 조회 ](../../ui/explore.md) 또는 의 전체 스키마 보기 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## 필드 그룹 구조

필드 그룹은 단일 `_experience` 단일 객체를 포함하는 스키마 객체 `analytics` 개체.

![Analytics 필드 그룹의 최상위 필드](../../images/field-groups/analytics-full-extension/full-schema.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `customDimensions` | 오브젝트 | Analytics에서 추적하는 사용자 지정 차원을 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#custom-dimensions) 을 참조하십시오. |
| `endUser` | 오브젝트 | 이벤트를 트리거한 최종 사용자에 대한 웹 인터랙션 세부 정보를 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#end-user) 을 참조하십시오. |
| `environment` | 오브젝트 | 이벤트를 트리거한 브라우저 및 운영 체제에 대한 정보를 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#environment) 을 참조하십시오. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | 오브젝트 | 필드 그룹은 최대 1000개의 사용자 지정 이벤트를 캡처할 수 있는 개체 필드를 제공합니다. 다음을 참조하십시오. [아래 하위 섹션](#events) 를 참조하십시오. |
| `session` | 오브젝트 | 이벤트를 트리거한 세션에 대한 정보를 캡처합니다. 다음을 참조하십시오. [아래 하위 섹션](#session) 을 참조하십시오. |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` 사용자 정의 캡처 [치수](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=ko-KR) Analytics에서 추적합니다.

![customDimensions 필드](../../images/field-groups/analytics-full-extension/customDimensions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `eVars` | 오브젝트 | 최대 250개의 전환 변수를 캡처하는 개체([eVar](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=ko-KR)). 이 개체의 속성은 키 처리됩니다. `eVar1` 끝 `eVar250` 및 에서는 해당 데이터 형식에 대한 문자열만 허용합니다. |
| `hierarchies` | 오브젝트 | 최대 5개의 사용자 지정 계층 변수를 캡처하는 개체([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html)). 이 개체의 속성은 키 처리됩니다. `hier1` 끝 `hier5`: 다음 하위 속성을 갖는 객체 그 자체입니다.<ul><li>`delimiter`: 아래에 제공된 목록을 생성하는 데 사용되는 원래 구분 기호 `values`.</li><li>`values`: 문자열로 표시되는 계층 수준 이름의 구분된 목록입니다.</li></ul> |
| `listProps` | 오브젝트 | 최대 75개를 캡처하는 오브젝트 [list props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). 이 개체의 속성은 키 처리됩니다. `prop1` 끝 `prop75`: 다음 하위 속성을 갖는 객체 그 자체입니다.<ul><li>`delimiter`: 아래에 제공된 목록을 생성하는 데 사용되는 원래 구분 기호 `values`.</li><li>`values`: 문자열로 표시되는 prop의 구분된 값 목록입니다.</li></ul> |
| `lists` | 오브젝트 | 최대 3개를 캡처하는 오브젝트 [목록](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). 이 개체의 속성은 키 처리됩니다. `list1` 끝 `list3`. 이러한 각 속성에는 단일 항목이 포함됩니다 `list` 배열 [[!UICONTROL 키 값 쌍]](../../data-types/key-value-pair.md) 데이터 유형. |
| `props` | 오브젝트 | 최대 75개를 캡처하는 오브젝트 [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). 이 개체의 속성은 키 처리됩니다. `prop1` 끝 `prop75` 및 에서는 해당 데이터 형식에 대한 문자열만 허용합니다. |
| `postalCode` | 문자열 | 클라이언트가 제공한 우편 번호. |
| `stateProvince` | 문자열 | 클라이언트가 제공한 주 또는 시/도 위치. |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` 이벤트를 트리거한 최종 사용자에 대한 웹 인터랙션 세부 정보를 캡처합니다.

![endUser 필드](../../images/field-groups/analytics-full-extension/endUser.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL 웹 정보]](../../data-types/web-information.md) | 이 최종 사용자에 대한 첫 번째 경험 이벤트의 웹 페이지, 링크 및 레퍼러 관련 정보입니다. |
| `firstTimestamp` | 정수 | 이 최종 사용자의 첫 번째 ExperienceEvent에 대한 Unix 타임스탬프입니다. |

## `environment` {#environment}

`environment` 이벤트를 트리거한 브라우저 및 운영 체제에 대한 정보를 캡처합니다.

![환경 필드](../../images/field-groups/analytics-full-extension/environment.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `browserIDStr` | 문자열 | 사용된 브라우저의 Adobe Analytics 식별자(또는 [브라우저 유형 차원](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html?lang=ko-KR)). |
| `operatingSystemIDStr` | 문자열 | 사용된 운영 체제용 Adobe Analytics 식별자(또는 [운영 체제 유형 차원](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html?lang=ko-KR)). |

## 사용자 정의 이벤트 필드 {#events}

Analytics 확장 필드 그룹은 최대 100개를 캡처하는 10개의 개체 필드를 제공합니다 [사용자 지정 이벤트 지표](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=ko-KR) 각각, 필드 그룹의 총 1000개

각 최상위 이벤트 객체에는 해당 범위의 개별 이벤트 객체가 포함되어 있습니다. 예를 들어, `event101to200` 은(는) 다음을 키로 한 이벤트를 포함합니다. `event101` 끝 `event200`.

각 짝수 오브젝트는 [[!UICONTROL 측정]](../../data-types/measure.md) 고유 식별자 및 수량 가능한 값을 제공하는 데이터 유형.

![사용자 정의 이벤트 필드](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` 이벤트를 트리거한 세션에 대한 정보를 캡처합니다.

![세션 필드](../../images/field-groups/analytics-full-extension/session.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `search` | [[!UICONTROL 검색]](../../data-types/search.md) | 세션 항목에 대한 웹 또는 모바일 검색 관련 정보를 캡처합니다. |
| `web` | [[!UICONTROL 웹 정보]](../../data-types/web-information.md) | 세션 항목에 대한 링크 클릭 수, 웹 페이지 세부 정보, 레퍼러 정보 및 브라우저 세부 정보를 캡처합니다. |
| `depth` | 정수 | 최종 사용자의 현재 세션 깊이(예: 페이지 번호)입니다. |
| `num` | 정수 | 최종 사용자의 현재 세션 번호입니다. |
| `timestamp` | 정수 | 세션 항목에 대한 Unix 타임스탬프입니다. |

## 다음 단계

이 문서에서는 Analytics 확장 필드 그룹의 구조 및 사용 사례를 다룹니다. 필드 그룹 자체에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

이 필드 그룹을 사용하여 Adobe Experience Platform Web SDK를 사용하여 Analytics 데이터를 수집하는 경우 [데이터스트림 구성](../../../edge/datastreams/overview.md) 를 사용하여 서버측에서 XDM에 데이터를 매핑하는 방법을 알아봅니다.
