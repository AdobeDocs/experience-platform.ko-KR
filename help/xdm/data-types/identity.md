---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;ID;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: ID 데이터 유형
description: 이 문서에서는 ID XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

# [!UICONTROL ID] 데이터 유형

[!UICONTROL ID] 는 디지털 경험과 상호 작용하는 사용자를 명확하게 구분하는 데 사용되는 표준 XDM 데이터 유형입니다. ID는 ID 공급자에서 참조되는 ID 공급자에 의해 설정됩니다 `namespace` 속성을 사용합니다. 각 `namespace`, id 는 고유합니다.

<img src="../images/data-types/identity.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `namespace` | 오브젝트 | 단일 문자열 필드(`code`). `id` 속성을 사용합니다. |
| `authenticatedState` | 문자열 | 관찰된 경험 이벤트 시 이 ID에 대한 인증된 상태입니다. 자세한 내용은 [부록](#authenticatedState) 참조하십시오. |
| `id` | 문자열 | 관련 네임스페이스에서 소비자의 ID입니다. |
| `primary` | 부울 | 개인이 기본 ID인지 여부를 나타냅니다. 각 개인은 하나의 기본 ID만 가질 수 있습니다. |
| `xid` | 문자열 | 이 값은 모든 네임스페이스에서 모든 네임스페이스 범위 식별자에서 고유한 네임스페이스 간 식별자를 나타냅니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 부록

다음 섹션에는 [!UICONTROL ID] 데이터 유형.

## authenticatedState에 대해 허용되는 값 {#authenticatedState}

다음 표에서는 `authenticatedState` 그리고 그들의 연관 의미는 다음과 같습니다.

| 값 | 설명 |
| --- | --- |
| `ambiguous` | 인증된 상태가 모호합니다. |
| `authenticated` | 사용자가 이벤트 관찰 시 유효한 로그인 또는 유사한 동작으로 식별되었습니다. |
| `loggedOut` | 사용자가 이전 특정 시점에 로그인 동작으로 식별되었지만 이벤트 관찰 시에 로그인되지 않았습니다. |
