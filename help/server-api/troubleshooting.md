---
title: 문제 해결
description: Adobe Experience Platform Edge Network Server API를 사용할 때 오류를 해결하는 방법을 알아봅니다
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: 에지 네트워크;게이트웨이;api;문제 해결;오류;그리폰
exl-id: f0223fca-30ec-4229-93a5-3faa6cef5482
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---

# 문제 해결

Adobe Experience Platform Edge Network Server API를 사용하면 이벤트가 Edge Network 데이터 수집 파이프라인을 통해 처리되므로 서비스에서 디버그 정보를 캡처할 수 있습니다.

에서 사용하는 것과 동일한 메커니즘 [Experience Platform 디버거](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) api 기반 구현을 디버깅할 수 있습니다.

사용 [프로젝트 그리폰](https://aep-sdks.gitbook.io/docs/beta/project-griffon)를 설정하는 경우 Edge Network 요청에서 추가로 사용하여 이벤트를 추적할 수 있는 디버깅 세션 ID를 만들 수 있습니다.
