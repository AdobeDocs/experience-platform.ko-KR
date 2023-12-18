---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;ID;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: ID 데이터 유형
description: ID XDM 데이터 유형에 대해 알아봅니다.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# [!UICONTROL 신원] 데이터 유형

[!UICONTROL 신원] 는 디지털 경험과 상호 작용하는 사용자를 명확하게 구분하는 데 사용되는 표준 XDM 데이터 유형입니다. ID 공급자에 의해 ID가 설정되며, ID 제공자 자체에서 참조됨 `namespace` 특성. 각 항목 내 `namespace`, ID는 고유합니다.

<img src="../images/data-types/identity.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `namespace` | 오브젝트 | 단일 문자열 필드를 포함하는 개체(`code`): 제공된 와 연결된 네임스페이스를 나타냅니다. `id` 특성. |
| `authenticatedState` | 문자열 | 관찰된 경험 이벤트 당시 이 ID에 대한 인증 상태입니다. 다음을 참조하십시오. [부록](#authenticatedState) 허용되는 값 및 정의용. |
| `id` | 문자열 | 관련 네임스페이스의 소비자 ID. |
| `primary` | 부울 | 개인의 기본 ID인지 여부를 나타냅니다. 각 개인은 하나의 기본 ID만 가질 수 있습니다. |
| `xid` | 문자열 | 존재하는 경우 해당 값은 모든 네임스페이스의 모든 네임스페이스 범위 식별자에서 고유한 크로스 네임스페이스 식별자를 나타냅니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 부록

다음 섹션은 다음에 대한 추가 정보를 포함합니다. [!UICONTROL 신원] 데이터 유형.

## authenticatedState에 대해 허용되는 값 {#authenticatedState}

다음 표에서 허용되는 값을 간략하게 설명합니다. `authenticatedState` 및 관련 의미:

| 값 | 설명 |
| --- | --- |
| `ambiguous` | 인증된 상태가 모호합니다. |
| `authenticated` | 사용자는 이벤트 관찰 시 유효한 로그인 또는 유사한 동작으로 식별되었습니다. |
| `loggedOut` | 사용자는 이전의 특정 시점에 로그인 작업으로 확인되었지만 이벤트 관찰 당시에는 로그인되지 않았습니다. |
