---
solution: Experience Platform
title: 범용 마케팅 기본 설정 필드 데이터 유형
topic: overview
description: 이 문서에서는 범용 마케팅 기본 설정 필드 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5ec59e609fda66d379847dca068d19d4cce8228
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 2%

---


# [!UICONTROL Generic Marketing Preference Field] 데이터 유형

[!UICONTROL Generic Marketing Preference Field] 은 특정 마케팅 기본 설정에 대한 고객의 선택을 설명하는 표준 XDM 데이터 유형입니다.

>[!NOTE]
>
>이 데이터 유형은 [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixin](../mixins/profile/consents.md)을 기준선으로 사용하여 조직의 동의 스키마 구조를 사용자 지정하는 데 사용됩니다.
>
>특정 마케팅 환경 설정 필드에 `subscriptions` 맵이 필요한 경우 대신 구독 데이터 유형](./marketing-field-subscriptions.md)이 있는 [마케팅 필드를 사용해야 합니다.

![](../images/data-types/marketing-field.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `reason` | 문자열 | 고객이 마케팅 사용 사례를 옵트아웃할 때 이 문자열 필드는 고객이 옵트아웃한 이유를 나타냅니다. |
| `time` | DateTime | 해당되는 경우 마케팅 기본 설정이 변경된 시점의 ISO 8601 타임스탬프. |
| `val` | 문자열 | 이 마케팅 사용 사례에 대해 고객이 제공한 환경 설정 선택 사항입니다. 허용되는 값과 정의는 아래 표를 참조하십시오. |

다음 표에서는 `val`에 대해 허용된 값에 대해 대략적으로 설명합니다.

| 값 | Title | 설명 |
| --- | --- | --- |
| `y` | 예 | 고객이 선호하는 것을 선택하였습니다. 즉, 해당 기본 설정에서 지정한 대로 해당 데이터의 사용에 대해 **do** 동의가 있습니다. |
| `n` | 아니요 | 고객이 선호하는 옵션을 선택 해제했습니다. 즉, **은(는) 해당 기본 설정에서 지정한 대로 해당 데이터의 사용에 동의하지 않습니다.** |
| `p` | 보류 중인 확인 | 시스템에 최종 환경 설정 값이 아직 수신되지 않았습니다. 이것은 2단계 확인이 필요한 동의의 일부로서 가장 자주 사용됩니다. 예를 들어 고객이 이메일 수신을 거부하는 경우, 해당 동의는 이메일 링크를 선택하여 올바른 이메일 주소를 제공했는지 확인할 때까지 `p`로 설정됩니다. 이 경우 동의는 `y`로 업데이트됩니다.<br><br>이 기본 설정이 2개의 확인 프로세스를 사용하지 않는 경우, 대신 고객이 아직 동의 프롬프트에 응답하지  `p` 않았음을 나타내는 옵션을 사용할 수 있습니다. 예를 들어 고객이 동의 프롬프트에 응답하기 전에 웹 사이트의 첫 페이지에서 값을 `p`으로 자동으로 설정할 수 있습니다. 명시적 동의가 필요하지 않은 관할 지역에서는 고객이 명시적으로 선택하지 않았음을 나타내기 위해 사용할 수도 있습니다(즉, 동의는 가정됨). |
| `u` | 알 수 없음 | 고객의 환경 설정 정보를 알 수 없습니다. |
| `LI` | 합법적인 관심 | 특정 목적에 맞게 이 데이터를 수집 및 처리하는 합법적인 비즈니스 이익은 개인에게 미칠 수 있는 잠재적인 해를 초과합니다. |
| `CT` | 계약 | 특정 목적을 위해 데이터를 수집하려면 개인 사용자와 계약 의무를 충족해야 합니다. |
| `CP` | 법적 의무 준수 | 기업의 법적 책임을 충족하기 위해서는 특정 목적에 대한 데이터를 수집해야 합니다. |
| `VI` | 개인의 중요한 관심 | 특정 목적을 위해 데이터를 수집하여 개인의 중요한 이익을 보호해야 합니다. |
| `PI` | 공익 | 특정 목적을 위한 자료의 수집은 공익적 또는 공권력의 행사에 필요한 것이다. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)