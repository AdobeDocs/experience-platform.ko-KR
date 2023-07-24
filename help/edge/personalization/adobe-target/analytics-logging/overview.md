---
title: Platform Web SDK에서 A4T(Adobe Analytics for Target) 로깅
description: Adobe Analytics Experience Platform Web SDK를 사용하여 Target (A4T) 데이터 수집을 제어하는 방법에 대해 알아봅니다.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;로깅;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Platform Web SDK에서 A4T(Adobe Analytics for Target) 로깅

개인화에 Adobe Target을 사용할 때 성과 측정에 사용할 시스템을 선택할 수 있습니다. 각 [Target 활동](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) Target 보고와 Adobe Analytics 보고 중에서 선택할 수 있습니다.

Analytics 보고를 사용하는 경우 Adobe Target은 다음을 Analytics에 전달해야 합니다.

* 방문자가 입력한 Adobe Target 활동
* 어떤 경험을 보았습니까
* 전환에 도달함

Adobe Experience Platform Web SDK는 Analytics for Target(A4T) 사용 사례의 두 가지 유형의 Analytics 로깅을 지원합니다.

| 로깅 방법 | 설명 |
| --- | --- |
| 서버측 분석 로깅 | Edge Network를 통해 전송되는 모든 Analytics 히트는 히트 결합 프로세스를 거치지 않고도 서버측에서 Target 세부 사항으로 보강됩니다. |
| 클라이언트 측 분석 로깅 | Target 데이터는 클라이언트측에서 반환되므로, 를 사용하여 데이터를 수동으로 늘리고 Analytics에 보낼 수 있습니다. [데이터 삽입 API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

로깅 방법은 구성된 페이지에서 Adobe Analytics을 활성화했는지 여부에 따라 결정됩니다 [데이터스트림](../../../../datastreams/overview.md):

![로깅 방법 결정 흐름](../assets/analytics-logging.png)

## 다음 단계

이 문서에서는 Web SDK의 A4T 데이터에 대한 다양한 로깅 방법에 대해 간략하게 소개합니다. 이러한 각 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Platform Web SDK의 A4T 데이터에 대한 서버측 로깅](./server-side.md)
* [Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅](./client-side.md)
