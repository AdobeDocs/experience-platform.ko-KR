---
keywords: Experience Platform;홈;인기 항목;날짜 범위
solution: Experience Platform
title: Observability Insights API 시작하기
description: Observability Insights API 를 통해 다양한 Adobe Experience Platform 기능에 대한 지표 데이터를 검색할 수 있습니다. 이 문서에서는 Observability Insights API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 시작하기 [!DNL Observability Insights] API

다음 [!DNL Observability Insights] API를 사용하면 다양한 Adobe Experience Platform 기능에 대한 지표 데이터를 검색할 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다. [!DNL Observability Insights] API.

## 샘플 API 호출 읽기

다음 [!DNL Observability Insights] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 의 예제 API 호출을 읽는 방법에 대한 섹션을 참조하십시오. [Experience Platform 문제 해결 안내서](../../landing/troubleshooting.md).

## 필수 헤더

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다. 의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## 다음 단계

을 사용하여 호출을 시작하려면 [!DNL Observability Insights] API, 다음 단계로 진행 [metrics endpoint 안내서](./metrics.md).
