---
title: 경고 테스트 참조
description: Auditor가 Adobe Experience Platform Debugger에서 경고에 대한 테스트를 수행하는 방법을 알아봅니다.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 12%

---

# 경고 테스트 참조

이 참조는 Adobe Experience Platform Debugger의 auditor 기능이 경고 테스트를 실행하는 방법에 대한 자세한 정보를 제공합니다.

>[!NOTE]
>
>Experience Platform Debugger의 Auditor 테스트에 대한 자세한 내용은 [Auditor 기능 개요](./overview.md)를 참조하십시오.

알림은 인지해야 하는 문제를 보여주지만 점수에 영향을 주지 않습니다. 이러한 우수 사례 추천은 경우에 따라 구현에 적용되지 않을 수 있습니다.

| 테스트 | 두께 | 기준 | 권장 사항 |
| --- | --- | --- | --- |
| Advertising Cloud - 구현된 변환 태그 수정 | 0 | 올바른 변환 태그가 사용되는지 확인합니다.<br><br>**경고**: 더 이상 사용되지 않는 TubeMogul 변환 태그를 사용하면 데이터가 손실될 수 있습니다. | 변환 픽셀을 새로운 Advertising Cloud 이미지 전용 변환 태그로 업그레이드합니다. 이 작업은 [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md)을 통해 가장 쉽게 수행할 수 있습니다. |
| Advertising Cloud - 사용된 JS 태그 수정 | 0 | Advertising Cloud는 최신 JavaScript 태그를 사용해야 합니다. | Advertising Cloud JavaScript를 최신 버전으로 업그레이드하십시오. 더 이상 사용되지 않는 JavaScript 버전을 사용하면 기능이 손실될 수 있습니다. 이 작업은 [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md)을 사용하여 보다 쉽게 수행할 수 있습니다. |
| Advertising Cloud - 이미지 전용 태그 | 0 | Advertising Cloud 이미지 픽셀 형식은 다음 권장 형식 중 하나와 일치해야 합니다. <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Advertising Cloud 픽셀을 새로운 Advertising Cloud 이미지 전용 태그로 업그레이드하여 전체 Advertising Cloud 기능을 활용할 수 있습니다. 이 작업은 [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md)을 통해 가장 쉽게 수행할 수 있습니다. |
| Advertising Cloud - 세그먼트 픽셀 DSP 동기화 사용 | 0 | TubeMogul 세그먼트 픽셀에 DSP 동기화 설정이 포함되어 있는지 확인하고 픽셀에 설정을 추가하는 것이 좋습니다. DSP 동기화 설정은 쿼리 문자열 매개 변수를 사용하여 결정됩니다. 요약하려면: <ul><li>태그를 실행하는 경우:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>태그에 URL 매개 변수 `sid=`이(가) 포함되어 있습니다.</li><li>URL 매개 변수 `cs=0` 또는 `cs=1`이(가) 있는지 확인하고, 없다면 대상 일치율이 향상될 수 있도록 `cs=1`을(를) 해당 픽셀에 추가하는 것이 좋습니다.</li></ul> | DSP 동기화가 발생할 수 있도록 URL 매개 변수 `cs=1`을(를) Advertising Cloud 픽셀에 추가하여 대상 일치율을 높입니다. 이 작업은 [Advertising Cloud 태그 확장](../../destinations/catalog/advertising/adobe-advertising-cloud.md)을 통해 쉽게 수행할 수 있습니다. |
| Experience Cloud ID Service - AdobeOrg 하나만 사용 | 0 | 일반 ECID 구현에서는 단일 AdobeOrg를 사용해야 합니다. | 이 구현에 대해 여러 AdobeOrg ID가 있는지 확인합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=ko) |
| Launch - `pageBottom` 콜백 배치 | 0 | 태그가 작동하려면 `_satellite.pageBottom()` 함수가 있어야 합니다. 닫기 `</body>` 태그 바로 앞에 인라인 스크립트를 추가하여 DTM 기능이 적절히 작동하도록 합니다. 참고: 태그가 `<body>`의 마지막 태그가 되는 것이 좋습니다. `<body>` 태그 내에 있는 경우 작동할 수도 있지만, 우수 사례가 아니므로 제대로 기능하지 않거나 예기치 않거나 원치 않는 결과로 작동할 수 있습니다. | 닫기 `</body>` 태그 바로 앞에 인라인 스크립트를 추가하여 DTM 기능이 적절히 작동하도록 합니다. <br><br>[추가 정보](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - 자체 호스팅 | 0 | 태그 라이브러리가 `assets.adobedtm.com`의 Adobe Akamai 인스턴스에서 호스팅 중입니다. 자체 호스팅은 캐시 제어를 통해 웹 사이트 성능을 더욱 강력하게 제어하고 타사 스크립트 의존성을 줄이며 게시 프로세스를 더욱 강력하게 제어할 수 있기 때문에 태그를 로드하는 데 권장되는 방법입니다. 태그 라이브러리는 자체 웹 호스팅 또는 CDN을 통해 호스팅 및 관리할 수 있습니다. | 자체 호스팅으로 전환은 페이지에서 태그를 로드하는 접근 방식입니다. Akamai CDN을 통한 호스팅은 대부분의 경우 작동하지만 자체 호스팅이 페이지 성능을 향상시킵니다. <br><br>추가 정보:<ul><li>[태그 빠른 시작 안내서](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[비동기 배포](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - 비동기적으로 배포해야 함 | 0 | 최적의 성능을 위해 태그를 비동기적으로 배포해야 합니다. | 인라인 스크립트에 `async` 매개 변수를 포함시켜 태그 기능이 적절히 작동하도록 합니다. <br><br>[추가 정보](../../tags/ui/client-side/asynchronous-deployment.md) |
| 대상 - `mboxDefault`의 콘텐츠 | 0 | `at.js`을(를) 사용하는 경우 `mboxDefault`에 콘텐츠가 있어야 합니다. | 콘텐츠를 사용할 수 있는지 확인합니다. <br><br>[추가 정보](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ko) |

{style="table-layout:auto"}
