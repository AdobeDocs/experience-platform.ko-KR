---
keywords: Experience Platform;문제 해결;보호 기능;지침
title: 데이터 수집 보호 기능
description: 이 문서에서는 Adobe Experience Platform의 데이터 수집을 위한 보호 기능에 대한 지침을 제공합니다
source-git-commit: 3f558c9c11945cc9af51c42f7ed872101521259f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---

# 데이터 수집 보호 기능

가드레일은 데이터 및 시스템 사용, 성능 최적화, Adobe Experience Platform에서 오류 또는 예기치 않은 결과를 방지하기 위한 지침을 제공하는 임계값입니다. 보호 기능은 라이선스 권한과 관련하여 데이터 및 처리 사용량 또는 사용을 참조할 수 있습니다.

이 문서에서는 Adobe Experience Platform의 데이터 수집을 위한 보호 기능에 대한 지침을 제공합니다.

## 배치 수집 보호

다음 표에서는 [배치 수집 API](./batch-ingestion/overview.md) 또는 소스:

| 수집 유형 | 지침 | 참고 |
| --- | --- | --- |
| 배치 수집 API를 사용한 데이터 레이크 수집 | <ul><li>배치 수집 API를 사용하여 데이터 레이크에 시간당 최대 20GB의 데이터를 수집할 수 있습니다.</li><li>배치당 최대 파일 수는 1500개입니다.</li><li>최대 일괄 처리 크기는 100GB입니다.</li><li>행당 최대 속성 또는 필드 수는 10000.</li><li>사용자당 최대 분당 배치 수는 138개입니다.</li></ul> |
| 배치 소스를 사용한 데이터 레이크 수집 | <ul><li>다음과 같은 배치 수집 소스를 사용하여 데이터 레이크에 시간당 최대 200GB의 데이터를 수집할 수 있습니다 [!DNL Azure Blob], [!DNL Amazon S3], 및 [!DNL SFTP].</li><li>일괄 처리 크기는 256MB와 100GB 사이여야 합니다.</li><li>배치당 최대 파일 수는 1500개입니다.</li></ul> | 자세한 내용은 [소스 개요](../sources/home.md) 소스 카탈로그의 경우 데이터 처리에 를 사용할 수 있습니다. |
| 프로필에 일괄 수집 | <ul><li>시간당 최대 120GB의 데이터를 수집할 수 있습니다.</li><li>레코드 클래스의 최대 크기는 100KB(소프트)입니다.</li><li>ExperienceEvent 클래스의 최대 크기는 10KB(소프트)입니다.</li><li>단일 레코드의 최대 크기는 1MB입니다.</li></ul> |

## 스트리밍 수집 가드 레일

다음 표에서는 [스트리밍 수집 API](./streaming-ingestion/overview.md) 또는 스트리밍 소스:

| 수집 유형 | 지침 | 참고 |
| --- | --- | --- |
| 스트리밍 수집 | <ul><li>최대 레코드 크기는 1MB이며 권장 크기는 10KB입니다.</li><li>1분 이내에 프로필에 대한 초당 20000 요청을 처리할 수 있습니다.</li><li>15분 이내에 데이터 레이크에 대한 최대 20000 요청을 처리할 수 있습니다.</li></ul> | 더 높은 데이터 처리량이 필요한 경우 배치 수집 API를 사용합니다. |
| 스트리밍 소스 | <ul><li>최대 레코드 크기는 1MB이며 권장 크기는 10KB입니다.</li><li>스트리밍 소스는 새로운 소스 연결을 만들 때 초당 4000~5000개의 요청을 지원합니다.</li><li>Data Lake에 초당 4000~5000개의 요청을 처리할 수 있습니다.</li></ul> | 과 같은 스트리밍 소스 [!DNL Kafka], [!DNL Azure Event Hubs], 및 [!DNL Amazon Kinesis] 를 사용하지 않음 [!DNL Data Collection Core Service] (DCCS) 경로 및 처리량 제한이 다를 수 있습니다. 자세한 내용은 [소스 개요](../sources/home.md) 소스 카탈로그의 경우 데이터 처리에 를 사용할 수 있습니다. |

## 다음 단계

Experience Platform의 데이터 및 처리 가드레일에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [실시간 고객 프로필 데이터에 대한 보호 기능](../profile/guardrails.md)
* [ID 서비스 데이터에 대한 보호 기능](../identity-service/guardrails.md)