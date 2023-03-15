---
title: 감사 쿼리 API 안내서
description: 감사 쿼리는 개발자가 Adobe Experience Platform에서 누가 어떤 작업을 수행했는지 확인할 수 있는 RESTful API입니다.
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---

# [!DNL Audit Query] API 안내서

다음 [!DNL Audit Query] API는 다양한 Adobe Experience Platform 기능에 대한 이벤트 데이터를 프로그래밍 방식으로 검색하고 모니터링할 수 있는 끝점을 제공합니다. 엔드포인트는 아래에 요약되어 있습니다. 다음을 방문하십시오. [시작 안내서](./getting-started.md) 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 제공합니다.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [[!DNL Audit Query] API Swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## 이벤트

감사 이벤트는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 Adobe Experience Platform의 다양한 기능에 대한 작업 유형과 관련된 추가 속성을 포함하여 플랫폼의 사용자 작업에 대한 통찰력을 제공합니다. API를 사용하여 지표를 검색하는 방법에 대한 자세한 내용은 [events endpoint 안내서](./events.md).

## 내보내기

감사 내보내기를 사용하면 페이로드에서 검색할 이벤트를 지정하여 이벤트 데이터를 검색할 수 있습니다. API를 사용하여 지표를 검색하는 방법에 대한 자세한 내용은 [끝점 내보내기 안내서](./export.md).
