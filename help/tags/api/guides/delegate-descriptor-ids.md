---
title: 위임 설명자 ID
description: Reactor API의 위임 설명자 ID와 이것이 리소스를 확장과 연결하는 방법에 대해 알아봅니다.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 위임 설명자 ID

Adobe Experience Platform에서 태그를 사용할 때 사이트에서 배포할 수 있는 모든 기능은 확장에서 제공합니다. 각 확장에서 제공하는 기능은 확장 개발자가 정의합니다. 확장이 배포되면 [확장 패키지](../endpoints/extension-packages.md) 형식으로 다양한 기능과 함께 번들로 제공됩니다. 개발자가 확장 패키지에 추가하는 기능은 해당 패키지의 &quot;위임&quot;으로 간주됩니다.

확장 패키지 내의 각 대리자에게는 고유한 위임 설명자 ID가 제공됩니다. 특정 리소스에 대한 위임 설명자 ID는 시스템의 리소스 종류와 해당 리소스가 속한 확장 패키지를 알려줍니다.

## 구문

대리자 설명자 ID는 확장 패키지 이름, 대리자 형식 및 대리자 이름을 각각 나타내는 이중 콜론 문자(`::`)로 연결된 3개의 문자열로 구성됩니다. 이러한 문자열은 사람이 읽을 수 있도록 구성되며 확장 패키지가 수집될 때 시스템에서 자동으로 생성되고 할당됩니다.

예를 들어, 확장 패키지 `example-package`에 `custom-code`(이)라는 작업이 있는 경우 해당 작업에는 다음 위임 설명자 ID가 있습니다. `example-package::actions::custom-code`.

## 해당 리소스에 위임 설명자 ID 사용

위임 설명자 ID는 API에서 규칙 구성 요소(이벤트, 조건 및 작업)와 데이터 요소를 정의할 때 이해하는 데 중요합니다. 아래 섹션에서는 각 리소스에 대해 이러한 ID가 어떻게 작동되는지에 대해 간략히 설명합니다.

### 규칙 구성 요소

[규칙 구성 요소](../endpoints/rule-components.md)은(는) 확장 패키지에 속하는 이벤트, 조건 또는 작업에 연결되어 있어야 합니다. 전체 규칙 논리(이벤트, 조건 또는 작업)와 관련된 규칙 구성 요소의 &quot;유형&quot;을 나타냅니다. 따라서 규칙 구성 요소를 만들 때 규칙 구성 요소와 연결해야 하는 이벤트, 조건 또는 작업을 나타내는 위임 설명자 ID를 제공해야 합니다.

예를 들어 확장 패키지 `example-package`에서 `click` 이벤트를 기반으로 하는 이벤트 규칙 구성 요소를 만들려면 규칙 구성 요소는 `delegate_descriptor_id` 값 `example-package::events::click`을(를) 사용합니다.

자세한 내용은 [규칙 구성 요소 만들기](../endpoints/rule-components.md#create)에 대한 섹션을 참조하십시오.

### 데이터 요소

[데이터 요소](../endpoints/data-elements.md)은(는) 처음 만들 때 확장 패키지와 연결되어야 합니다. 각 확장 패키지는 대리자 데이터 요소와 의도한 동작에 대해 호환 가능한 형식을 정의합니다.

예를 들어, 확장 패키지 `example-package`에 정의된 대로 `cookie` 형식을 사용하는 데이터 요소를 만들려면 데이터 요소는 `delegate_descriptor_id` 값 `example-package::dataElements::cookie`을(를) 사용합니다.

자세한 내용은 [데이터 요소 만들기](../endpoints/data-elements.md#create) 섹션을 참조하십시오.

### 확장

[extension](../endpoints/extensions.md)은(는) 처음 만들 때 확장 패키지와 자동으로 연결되며 확장의 `relationships` 개체 내에 표시됩니다. 확장에 사용자 지정 설정이 필요한 경우 위임 설명자 ID도 필요합니다.

>[!NOTE]
>
>사용자 지정 설정이 필요하지 않은 확장에는 위임 설명자 ID가 필요하지 않습니다.

예를 들어 확장 패키지 `example-package`에 속하는 확장에 위임 설명자 ID를 추가하려면 확장에서 다음 `delegate_descriptor_id` 값을 사용합니다. `example-package::extensionConfiguration::config`.

자세한 내용은 [확장 만들기](../endpoints/extensions.md#create)에 대한 안내서를 참조하십시오.
