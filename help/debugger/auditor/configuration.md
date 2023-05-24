---
title: 구성 테스트 참조
description: Auditor 기능이 Adobe Experience Platform Debugger에서 구성을 테스트하는 방법을 알아봅니다.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 797d4f305b4a6884ada4e0619beadff6a45ab42d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 66%

---

# 구성 테스트 참조

이 참조는 Adobe Experience Platform Debugger의 auditor 기능이 구성 테스트를 실행하는 방법에 대한 자세한 정보를 제공합니다.

>[!NOTE]
>
>Platform Debugger의 Auditor 테스트에 대한 자세한 내용은 [auditor 기능 개요](./overview.md).

구성 테스트는 구현에서 특정 설정, 값 또는 잠재적인 충돌을 검사합니다. Platform Auditor는 다른 규칙에 대해 태그를 평가하고 우수 사례를 권장합니다.

| 테스트 | 가중치 | 기준 | 권장 사항 |
| --- | --- | --- | --- |
| Advertising Cloud - 변환 이름은 영숫자만 사용 | 3 | 다음 `ev_conversion_property_name` 매개 변수에는 다음을 제외한 숫자 및 십진수 값만 포함되어야 합니다. `ev_transid` 매개 변수 - 텍스트 또는 숫자 값을 포함할 수 있습니다. `everesttech.net`_로 시작하는 URL 매개 변수가 포함된 `ev_` 픽셀을 찾습니다. | 거래 속성 매개 변수에는 숫자 및 십진수 값만 포함되어야 합니다.<br><br>경고: 다른 모든 값 유형은 데이터 손실을 초래할 수 있습니다. |
| Advertising Cloud - 변환 이름은 URL 안전 문자를 사용 | 3 | 변환 속성 이름에 앰퍼샌드 또는 물음표를 포함해서는 안 됩니다. | 거래 속성 매개 변수에 인코딩되지 않은 앰퍼샌드 또는 물음표가 포함되어 있지 않아야 합니다. 이렇게 하면 URL 형식이 손상됩니다.<br><br>경고: 인코딩되지 않은 앰퍼샌드 또는 물음표가 포함된 속성 매개 변수입니다(예:  `ev_formComplete?=1` 또는  `ev_formComplete&Submit=1`)으로 설정하면 데이터가 손실될 수 있습니다. |
| Advertising Cloud - 올바르게 구현된 거래 ID | 1 | 속성 이름  `ev_transid=` 비워둘 수 없습니다. | 속성 이름  `ev_transid=` 값을 비워둘 수 없습니다. 값 없이 비워 두면 거래 데이터가 손실될 수 있습니다. 값 할당 대상 `ev_transid=` 또는 픽셀에서 매개 변수를 제거합니다. |
| Analytics - DOM에서 인스턴스화 | 5 | Adobe Analytics 코드가 설치되지 않았거나 실행되지 않았습니다. 웹 페이지에 Analytics 코드가 없으면 0을 반환합니다. | Analytics 태그가 페이지에 구현되어 있고 후속 스크립트 활동에서 차단되지 않았는지 확인합니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics - 한 번 인스턴스화 | 5 | Adobe Analytics 코드가 페이지에서 두 번 이상 검색되었습니다. 웹 페이지에 A-Analytics 코드가 없으면 0을 반환합니다. | 페이지에 Analytics 태그가 하나만 있어야 합니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics - 최신 버전 | 3 | 페이지에서 최신 버전의 Analytics 코드 라이브러리를 실행하고 있지 않습니다. 향상된 성능을 활용하고 최신 기능을 제공하기 위해 Experience Cloud 기술을 지원하는 코드 라이브러리가 지속적으로 업데이트 및 변경되고 있습니다. 웹 페이지에 Analytics 코드가 없으면 0을 반환합니다. | 최신 버전의 Analytics 라이브러리를 설치합니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html) |
| Launch - DOM Ready 이후 타사 태그가 비동기적으로 로드 | 3 | 양호한 사용자 경험과 정확한 데이터 수집 간의 균형을 맞추기 위해 서드파티 태그를 DOM Ready에서 트리거해야 합니다. 이렇게 하면 사이트 기능에 영향을 주지 않고 이러한 추적 스크립트가 실행됩니다. | DOM Ready에서 시작할 타사 픽셀을 실행하는 모든 규칙을 조정하여 이 문제를 해결합니다.<br><br>[추가 정보](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID Service - 최신 버전 | 2 | 페이지에서 방문자 ID 서비스 코드 라이브러리의 최신 버전인 visitorAPI.js를 실행하고 있지 않습니다. 향상된 성능을 활용하고 최신 기능을 제공하기 위해 Experience Cloud 기술을 지원하는 코드 라이브러리가 지속적으로 업데이트 및 변경되고 있습니다. | 최신 버전의 방문자 ID 서비스 라이브러리를 설치합니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch - 최신 버전 | 2 | 이러한 페이지에서 최신 버전의 태그 코드 라이브러리(Turbine)를 실행하고 있지 않습니다. 향상된 성능을 활용하고 최신 기능을 제공하기 위해 Experience Cloud 기술을 지원하는 코드 라이브러리가 지속적으로 업데이트 및 변경되고 있습니다. | 태그 라이브러리를 다시 빌드하고 게시합니다.<br><br>[추가 정보](../../tags/quick-start/quick-start.md) |
| Target - 최신 버전 | 2 | 페이지에서 최신 버전의 Target 코드 라이브러리를 실행하고 있지 않습니다. 향상된 성능을 활용하고 최신 기능을 제공하기 위해 Experience Cloud 기술을 지원하는 코드 라이브러리가 지속적으로 업데이트 및 변경되고 있습니다. | 최신 버전의 Target 라이브러리를 설치합니다.<br><br>[추가 정보](https://developer.adobe.com/target/implement/client-side/) |
| Target - mboxDefault가 mboxCreate보다 우선함 | 5 | mboxCreate의 적절한 사용은 다음과 유사합니다.<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | 다음을 포함해야 합니다.  `<div class="mboxDefault"></div>` 태그를 지정한 후 mboxCreate(). at.js는 사용자를 위해 추가하지 않습니다.<br><br>[추가 정보](https://developer.adobe.com/target/implement/client-side/) |
| Target - 유효한 DOCTYPE | 5 | 잘못된 DOCTYPE이 검색되었습니다. 이 시나리오에서는 mbox가 실행되지 않습니다.  at.js의 경우 DOCTYPE이 표준 모드여야 합니다. 그렇지 않으면 Target이 작동하지 않습니다. | 페이지에서 DOCTYPE을 업데이트합니다.<br><br>[추가 정보](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
