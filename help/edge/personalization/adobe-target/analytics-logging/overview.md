---
title: Platform Web SDK에서 A4T(Adobe Analytics for Target) 로깅
description: Experience Platform 웹 SDK를 사용하여 A4T(Adobe Analytics for Target) 데이터의 컬렉션을 제어하는 방법을 알아봅니다.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;로깅;analytics;sdk;웹 sdk
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Platform Web SDK에서 A4T(Adobe Analytics for Target) 로깅

개인화에 Adobe Target을 사용할 때 성능 측정에 사용할 시스템을 선택할 수 있습니다. 각 [Target 활동](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) Target 보고과 Adobe Analytics 보고 중에서 선택할 수 있습니다.

Analytics 보고를 사용하는 경우 Adobe Target에서 다음 내용을 Analytics에 전달해야 합니다.

* 방문자가 입력한 Adobe Target 활동
* 그들이 본 경험
* 어느 변환에 도달했는지

Adobe Experience Platform Web SDK는 A4T(Analytics for Analytics) 사용 사례에 대한 두 가지 유형의 Analytics 로깅을 지원합니다.

| 로깅 메서드 | 설명 |
| --- | --- |
| 서버 측 Analytics 로깅 | Edge Network를 통해 전송된 모든 Analytics 히트는 히트 결합 프로세스를 거치지 않고 서버 쪽의 Target 세부 사항으로 강화됩니다. |
| 클라이언트 측 분석 로깅 | Target 데이터가 클라이언트측에서 반환되므로, 를 사용하여 데이터를 수동으로 증가시키고 Analytics로 전송할 수 있습니다 [데이터 삽입 API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

로깅 방법은 구성된 페이지에 Adobe Analytics을 활성화했는지 여부에 따라 결정됩니다 [데이터 스트림](../../../fundamentals/datastreams.md):

![로깅 방법 결정 흐름](../assets/analytics-logging.png)

## 다음 단계

이 문서에서는 웹 SDK의 A4T 데이터에 대한 다양한 로깅 방법을 간략하게 소개합니다. 이러한 각 메서드에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Platform Web SDK의 A4T 데이터에 대한 서버 측 로깅](./server-side.md)
* [Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅](./client-side.md)
