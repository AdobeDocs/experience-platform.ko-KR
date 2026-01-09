---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;쿼리
title: Adobe Experience Platform 쿼리 서비스 시작
description: Adobe Experience Platform 쿼리 서비스를 완전히 활용하는 데 필요한 단계에 대한 분류
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Adobe Experience Platform [!DNL Query Service] 시작 {#getting-started}

Adobe Experience Platform 쿼리 서비스를 사용하여 수집된 데이터 세트에 대해 SQL 쿼리를 실행하고, 여러 소스에서 데이터를 결합하고, 분석, 머신 러닝 워크플로우 또는 실시간 고객 프로필에 대해 파생된 데이터 세트를 생성할 수 있습니다. 데이터를 수집한 후 대화형 분석 및 공동 작업을 위해 UI를 통해 또는 자동화된 프로그래밍 방식 쿼리 실행을 위해 API를 통해 쿼리 서비스에 액세스합니다.

## 전제 조건 {#prerequisites}

데이터 쿼리를 시작하기 전에 다음을 확인하십시오.

- **필수 권한**: 사용자 계정이 Experience Platform의 쿼리 서비스에 액세스할 수 있습니다. UI에서 서비스를 사용할 수 없는 경우 [권한 설명서](../../access-control/home.md#permissions)를 검토하고 시스템 관리자에게 문의하십시오.
- **데이터 수집**: Experience Platform에 데이터가 수집되었습니다.

데이터를 수집해야 하는 경우 [데이터 수집 튜토리얼 비디오](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)에서 데이터 세트 생성, 스키마 매핑, 수집 및 유효성 검사에 대한 개요를 검토하십시오. 자세한 정보와 다른 학습 리소스에 대한 링크는 [수집 개요 설명서](../../ingestion/home.md)를 참조하십시오.

## 빠른 시작 경로

데이터를 Experience Platform에 수집하면 Experience Platform의 [!DNL Query Editor] 또는 쿼리 서비스 API를 사용하여 쿼리 서비스 작업을 시작할 수 있습니다.

### [!DNL Query Editor]

분석, 데이터 탐색 및 공동 쿼리 개발에 [!DNL Query Editor]을(를) 사용합니다. UI 기능에 대한 개요는 [쿼리 서비스 UI 설명서](../ui/overview.md)를 참조하십시오. UI에서 쿼리를 작성하고 실행하는 방법에 대해 알아보려면 [[!DNL Query Editor user guide]](../ui/user-guide.md)을(를) 읽어 보십시오.

### 쿼리 서비스 API

자동화된 워크플로우, 쿼리 템플릿 관리 및 프로그래밍 방식 통합에 쿼리 서비스 API를 사용합니다. 쿼리 서비스 API 사용에 대한 자세한 지침은 [쿼리 서비스 개발자 안내서](../api/getting-started.md)를 참조하세요.

## 다음 단계

이 문서에서는 Experience Platform의 [!DNL Query Service] 기능을 사용하는 데 필요한 필수 구성 요소에 대해 설명합니다. 쿼리 서비스 기능을 빠르게 시작하려면 다음 문서를 읽는 것이 좋습니다.

- [쿼리 실행에 대한 일반 지침](../best-practices/writing-queries.md)
- [쿼리 서비스의 SQL 구문](../sql/syntax.md)
- [SQL을 사용하여 파생 데이터 세트 만들기](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

또는 Query Service가 Experience Platform에서 데이터 처리에 어떻게 도움이 되는지 자세히 알아보려면 [중단된 찾아보기 사용 사례 프레젠테이션](../use-cases/abandoned-browse.md#video-example)을 시청하십시오.

다음 리소스는 [!DNL Query Service]에 대한 이해를 높이는 데 유용합니다.

- [[!DNL Query Service] UI 개요](../ui/overview.md)
- [[!DNL Query Service] 자격 증명](../ui/credentials.md)
- [클라이언트 연결 개요](../clients/overview.md)
