---
title: Adobe Experience Platform Debugger을 사용하여 포함 코드 테스트
description: Platform Debugger를 사용하여 웹 사이트에서 Adobe Experience Platform에 대한 다양한 포함 코드를 로컬에서 테스트하는 방법에 대해 알아봅니다.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 51%

---

# Adobe Experience Platform Debugger를 사용하여 포함 코드 테스트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Adobe Experience Platform에서 태그 라이브러리 빌드를 변경할 때 프로덕션 환경에 빌드를 배포하기 전에 이러한 변경 사항을 테스트해야 합니다. 웹 사이트에 대한 전용 스테이징 또는 개발 환경이 없는 경우 Adobe Experience Platform Debugger를 사용하여 사이트 내에서 다른 포함 코드를 로컬에서 테스트할 수 있습니다.

## 전제 조건

이 자습서에서는 태그에 대한 환경 및 포함 코드 사용에 대한 작업 이해가 필요합니다. 자세한 내용은 [환경 개요](./environments.md)를 참조하십시오.

또한 이 자습서에서는 Platform Debugger 브라우저 확장이 설치되어 있어야 합니다. Platform Debugger는 Chrome 브라우저에서 사용할 수 있습니다. 자습서를 시작하기 전에 다음 링크를 사용하여 확장을 설치합니다.

* [Chrome용 Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## 웹 사이트에서 Platform Debugger 열기

원하는 브라우저를 사용하여 웹 사이트로 이동하여 Platform Debugger 확장을 엽니다. Platform Debugger가 현재 연결되어 있는 사이트가 창 하단에 표시됩니다. 현재 사이트에서 태그가 실행 중인 경우 [!UICONTROL 요약] 탭에 나열됩니다.

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Platform Debugger가 처음에 연결되지 않은 경우 웹 사이트를 표시하는 브라우저 탭을 다시 로드한 후 다시 시도하십시오.

## 포함 코드 바꾸기

Platform Debugger가 사이트에 연결되면 왼쪽 탐색에서 **[!UICONTROL 시작]**&#x200B;을 선택합니다. 사이트에서 현재 실행 중인 라이브러리 빌드에 대한 정보(환경 및 관련 확장 포함)를 확인할 수 있습니다. 여기에서 포함 코드 관리를 위한 컨트롤을 표시하려면 **[!UICONTROL 구성]**&#x200B;을(를) 선택하십시오.

![](./images/embed-code-testing/launch-tab.png)

[!UICONTROL 페이지 포함 코드]에 현재 사이트에서 사용 중인 포함 코드가 표시됩니다. 포함 코드의 오른쪽에서 **[!UICONTROL 작업]**&#x200B;을 선택한 다음 **[!UICONTROL 바꾸기]**&#x200B;를 선택합니다.

![](./images/embed-code-testing/replace.png)

현재 코드를 바꿀 포함 코드를 제공하라는 팝업 창이 나타납니다. Platform Debugger를 사용하여 포함 코드를 바꾸더라도 사이트에 배포된 포함 코드는 변경되지 않습니다. 오히려 로컬에서 실행되는 포함 코드만 대체되므로 구현을 테스트 및 디버그할 수 있습니다.

테스트할 포함 코드를 제공된 텍스트 상자에 붙여 넣은 다음 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![](./images/embed-code-testing/paste-code.png)

**[!UICONTROL 구성]** 탭이 다시 표시되어 라이브 포함 코드가 입력한 코드로 대체되었음을 나타냅니다. 이제 웹 브라우저를 사용하여 테스트하고 있는 포함 코드가 예상대로 작동하는지 확인할 수 있습니다.

![](./images/embed-code-testing/code-replaced.png)

## 다음 단계

이 자습서에서는 Platform Debugger를 사용하여 테스트용으로 포함 코드를 로컬에서 전환하는 방법에 대해 설명합니다. 다양한 기능에 대한 자세한 내용은 [Platform Debugger 설명서](../../../debugger/home.md)를 참조하십시오.
