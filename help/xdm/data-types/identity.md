---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: ID 데이터 유형
topic: overview
description: 이 문서에서는 ID XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---


# [!UICONTROL ID] 데이터 유형

[!UICONTROL ID는] 디지털 경험과 상호 작용하는 사용자를 명확하게 구분하는 데 사용되는 표준 XDM 데이터 유형입니다. ID는 ID 공급자가 설정하며, 이 ID는 `namespace` 속성에서 참조됩니다. 각 ID `namespace`는 고유합니다.

<img src="../images/data-types/identity.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `namespace` | 개체 | 제공된 속성과 연결된 네임스페이스를 나타내는 단일 문자열 필드(`code`)가 들어 있는 `id` 개체입니다. |
| `authenticatedState` | 문자열 | 관찰된 경험 이벤트 시 이 ID에 대한 인증된 상태입니다. 허용되는 값 및 정의는 [부록을](#authenticatedState) 참조하십시오. |
| `id` | 문자열 | 관련 네임스페이스에 있는 소비자의 ID입니다. |
| `primary` | 부울 | 개인 ID인지 여부를 나타냅니다. 각 개인은 하나의 기본 ID만 가질 수 있습니다. |
| `xid` | 문자열 | 이 값은 모든 네임스페이스의 모든 네임스페이스 범위 식별자에 대해 고유한 상호 네임스페이스 식별자를 나타냅니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 부록

다음 섹션에는 [!UICONTROL ID] 데이터 유형에 대한 추가 정보가 포함되어 있습니다.

## authenticatedState에 대해 허용된 값 {#authenticatedState}

다음 표에서는 해당 의미와 관련하여 허용된 값에 대해 `authenticatedState` 개괄적으로 설명합니다.

| 값 | 설명 |
| --- | --- |
| `ambiguous` | 인증된 상태는 모호합니다. |
| `authenticated` | 사용자가 이벤트 관찰 시 유효한 로그인 또는 유사한 동작으로 식별되었습니다. |
| `loggedOut` | 사용자가 이전 시점의 로그인 동작으로 식별되었지만 이벤트 관찰 당시에 로그인하지 않았습니다. |