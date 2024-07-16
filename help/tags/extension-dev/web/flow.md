---
title: 웹 확장 흐름
description: Adobe Experience Platform에서 런타임 시 웹 확장 구성 요소가 서로 상호 작용하는 방법에 대해 알아봅니다.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 42%

---

# 웹 확장 흐름

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

웹 확장에서는 각 이벤트, 조건, 작업 및 데이터 요소 유형에 사용자에게 설정 수정 기능을 제공하는 보기와 사용자 정의 설정에 따라 작동하는 라이브러리 모듈이 모두 포함됩니다.

다음 고급 다이어그램에서와 같이 확장의 이벤트 유형 보기는 Adobe Experience Platform과 통합된 애플리케이션의 iframe 내에 표시됩니다. 그런 다음 사용자는 보기를 사용하여 설정을 수정하고 이 설정은 Platform 내에 저장됩니다. 태그 런타임 라이브러리가 빌드되면 확장의 이벤트 유형 라이브러리 모듈과 사용자 정의 설정이 모두 런타임 라이브러리에 포함됩니다. 런타임 시 Platform은 사용자 정의 설정을 라이브러리 모듈에 전달합니다.

![확장 흐름 다이어그램](../images/flow/web/extension-flow.png)

다음 다이어그램에서는 규칙 처리 흐름 내의 이벤트, 조건 및 작업 사이의 링크를 볼 수 있습니다.

![규칙 처리 흐름 다이어그램](../images/flow/web/rule-processing-flow.png)

규칙 처리 흐름에 포함되는 단계는 다음과 같습니다.

1. `settings` 및 `trigger` 메서드는 시작 시 이벤트 라이브러리 모듈에 제공됩니다.
1. 이벤트 라이브러리 모듈에서 이벤트가 발생된 것으로 판단되면 이벤트 라이브러리 모듈이 `trigger`를 호출합니다.
1. 태그는 `settings`을(를) 조건이 평가되는 규칙의 조건 라이브러리 모듈로 전달합니다.
1. 각 조건 라이브러리 모듈은 조건이 true로 평가되는지의 여부를 반환합니다.
1. 모든 조건이 통과하면 규칙의 작업이 실행됩니다.
