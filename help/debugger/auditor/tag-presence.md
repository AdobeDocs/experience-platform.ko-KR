---
title: 태그 유무 테스트 참조
description: Adobe Experience Platform Debugger에서 auditor 기능이 태그 유무를 테스트하는 방법을 알아봅니다.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 34%

---

# 태그 유무 테스트 참조

이 참조는 Adobe Experience Platform Debugger의 auditor 기능이 태그 유무를 테스트하는 방법에 대한 자세한 정보를 제공합니다.

>[!NOTE]
>
>Platform Debugger의 auditor 테스트에 대한 자세한 내용은 [auditor 기능 개요](./overview.md).

태그 유무 테스트는 페이지에 특정 태그가 있는지 여부, 페이지 코드가 올바른 위치에 있는지 여부를 평가합니다.

| 테스트 | 가중치 | 기준 | 권장 사항 |
| --- | --- | --- | --- |
| Advertising Cloud - 코드 유무 | 5 | Advertising Cloud 태그는 DOM에서 사용할 수 없습니다. | 를 사용하여 Advertising Cloud 태그 구현 [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - 구현된 세그먼트 픽셀 | 5개 | Advertising Cloud 세그먼트 픽셀을 새로운 Advertising Cloud 이미지 전용 태그로 업그레이드합니다. 더 이상 사용되지 않는 AMO 세그먼트 태그를 사용하면 데이터가 손실될 수 있습니다. | 를 사용하여 Advertising Cloud 세그먼트 픽셀 구현 [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - DOM에서 로드됨 | 5개 | Adobe Analytics 태그가 검색되지 않았습니다. | 최신 버전의 Analytics를 설치합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ko-KR) |
| Launch - 라이브러리가 로드됨 | 5개 | A `global _satellite` 개체를 DOM에서 찾을 수 없습니다. 즉, 태그 라이브러리가 설치되지 않았거나 실행되지 않았습니다. | 태그 라이브러리가 페이지에 구현되어 있고 후속 스크립트 활동에서 차단되지 않았는지 확인합니다. |
| Launch - 여러 개의 포함 스크립트가 없음 | 5개 | 프로덕션 사이트는 페이지당 하나의 포함 코드만 로드해야 합니다. | 프로덕션 라이브러리만 페이지에 로드되고 있는지 확인합니다. |
| Launch - `pageBottom` 콜백이 존재함 `<body>` | 5개 | 필수 `_satellite.pageBottom()` 콜백을 찾을 수 없습니다. `<body>` 섹션에 있는 마지막 항목이 될 필요가 없습니다. 이 테스트가 `pageBottom` 호출은 페이지에서 전혀 없거나 `<head>` 태그(또는 기타 예기치 않은 위치)를 지정합니다. 다음 경우에만 전달됩니다 `pageBottom` 내 어딘가에 있음 `<body>` 태그에 가깝게 포함했습니다. | 닫기 바로 앞에 인라인 스크립트를 추가합니다 `</body>` 태그 내에 이미지 요청을 완전히 채우는 데 사용할 수 있습니다.<br><br>[추가 정보](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` 콜백은 비동기적으로 배포할 때 존재하지 않아야 합니다. | 5개 | 다음 `_satellite.pageBottom()` 콜백이 페이지에서 발견되었으며, 이는 태그가 비동기적으로 배포된 경우에는 해당되지 않습니다. | 제거 `_satellite.pageBottom()` 적절한 태그 기능을 활성화하는 스크립트. <br><br>[추가 정보](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID Service - 코드 유무 | 5개 | Experience Cloud ID Service 코드를 찾을 수 없습니다. ECID(Experience Cloud ID)를 사용하는 것은 Experience Cloud 솔루션의 가치를 극대화하기 위해 매우 권장되며 Experience Cloud 솔루션 전반에서 매우 중요합니다. | 최신 버전의 ECID를 설치합니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID Service - 쿠키 유무 | 5개 | 다음 `AMCV_` 쿠키를 찾을 수 없습니다. `VisitorAPI.js`   코드에서 방문자 개체를 인스턴스화해야 합니다. | 태그 구현인 경우 AdobeOrg ID가 ECID 도구에 제대로 입력되었는지 확인합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=ko-KR) |
| Experience Cloud ID Service - MID 값 유무 | 5개 | MID 값이 `AMCV_` 쿠키 . | 다시 테스트하여 ECID API 지연을 확인합니다. 상태가 지속되면 Adobe 고객 지원 센터에 문의하십시오. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - 코드 여부 | 5개 | Adobe Target은 DOM에서 정의해야 합니다. | 최신 버전의 Target (at.js)을 설치합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - 에 로드된 라이브러리 `<head>` | 4 | Target 라이브러리는 `<head>` 태그에 가깝게 포함했습니다. | Target 라이브러리가 `<head>` 태그에 가깝게 포함했습니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
