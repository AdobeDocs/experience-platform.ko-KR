---
solution: Experience Platform
title: 가입 데이터 유형이 있는 범용 마케팅 환경 설정 필드
topic-legacy: overview
description: 이 문서에서는 구독 XDM 데이터 유형이 있는 범용 마케팅 기본 설정 필드에 대한 개요를 제공합니다.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# [!UICONTROL Generic Marketing Preference Field with Subscriptions] 데이터 유형

[!UICONTROL Generic Marketing Preference Field with Subscriptions] 은 특정 마케팅 기본 설정에 대한 고객의 선택을 설명하는 표준 XDM 데이터 유형입니다.

>[!NOTE]
>
>이 데이터 유형은 [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] 필드 그룹](../field-groups/profile/consents.md)을 기준선으로 사용하여 조직의 동의 스키마 구조를 사용자 지정하는 데 사용됩니다.
>
>특정 마케팅 환경 설정 필드에 `subscriptions` 맵이 필요하지 않은 경우 대신 [기본 마케팅 필드 데이터 유형](./marketing-field.md)을(를) 사용할 수 있습니다.

![](../images/data-types/marketing-field-subscriptions.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `reason` | 문자열 | 고객이 마케팅 사용 사례를 옵트아웃할 때 이 문자열 필드는 고객이 옵트아웃한 이유를 나타냅니다. |
| `subscriptions` | 맵 | 특정 구독에 대한 고객 마케팅 기본 설정 맵 자세한 내용은 [구독](#subscriptions)의 섹션을 참조하십시오. |
| `time` | DateTime | 해당되는 경우 마케팅 기본 설정이 변경된 시점의 ISO 8601 타임스탬프. |
| `val` | 문자열 | 이 마케팅 사용 사례에 대해 고객이 제공한 환경 설정 선택 사항입니다. 허용되는 값과 정의는 [다음 섹션](#val)을 참조하십시오. |

## `val` {#val}

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

## `subscriptions` {#subscriptions}

일부 기업은 고객이 특정 마케팅 채널과 연관된 서로 다른 가입을 선택할 수 있도록 허용합니다. 예를 들어, 은행 회사는 고객이 초과 인출된 계정에 대해 전화 경고에 가입하도록 하거나 로열티 프로그램 오퍼에 대한 판매 요청을 받을 수 있습니다.

다음 JSON은 `subscriptions` 맵이 포함된 전화 통화 마케팅 채널에 대한 예제 마케팅 필드를 나타냅니다. `subscriptions` 개체의 각 키는 마케팅 채널에 대한 개별 구독을 나타냅니다. 그러면 각 구독에 옵트인 값(`val`)이 포함됩니다.

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 구독 유형입니다. 15자 이하일 경우 설명형 문자열일 수 있습니다. |
| `subscribers` | 특정 구독에 구독한 식별자 집합(예: 이메일 주소 또는 전화 번호)을 나타내는 선택적 맵 유형 필드입니다. 이 객체의 각 키는 해당 식별자를 나타내며 2개의 하위 속성을 포함합니다. <ul><li>`time`:해당되는 경우 ID가 가입된 시점의 ISO 8601 타임스탬프.</li><li>`source`:구독자가 생성한 소스입니다. 15자 이하일 경우 설명형 문자열일 수 있습니다.</li></ul> |

## 추가 리소스

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
