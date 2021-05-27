---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;ID;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: ID 데이터 유형
topic-legacy: overview
description: 이 문서에서는 ID XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 3%

---

#  ID 데이터 유형

 ID는 디지털 경험과 상호 작용하는 사용자를 명확하게 구분하는 데 사용되는 표준 XDM 데이터 유형입니다. ID는 ID 공급자가 설정하며, ID 공급자는 `namespace` 속성에서 참조됩니다. 각 `namespace` 내에서 ID는 고유합니다.

<img src="../images/data-types/identity.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `namespace` | 개체 | 제공된 `id` 속성과 연관된 네임스페이스를 나타내는 단일 문자열 필드(`code`)가 포함된 객체입니다. |
| `authenticatedState` | 문자열 | 관찰된 경험 이벤트 시 이 ID에 대한 인증된 상태입니다. 허용되는 값 및 정의는 [부록](#authenticatedState)을 참조하십시오. |
| `id` | 문자열 | 관련 네임스페이스에서 소비자의 ID입니다. |
| `primary` | 부울 | 개인이 기본 ID인지 여부를 나타냅니다. 각 개인은 하나의 기본 ID만 가질 수 있습니다. |
| `xid` | 문자열 | 이 값은 모든 네임스페이스에서 모든 네임스페이스 범위 식별자에서 고유한 네임스페이스 간 식별자를 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 부록

다음 섹션에는 [!UICONTROL Identity] 데이터 유형에 대한 추가 정보가 들어 있습니다.

## authenticatedState에 대해 허용되는 값 {#authenticatedState}

다음 표에서는 `authenticatedState`에 대해 허용되는 값과 관련된 의미에 대해 설명합니다.

| 값 | 설명 |
| --- | --- |
| `ambiguous` | 인증된 상태가 모호합니다. |
| `authenticated` | 사용자가 이벤트 관찰 시 유효한 로그인 또는 유사한 동작으로 식별되었습니다. |
| `loggedOut` | 사용자가 이전 특정 시점에 로그인 동작으로 식별되었지만 이벤트 관찰 시에 로그인되지 않았습니다. |
