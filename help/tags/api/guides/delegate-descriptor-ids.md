---
title: 위임 설명자 ID
description: Reactor API의 위임 설명자 ID 및 리소스를 확장과 연결하는 방법에 대해 알아봅니다.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 위임 설명자 ID

Adobe Experience Platform에서 태그를 사용할 때 사이트에서 배포할 수 있는 모든 기능은 확장에서 제공합니다. 각 확장에서 제공하는 기능은 확장 개발자가 정의합니다. 확장이 배포되면 [확장 패키지](../endpoints/extension-packages.md) 형태로 다양한 기능과 번들로 제공됩니다. 개발자가 확장 패키지에 추가하는 기능은 해당 패키지의 &quot;위임&quot;으로 간주됩니다.

확장 패키지 내의 각 대리자에게는 고유한 위임 설명자 ID가 제공됩니다. 특정 리소스에 대한 위임 설명자 ID는 시스템에 어떤 리소스 종류 및 어떤 확장 패키지가 속하는지 알려줍니다.

## 구문

위임 설명자 ID는 각각 확장 패키지 이름, 위임 유형 및 위임 이름을 나타내는 이중 콜론 문자(`::`)로 연결된 세 개의 문자열로 구성됩니다. 이러한 문자열은 사람이 읽을 수 있도록 작성되며, 확장 패키지를 수집할 때 시스템에서 자동으로 생성 및 할당됩니다.

예를 들어, `example-package` 확장 패키지에 `custom-code` 작업이 있는 경우 해당 작업에는 다음 위임 설명자 ID가 있습니다. `example-package::actions::custom-code`

## 적용 가능한 리소스에 위임 설명자 ID 사용

위임 설명자 ID는 API에서 규칙 구성 요소(이벤트, 조건 및 작업)와 데이터 요소를 정의하는 시점을 이해하는 데 중요합니다. 아래 섹션에서는 각 리소스에 대해 이러한 ID가 재생되는 방법을 간략하게 설명합니다.

### 규칙 구성 요소

[규칙 구성 요소](../endpoints/rule-components.md)는 확장 패키지에 속하는 이벤트, 조건 또는 작업과 연결되어 있어야 합니다. 전체 규칙(이벤트, 조건 또는 작업)의 논리와 관련이 있는 규칙 구성 요소의 &quot;유형&quot;을 나타냅니다. 따라서 규칙 구성 요소를 만들 때 규칙 구성 요소와 연관되어야 하는 이벤트, 조건 또는 작업을 나타내는 위임 설명자 ID를 제공해야 합니다.

예를 들어, 확장 패키지 `example-package`에서 `click` 이벤트를 기반으로 하는 이벤트 규칙 구성 요소를 만들려면 규칙 구성 요소에서 다음 `delegate_descriptor_id` 값을 사용합니다. `example-package::events::click`.

자세한 내용은 [규칙 구성 요소](../endpoints/rule-components.md#create) 만들기 섹션을 참조하십시오.

### 데이터 요소

각 확장 패키지는 위임 데이터 요소에 대한 호환 유형과 의도한 동작을 정의하므로 [데이터 요소](../endpoints/data-elements.md)를 처음 만들 때 확장 패키지와 연결해야 합니다.

예를 들어 확장 패키지 `example-package`에 정의된 대로 `cookie` 유형을 사용하는 데이터 요소를 만들려면 데이터 요소는 다음 `delegate_descriptor_id` 값을 사용합니다. `example-package::dataElements::cookie`.

자세한 내용은 [데이터 요소 만들기](../endpoints/data-elements.md#create)의 섹션을 참조하십시오.

### 확장

[확장](../endpoints/extensions.md)은 처음 만들 때 확장 패키지와 자동으로 연결되며, 확장의 `relationships` 개체 내에 표시됩니다. 확장에는 사용자 지정 설정이 필요한 경우 위임 설명자 ID도 필요합니다.

>[!NOTE]
>
>사용자 지정 설정이 필요하지 않은 확장에는 위임 설명자 ID가 필요하지 않습니다.

예를 들어 확장 패키지 `example-package`에 속하는 확장에 위임 설명자 ID를 추가하려면 확장에서 다음 `delegate_descriptor_id` 값을 사용합니다. `example-package::extensionConfiguration::config`

자세한 내용은 [확장 만들기](../endpoints/extensions.md#create)의 안내서를 참조하십시오.