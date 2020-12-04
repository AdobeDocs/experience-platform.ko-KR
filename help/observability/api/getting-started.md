---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Observability Insights API 시작하기
topic: developer guide
description: Observability Insights API를 사용하면 다양한 Adobe Experience Platform 기능에 대한 지표 데이터를 검색할 수 있습니다. 이 문서에서는 Observability Insights API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

API를 [!DNL Observability Insights] 사용하면 다양한 Adobe Experience Platform 기능에 대한 지표 데이터를 검색할 수 있습니다. 이 문서에서는 [!DNL Observability Insights] API를 호출하기 전에 알아야 할 핵심 개념을 소개합니다.

## 샘플 API 호출 읽기

API 설명서는 요청의 서식을 지정하는 방법을 시연하기 위한 예제 API 호출을 제공합니다. [!DNL Observability Insights] 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 [Experience Platform 문제 해결 안내서에서 예제 API 호출을 읽는 방법에 대한 섹션을 참조하십시오](../../landing/troubleshooting.md).

## 필요한 헤더

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다. 의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## 다음 단계

API를 사용하여 [!DNL Observability Insights] 호출을 시작하려면 [지표 끝점 안내서로 진행하십시오](./metrics.md).