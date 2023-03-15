---
title: Edge 확장 흐름
description: Adobe Experience Platform의 Edge 확장 구성 요소가 런타임 시 상호 작용하는 방법에 대해 알아봅니다.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 50%

---

# Edge 확장 흐름

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Edge 확장에서는 각 조건, 작업 및 데이터 요소 유형에 사용자가 설정을 수정하는 보기와 라이브러리 모듈이 사용자 정의 설정에 따라 작동하는 보기가 모두 포함됩니다.

다음 고급 다이어그램에서와 같이 확장의 작업 유형 보기는 Adobe Experience Platform과 통합된 애플리케이션의 iframe 내에 표시됩니다. 그런 다음 보기를 사용하여 설정을 수정하고 이 설정은 Platform 내에 저장됩니다. 태그 런타임 라이브러리가 빌드되면 확장의 작업 유형 라이브러리 모듈과 사용자 정의 설정이 모두 Edge 노드에 배포되는 런타임 라이브러리에 포함됩니다. Platform의 사용자 정의 설정은 런타임 시 라이브러리 모듈에 삽입됩니다.

![확장 흐름 다이어그램](../images/flow/edge/event-processing-flow.png)

다음 다이어그램에서는 규칙 처리 흐름 내의 이벤트, 조건 및 작업 사이의 링크를 볼 수 있습니다.

![규칙 처리 흐름 다이어그램](../images/flow/edge/rule-processing-flow.png)

규칙 처리 흐름에 포함되는 단계는 다음과 같습니다.

1. `settings` 및 `trigger` 메서드는 시작 시 이벤트 라이브러리 모듈에 제공됩니다.
1. 이벤트 라이브러리 모듈에서 이벤트가 발생된 것으로 판단되면 이벤트 라이브러리 모듈이 `trigger`를 호출합니다.
1. 플랫폼 통과 `settings` 를 사용하여 조건이 평가되는 규칙의 조건 유형 라이브러리 모듈에 추가합니다.
1. 각 조건 유형은 조건이 true로 평가되는지의 여부를 반환합니다.
1. 모든 조건이 통과하면 규칙의 작업이 실행됩니다.
