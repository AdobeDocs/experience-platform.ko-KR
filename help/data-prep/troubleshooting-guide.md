---
keywords: Experience Platform;홈;인기 있는 주제;
title: 데이터 준비 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform 데이터 준비에 대해 자주 묻는 질문에 대한 답변을 제공합니다.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# [!DNL Data Prep] 문제 해결 안내서

이 문서에서는 Adobe Experience Platform [!DNL Data Prep]에 대해 자주 묻는 질문에 대한 답변과 일반적인 오류에 대한 문제 해결 안내서를 제공합니다. 일반적으로 Platform API에 대한 질문 및 문제 해결 정보는 [Adobe Experience Platform API 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## FAQ

다음은 [!DNL Data Prep]과(와) 답변에 대한 FAQ 목록입니다.

### 변환 오류는 어떻게 해결됩니까?

[!DNL Data Prep]은(는) 모든 변환 오류를 발생한 열로 지역화합니다. 그 결과 해당 열이 무효화되고 나머지 행은 계속 처리됩니다. 이러한 변환 문제는 **경고**(으)로 기록됩니다. 정기적으로 경고를 검토하고 변형 문제를 고려하여 변형 논리를 조정하는 것이 좋습니다. 이렇게 하면 Experience Platform에 수집된 데이터의 품질이 향상됩니다.

변환 문제로 인해 **Required**(으)로 표시된 열이 무효화된 경우 행이 수집되지 않습니다. 부분 데이터 수집이 활성화되면 전체 흐름이 실패하기 전에 이러한 거부의 임계값을 설정할 수 있습니다. 무효화된 속성이 스키마 수준 유효성 검사에 영향을 주지 않았다면 행은 계속 수집됩니다.

변환 오류가 없더라도 유효하지 않은 모든 행도 거부됩니다. 예를 들어 데이터 수집 흐름에는 필수 필드에 대한 통과 매핑(변환 논리 없음)이 있을 수 있으며 해당 속성에 대한 들어오는 값이 없습니다. 이 행은 거부됩니다.

### 필드에 있는 특수 문자를 어떻게 이스케이프 처리할 수 있습니까?

`${...}`을(를) 사용하여 필드의 특수 문자를 이스케이프 처리할 수 있습니다. 그러나 마침표(`.`)가 있는 필드가 포함된 JSON 파일은 이 메커니즘에서 지원되지 않습니다. 계층과 상호 작용할 때 자식 특성에 마침표(`.`)가 있으면 백슬래시(`\`)를 사용하여 특수 문자를 이스케이프 처리해야 합니다. 예를 들어 `address`은(는) 특성 `street.name`을(를) 포함하는 개체로, `address.street.name` 대신 `address.street\.name`로 참조할 수 있습니다.

### 계산된 필드의 최대 길이는 얼마입니까?

계산된 필드의 최대 길이는 4096자입니다.

### 속성에 대한 유효성 검사로 인해 수집에 실패했지만 내 파일에 해당 속성이 올바르게 있습니다. 정확히 무엇이 문제입니까?

각 필드의 데이터 형식이 스키마에 정의된 형식과 일치하는지 확인합니다. 또한 &quot;Required&quot;, &quot;enum&quot; 및 &quot;format&quot;과 같은 제약 조건을 준수해야 합니다.

수집되는 데이터는 Experience Platform에 정의된 XDM(Experience Data Model) 스키마를 준수해야 합니다. 속성이 스키마에 지정된 예상 유형 또는 형식과 일치하지 않으면 수집이 실패합니다.

데이터 준비 함수가 사용 중인 경우 변환이 올바른 속성을 가져오는지 확인하십시오. 소스 워크플로우의 설정 프로세스 중에 속성을 검토할 수 있습니다. 매핑 단계에서 **[!UICONTROL 새 필드 유형]**&#x200B;을 선택한 다음 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택합니다. 그런 다음 계산된 필드 인터페이스를 사용하여 각 함수를 미리 봅니다.

### 스트리밍 또는 일괄 처리 수집 레코드에서 잘못된 데이터 값을 제거하려면 어떻게 해야 합니까?

데이터 준비 매핑 인터페이스를 사용하여 필요한 데이터가 있는 열만 매핑하여 열 수준 필터링을 수행할 수 있습니다. 계산된 필드를 사용하여 지원 함수를 사용하여 데이터를 변환할 수도 있습니다.

행 수준 필터링은 현재 [Adobe Analytics 원본 커넥터](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering)에만 사용할 수 있습니다.

수집 후 데이터 Distiller를 사용하여 SQL을 사용하여 데이터를 정리, 셰이핑 및 조작할 수 있습니다. 그러나 이 프로세스에서는 잘못된 레코드가 있는 배치를 삭제하고 SQL 결과로 생성된 새 배치를 다시 수집해야 합니다.

>[!IMPORTANT]
>
>* 데이터 레이크: 이미 수집된 레코드는 레코드가 포함된 일괄 처리를 삭제하고 다시 수집하여 제거할 수 있습니다.
>
>* 실시간 고객 프로필: 새 레코드를 수집하여 속성 기반 레코드를 덮어쓸 수 있지만, 경험 이벤트 레코드는 제거할 수 없습니다.
>
>* Identity Service: Identity Service에서 레코드를 완전히 제거할 수 없습니다. 전체 프로필을 삭제하고 프로필 삭제 API를 사용하여 올바른 레코드로 프로필을 다시 업로드해야 합니다.

### GIF 데이터에서 계산된 필드를 사용하는 우수 사례는 무엇입니까?

소스 데이터를 XDM 스키마에 매핑하는 단계 동안 데이터 준비 매핑 함수를 사용하여 새 계산된 필드를 생성할 수 있습니다.

### Adobe Analytics 데이터를 소스로 가져오면 프로필에 대해 생성된 스키마가 자동으로 활성화됩니까?

Analytics 데이터는 프로필에 대해 자동으로 구성되지 않습니다. 소스 커넥터를 구성한 후에는 데이터 세트 및 스키마로 이동하여 프로필 수집에 사용하도록 설정해야 합니다.

프로덕션 샌드박스에서 Analytics 소스 데이터 흐름을 만들면 두 개의 데이터 흐름이 만들어집니다.

* 내역 보고서 세트 데이터를 데이터 레이크로 13개월 채우도록 하는 데이터 흐름입니다. 이 데이터 흐름은 채우기가 완료되면 종료됩니다.
* 라이브 데이터를 데이터 레이크 및 프로필로 전송하는 데이터 흐름입니다. 이 데이터 흐름은 지속적으로 실행됩니다.

### 데이터 준비 함수를 사용하여 맵 개체 내에서 하나의 값을 소문자로 설정하려면 어떻게 해야 합니까?

`map_get_values` 함수를 사용하여 값을 검색한 다음 소문자 함수를 사용하여 소문자로 만들 수 있습니다.

```shell
lower(map_get_values(mapObject, 'keyName'))
```

동일한 함수를 사용하여 맵 개체를 소문자로 바꿀 수 있습니다. 그러나 전체 맵을 반복하고 모든 항목을 소문자로 만들 수는 없습니다.

### 중첩된 방식으로 데이터 준비 기능을 사용할 수 있습니까?

예. 다른 함수 내에서 한 개의 데이터 준비 함수를 사용하여 데이터 수집 중에 복잡한 데이터 준비 기능을 해결할 수 있습니다.

예를 들어 특정 조건을 기반으로 필드를 null로 정의하려면 &quot;iif&quot; 함수를 사용하여 해당 필드를 확인할 수 있습니다. 함수가 `true`을(를) 반환하는 경우 &quot;dislify()&quot;를 사용하고 `false`을 반환하는 경우 해당 필드를 사용할 수 있습니다.

marketing_type이 필드인 경우 &quot;.equals&quot;를 사용하여 marketing_type 필드의 값을 확인할 수 있으며 &quot;iif&quot; 함수 내에 중첩될 수 있습니다. `true`을(를) 반환하는 경우 다음과 같이 &quot;dislify()&quot; 함수를 사용할 수 있습니다.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

다음은 iif, 같음 및 무효화를 사용하여 데이터 준비 기능을 중첩할 수 있는 방법의 예입니다.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| --- | --- | --- | --- | --- | --- |
| iif | 주어진 부울 표현식을 평가하고 결과를 기반으로 지정된 값을 반환합니다. | <ul><li>식: **필수** 계산 중인 부울 식입니다.</li><li>TRUE_VALUE: **필수** 식이 true로 평가되는 경우 반환되는 값입니다.</li><li>FALSE_VALUE: **필수** 식이 false로 평가되는 경우 반환되는 값입니다.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| 같음 | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분합니다. | <ul><li>STRING1: **필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2: **필수** 비교할 두 번째 문자열입니다. | 문자열1&#x200B;.equals(&#x200B;STRING2) | &quot;string1&quot;. &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| 무효화 | 속성 값을 null로 설정합니다. 필드를 대상 스키마에 복사하지 않으려는 경우 사용해야 합니다. | | 무효화() | 무효화() | null |

{style="table-layout:auto"}

다음은 평가 중인 필드가 &quot;marketing_type&quot;이라고 가정하고 함수를 중첩할 수 있는 방법의 예입니다.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

다음으로, 다음 세 가지 필드가 있습니다.

* marketing_type: (이메일, phyMail, 푸시, sms, 전화)
* total_consents: 4000에서 5500까지의 숫자 범위
* 날짜: 2024년 2월부터 3월까지

위에 나열된 세 가지 함수를 사용하고 중첩하여 세 필드를 조작할 수 있습니다.

* iif(marketing_type.equals(&quot;email&quot;), dislify(), iif(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), iif(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type))
* iif(total_consents > 5000, iif(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;infficient-consents&quot;)
* iif(date.equals(&quot;3/21/24&quot;), iif(marketing_type.equals(&quot;push&quot;), dislify(), marketing_type), &quot;not-Marketing&quot;)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-consent-sms&quot;, marketing_type), &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_consents > 5000, nullify(), &quot;email-low-consents&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consents &lt; 4500, &quot;low-consent-push&quot;, dislify()), marketing_type)
* iif(total_consents >= 5500, iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-consents&quot;), marketing_type)