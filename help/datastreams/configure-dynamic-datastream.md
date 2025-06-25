---
title: 동적 데이터 스트림 구성 만들기
description: 규칙을 기반으로 다양한 Experience Cloud 서비스로 데이터를 라우팅하기 위해 동적 데이터스트림 구성을 만드는 방법을 알아봅니다.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
exl-id: 528ddf89-ad87-4021-b5a6-8e25b4469ac4
source-git-commit: c193a6aa45d179acdf655a70987875bf0da51b2b
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 3%

---

# 동적 데이터 스트림 구성 만들기

>[!AVAILABILITY]
>
>* 동적 데이터스트림 구성을 정의하는 옵션은 현재 Beta에 있으며 제한된 수의 고객이 사용할 수 있습니다. 이 기능에 대한 액세스 권한을 받으려면 Adobe 담당자에게 문의하십시오. 설명서 및 기능은 변경될 수 있습니다.

기본적으로 Experience Platform Edge Network은 데이터 스트림에 도달하는 모든 이벤트를 데이터 스트림에 대해 활성화한 모든 Experience Cloud [서비스](configure.md#add-services)로 보냅니다. 사용 사례에 따라 항상 적합한 워크플로는 아닐 수 있습니다.

동적 데이터스트림 구성은 데이터스트림에 대해 활성화된 각 서비스에 대해 정의하는 사용자 구성 가능한 규칙 세트를 통해 이러한 문제를 해결합니다. 이는 각 데이터 유형을 받아야 하는 Experience Cloud 솔루션을 지정합니다.

## 전제 조건 {#prerequisites}

데이터 스트림에 대한 동적 구성을 만들려면 다음 두 가지 조건을 충족해야 합니다.

* 작업할 데이터 스트림을 *최소*&#x200B;개 만들어야 합니다. 자세한 내용은 [데이터 스트림을 만드는 방법](configure.md)에 대한 설명서를 참조하십시오.
* 데이터 스트림에 *최소*&#x200B;개의 Experience Cloud 서비스가 추가되어 있어야 합니다. 자세한 내용은 데이터스트림에 [서비스를 추가](configure.md#add-services)하는 방법에 대한 설명서를 참조하십시오.

데이터 스트림을 만들고 Experience Cloud 서비스를 추가한 후 [동적 구성을 만들](#create-dynamic-configuration)수 있습니다.

## 가드레일 {#guardrails}

동적 데이터스트림 구성에는 최적의 시스템 성능 및 데이터 처리 효율성을 보장하기 위한 특정 제한 및 성능 제한이 있습니다. 동적 데이터스트림 규칙을 구성할 때 다음 보호 기능이 적용됩니다.

| 가드레일 | 제한 | 제한 유형 |
|---------|------------|------|
| Experience Platform 서비스의 데이터스트림당 최대 동적 데이터스트림 구성 수 | 5 | 성능 보호 |
| Adobe Analytics에 대한 데이터스트림당 최대 동적 데이터스트림 구성 수 | 5 | 성능 보호 |
| Adobe Target에 대한 데이터스트림당 최대 동적 데이터스트림 구성 수 | 5 | 성능 보호 |
| Adobe Audience Manager에 대한 데이터스트림당 최대 동적 데이터스트림 구성 수 | 5 | 성능 보호 |
| 단일 규칙 내에서 결합할 수 있는 최대 조건 수(술어) | 10 | 성능 보호 |
| 시간 초과 전에 데이터스트림당 모든 동적 데이터스트림 구성을 평가하는 데 허용된 최대 시간 | 25밀리초 | 시스템 강제 보호 |

## 동적 데이터스트림 구성 및 데이터스트림 구성 재정의 {#dynamic-versus-overrides}

동적 데이터 스트림 구성 및 [데이터 스트림 구성 재정의](overrides.md)는 함께 사용할 수 없는 기능입니다.

즉, 동적 데이터스트림 구성을 데이터스트림 구성 재정의와 함께 사용할 수 없습니다. 둘 중 하나를 선택해야 합니다.

동적 데이터스트림 구성 및 데이터스트림 구성 재정의를 모두 활성화하면 구성 재정의가 우선하며 동적 데이터스트림 구성 규칙이 무시됩니다.

## 동적 데이터 스트림 구성 만들기 {#create-dynamic-configuration}

[데이터 스트림을 만들고](configure.md)에 [서비스를 추가](configure.md#add-services)한 후 아래 단계에 따라 서비스에 동적 구성을 추가하십시오.

1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 데이터스트림]** 페이지로 이동하여 만든 데이터스트림을 선택합니다.

   ![데이터스트림 목록을 표시하는 데이터스트림 사용자 인터페이스의 이미지](assets/configure-dynamic-datastream/select-datastream.png)

1. 동적 구성을 정의할 서비스에서 **[!UICONTROL 편집]** 옵션을 선택하십시오.

   ![데이터스트림에 추가된 서비스를 보여 주는 데이터스트림 사용자 인터페이스의 이미지입니다.](assets/configure-dynamic-datastream/select-service.png)

1. **[!UICONTROL 구성]** 페이지에서 **[!UICONTROL 동적 구성 저장 및 편집]**&#x200B;을 선택합니다.

   ![데이터스트림 구성 페이지를 표시하는 데이터스트림 사용자 인터페이스 이미지.](assets/configure-dynamic-datastream/save-and-edit.png)

1. **[!UICONTROL 동적 구성 추가]**&#x200B;를 선택합니다.

   ![규칙 추가 없는 동적 구성을 보여 주는 데이터스트림 사용자 인터페이스의 이미지입니다.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. **[!UICONTROL 리소스]** 패널에서 규칙을 작성할 항목을 창의 오른쪽으로 끌어다 놓습니다. 여러 리소스를 결합하여 복잡한 규칙을 작성할 수 있습니다.

   **[!UICONTROL 같음]**, **[!UICONTROL 같지 않음]**, **[!UICONTROL 존재]** 등과 같은 각 리소스의 옵션을 사용하여 규칙을 미세 조정하십시오.

   ![동적 구성 규칙을 표시하는 데이터스트림 사용자 인터페이스의 이미지](assets/configure-dynamic-datastream/drag-resources.png)

1. **[!UICONTROL 구성]** 섹션에서 데이터를 각 서비스로 전송할지 여부에 따라 각 규칙에 대해 활성화하거나 비활성화할 서비스를 전환합니다. 토글을 끄면 서비스 라우팅이 비활성화되고 *데이터가 업스트림 서비스로 전송되지 않습니다*.

   ![동적 구성 규칙을 표시하는 데이터스트림 사용자 인터페이스의 이미지](assets/configure-dynamic-datastream/enable-service.png)

1. 규칙 구성이 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

## 규칙 우선 순위 고려 사항 {#considerations}

각 동적 데이터스트림 구성에 대해 여러 규칙을 정의할 수 있습니다. 그러나 데이터가 여러 규칙의 조건과 일치하는 경우 목록의 첫 번째 일치하는 규칙만 고려되며 다른 모든 일치하는 규칙은 무시됩니다.

원하는 데이터 라우팅 동작을 달성하려면 규칙을 정렬하는 순서에 주의하십시오.

규칙 순서를 구성하려면 규칙 창을 원하는 순서로 드래그 앤 드롭할 수 있습니다.

![끌어다 놓기를 통해 규칙 순서를 변경하는 방법을 보여 주는 GIF.](assets/configure-dynamic-datastream/move-rules.gif)

## 규칙 자격 기준 {#eligibility-criteria}

동적 데이터스트림 구성은 성능, 유지 관리 및 명확성을 보장하기 위해 특정 자격 기준을 충족해야 합니다. 아래는 규칙을 정의하기 위한 주요 요구 사항 및 모범 사례입니다.

### 지원되는 데이터 유형 {#supported-data-types}

동적 데이터스트림 구성 규칙은 최적의 성능과 안정적인 데이터 라우팅을 보장하기 위해 특정 데이터 유형과 함께 작동합니다. 지원되는 데이터 유형을 이해하면 데이터를 효율적으로 처리하는 효과적인 규칙을 만드는 데 도움이 됩니다.

| 데이터 유형 | 상태 | 참고 |
|-----------|--------|-------|
| 문자열 | 허용됨 | - |
| 숫자(정수, 긴, 짧은, 바이트) | 허용됨 | - |
| 열거형 | 허용됨 | - |
| 부울 | 허용됨 | - |
| 일자 | 허용됨 | - |
| 배열 | 허용되지 않음 | 스토리지를 기반으로 하는 규칙은 지원되지 않습니다. 성능이 저하될 수 있습니다. |
| 맵 | 허용되지 않음 | 맵을 기반으로 한 규칙은 성능을 저하시킬 수 있으므로 지원되지 않습니다. |

### 지원되는 연산자 {#supported-operators}

규칙은 데이터 유형에 따라 다음 연산자를 사용할 수 있습니다.

| 데이터 유형 | 지원되는 연산자 |
|-----------|-------------------|
| **문자열** | `equals`, `starts with`, `ends with`, `contains`, `exists`, `does not equal`, `does not start with`, `does not end with`, `does not contain`, `does not exist` |
| **숫자(긴, 정수, 짧은, 바이트)** | `equals`, `does not equal`, `greater than`, `less than`, `greater than or equal to`, `less than or equal to`, `exists`, `does not exist` |
| **부울** | `equals true/false`, `does not equal true/false` |
| **열거형** | `equals`, `does not equal`, `exists`, `does not exist` |
| **날짜** | `today`, `yesterday`, `this month`, `this year`, `custom date`, `in last`, `from`, `during`, `within`, `before`, `after`, `rolling range`, `in next`, `exists`, `does not exist` |
| **논리** | `INCLUDE`, `ANY/ALL`(AND/OR에 해당) |

>[!NOTE]
>
>**[!UICONTROL EXCLUDE]** 연산자는 직접 지원되지 않지만, 무시된 비교 연산자(예: &quot;같지 않음&quot;)와 함께 **[!UICONTROL INCLUDE]**&#x200B;을(를) 사용하여 동등한 논리를 얻을 수 있습니다.

### 규칙 구조 {#rule-structure}

동적 데이터스트림 구성에 대한 규칙을 생성할 때 최적의 성능과 시스템 호환성을 보장하는 구조적 요구 사항을 이해하는 것이 중요합니다. 규칙 구조는 데이터를 얼마나 효율적으로 처리하고 시스템을 통해 라우팅되는지에 직접적인 영향을 미칩니다.

**단순 식만 사용**. 규칙을 단순 논리 표현식으로 정의해야 합니다. 중첩된 논리 표현식(컨테이너 또는 여러 수준의 AND/OR 사용)은 지원되지 않습니다. 복잡한 논리가 필요한 경우 여러 플랫 규칙으로 나눕니다.

예를 들어 아래 이미지에 표시된 복잡한 규칙을 생각해 보십시오.

![복잡한 규칙을 표시하는 플랫폼 UI 이미지입니다.](assets/configure-dynamic-datastream/complex-rule.png)

이 규칙을 다음과 같은 간단한 규칙으로 나눌 수 있습니다.

![복잡한 규칙을 표시하는 플랫폼 UI 이미지입니다.](assets/configure-dynamic-datastream/simple-rule-1.png)

![복잡한 규칙을 표시하는 플랫폼 UI 이미지입니다.](assets/configure-dynamic-datastream/simple-rule-2.png)

**복잡한 규칙을 사용하지 마십시오**. 더 간단한 규칙을 통해 보다 신속하게 평가하고 유지 관리할 수 있습니다.

### 모범 사례 {#best-practices}

동적 데이터스트림 구성 규칙을 생성할 때 다음 모범 사례를 통해 최적의 성능, 시스템 안정성 및 유지 관리 가능한 구성을 보장합니다. 이러한 지침은 일반적인 위험을 방지하고 플랫폼 아키텍처와 원활하게 작동하는 효율적인 규칙을 만드는 데 도움이 됩니다.

* **규칙을 단순하고 단순하게 유지합니다.** 복잡한 논리를 표현해야 하는 경우 중첩 대신 여러 규칙을 사용하십시오.
* **[지원되는 데이터 형식](#supported-data-types) 및 [연산자](#supported-operators)만 사용**
* **성능을 위해 규칙을 테스트합니다.** 너무 복잡하거나 지원되지 않는 규칙으로 인해 시스템이 해당 규칙을 거부하거나 시스템 성능에 영향을 줄 수 있습니다.





