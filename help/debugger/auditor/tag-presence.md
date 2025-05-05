---
title: 태그 유무 테스트 참조
description: Auditor가 Adobe Experience Platform Debugger에서 태그 상태에 대한 테스트를 수행하는 방법을 알아봅니다.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 17%

---

# 태그 존재 테스트 참조

이 참조는 Adobe Experience Platform Debugger의 Auditor 기능이 어떻게 태그의 존재를 테스트하는지에 대한 자세한 정보를 제공합니다.

>[!NOTE]
>
>Experience Platform Debugger의 Auditor 테스트에 대한 자세한 내용은 [Auditor 기능 개요](./overview.md)를 참조하십시오.

태그 존재 테스트는 페이지에 특정 태그가 있는지 여부와 페이지 코드가 올바른 위치에 있는지 여부를 평가합니다.

| 테스트 | 두께 | 기준 | 권장 사항 |
| --- | --- | --- | --- |
| Advertising Cloud - 코드 유무 | 5 | Advertising Cloud 태그는 DOM에서 사용할 수 없습니다. | [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md)을 사용하여 Advertising Cloud 태그를 구현합니다. |
| Advertising Cloud - 구현된 세그먼트 픽셀 | 5 | Advertising Cloud 세그먼트 픽셀을 새로운 Advertising Cloud 이미지 전용 태그로 업그레이드합니다. 더 이상 사용되지 않는 AMO 세그먼트 태그를 사용하면 데이터가 손실될 수 있습니다. | [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md)을 사용하여 Advertising Cloud 세그먼트 픽셀을 구현합니다. |
| Analytics - DOM에서 로드됨 | 5 | Adobe Analytics 태그가 검색되지 않았습니다. | 최신 버전의 Analytics를 설치합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ko) |
| Launch - 라이브러리가 로드됨 | 5 | DOM에서 `global _satellite` 개체를 찾을 수 없습니다. 즉, 태그 라이브러리가 설치되지 않았거나 실행되지 않습니다. | 태그 라이브러리가 페이지에 구현되어 있고 후속 스크립트 활동에서 차단되지 않았는지 확인합니다. |
| Launch - 여러 개의 포함 스크립트가 없음 | 5 | 프로덕션 사이트는 페이지당 하나의 포함 코드만 로드해야 합니다. | 프로덕션 라이브러리만 페이지에 로드되고 있는지 확인합니다. |
| Launch - `pageBottom` 콜백이 `<body>`에 있습니다. | 5 | 필요한 `_satellite.pageBottom()` 콜백을 페이지의 `<body>` 내에서 찾을 수 없습니다. 페이지에서 `pageBottom` 호출을 전혀 찾을 수 없거나 `<head>` 태그(또는 기타 예기치 않은 위치)에 있는 경우 이 테스트가 실패합니다. `pageBottom`이(가) `<body>` 태그 내 어딘가에 있는 경우에만 전달됩니다. | 닫기 `</body>` 태그 바로 앞에 인라인 스크립트를 추가하여 태그 기능이 적절히 작동하도록 합니다.<br><br>[추가 정보](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` 콜백은 비동기적으로 배포할 때 존재하지 않아야 합니다. | 5 | 페이지에서 `_satellite.pageBottom()` 콜백이 발견되었으며, 태그가 비동기적으로 배포된 경우에는 해당되지 않습니다. | 올바른 태그 기능을 사용하려면 `_satellite.pageBottom()` 스크립트를 제거하십시오. <br><br>[추가 정보](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID Service - 코드 유무 | 5 | Experience Cloud ID Service 코드를 찾을 수 없습니다. ECID(Experience Cloud ID)를 사용하는 것은 Experience Cloud 솔루션의 가치를 극대화하기 위해 매우 권장되며 Experience Cloud 솔루션 전반에서 ID 관리에 중요합니다. | 최신 버전의 ECID를 설치합니다.<br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ko-KR) |
| Experience Cloud ID Service - 쿠키 유무 | 5 | `AMCV_` 쿠키를 찾을 수 없습니다. `VisitorAPI.js` 코드에서 방문자 개체를 인스턴스화해야 합니다. | 태그 구현인 경우 AdobeOrg ID가 ECID 도구에 제대로 입력되었는지 확인합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=ko) |
| Experience Cloud ID Service - MID 값 유무 | 5 | `AMCV_` 쿠키에 MID 값이 없습니다. | 다시 테스트하여 ECID API 지연을 확인합니다. 상태가 지속되면 Adobe 고객 지원 센터에 문의하십시오. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=ko) |
| Target - 코드 유무 | 5 | Adobe Target은 DOM에서 정의되어야 합니다. | 최신 버전의 Target(at.js)을 설치합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ko) |
| 대상 - `<head>`에 로드된 라이브러리 | 4 | Target 라이브러리는 `<head>` 태그에 로드되어야 합니다. | Target 라이브러리가 `<head>` 태그에 로드되었는지 확인하십시오. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ko) |

{style="table-layout:auto"}
