---
keywords: Experience Platform;문제 해결;보호 기능;지침;
title: 데이터 수집 보호
description: Adobe Experience Platform에서의 데이터 수집을 위한 보호 기능에 대해 알아봅니다.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 7a2463e1bb09180ae7e02674d0c0040c8c874ad5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 데이터 수집 보호

>[!IMPORTANT]
>
>일괄 처리 및 스트리밍 수집에 대한 보호는 샌드박스 수준이 아닌 조직 수준에서 계산됩니다. 즉, 샌드박스당 데이터 사용량이 전체 조직에 해당하는 총 라이선스 사용 권한에 바인딩됩니다. 또한 개발 샌드박스의 데이터 사용은 총 프로필의 10%로 제한됩니다. 라이선스 사용 권한에 대한 자세한 내용은 [데이터 관리 모범 사례 안내서](../landing/license-usage-and-guardrails/data-management-best-practices.md).

가드레일은 Adobe Experience Platform에서 데이터 및 시스템 사용, 성능 최적화 및 오류나 예기치 않은 결과의 회피를 위한 지침을 제공하는 임계값입니다. 보호 기능은 라이선스 권한과 관련하여 데이터 사용 또는 소비 및 처리를 의미할 수 있습니다.

>[!IMPORTANT]
>
>판매 주문에서 라이선스 권한을 확인하고 해당 권한을 확인하십시오. [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html) 이 보호 기능 페이지 외에 실제 사용 제한에서도 사용할 수 있습니다.

이 문서에서는 Adobe Experience Platform의 데이터 수집을 위한 보호 기능에 대한 지침을 제공합니다.

## 일괄 처리 수집 보호 기능

다음 표에는 사용 시 고려해야 할 보호 기능이 나와 있습니다. [일괄 처리 수집 API](./batch-ingestion/overview.md) 또는 소스:

| 수집 유형 | 지침 | 참고 |
| --- | --- | --- |
| 일괄 처리 수집 API를 사용한 데이터 레이크 수집 | <ul><li>일괄 처리 수집 API를 사용하여 시간당 최대 20GB의 데이터를 데이터 레이크로 수집할 수 있습니다.</li><li>배치당 최대 파일 수는 1500개입니다.</li><li>최대 배치 크기는 100GB입니다.</li><li>행당 최대 속성 또는 필드 수는 10000.</li><li>사용자당 분당 최대 배치 수는 138개입니다.</li></ul> | |
| 일괄 처리 소스를 사용한 데이터 레이크 수집 | <ul><li>다음과 같은 일괄 처리 수집 소스를 사용하여 데이터 레이크로 시간당 최대 200GB의 데이터를 수집할 수 있습니다. [!DNL Azure Blob], [!DNL Amazon S3], 및 [!DNL SFTP].</li><li>배치 크기는 256MB에서 100GB 사이여야 합니다. 압축되지 않은 데이터와 압축된 데이터 모두에 적용됩니다. 압축된 데이터가 데이터 레이크에서 압축되지 않은 경우 이러한 제한 사항이 적용됩니다.</li><li>배치당 최대 파일 수는 1500개입니다.</li><li>파일 또는 폴더의 최소 크기는 1바이트입니다. 0바이트 크기 파일 또는 폴더는 수집할 수 없습니다.</li></ul> | 읽기 [소스 개요](../sources/home.md) 소스 카탈로그의 경우 데이터 수집에 사용할 수 있습니다. |
| 프로필에 일괄 처리 수집 | <ul><li>레코드 클래스의 최대 크기는 100KB(하드)입니다.</li><li>ExperienceEvent 클래스의 최대 크기는 10KB(하드)입니다.</li></ul> | |
| 하루에 수집된 프로필 또는 ExperienceEvent 배치 수 | **하루에 수집할 수 있는 프로필 또는 ExperienceEvent 배치의 최대 수는 90개입니다.** 즉, 매일 수집된 프로필 및 ExperienceEvent 배치의 총 합은 90을 초과할 수 없습니다. 추가 배치를 수집하면 시스템 성능에 영향을 줍니다. | 이는 소프트 제한입니다. 소프트 제한을 넘어설 수 있지만 소프트 제한은 시스템 성능에 대한 권장 지침을 제공합니다. |

## 스트리밍 수집 보호 기능

읽기 [스트리밍 수집 개요](./streaming-ingestion/overview.md) 스트리밍 수집을 위한 가드레일에 대한 정보입니다.

## 스트리밍 소스 보호 기능

다음 표에서는 스트리밍 소스 사용 시 고려해야 할 가드레일에 대해 설명합니다.

| 수집 유형 | 지침 | 참고 |
| --- | --- | --- |
| 스트리밍 소스 | <ul><li>최대 레코드 크기는 1MB이며 권장 크기는 10KB입니다.</li><li>스트리밍 소스는 데이터 레이크로 수집할 때 초당 4000~5000개의 요청을 지원합니다. 이는 기존 소스 연결뿐만 아니라 새로 생성된 소스 연결 모두에 적용됩니다. **참고**: 스트리밍 데이터가 데이터 레이크로 완전히 처리되는 데 최대 30분이 걸릴 수 있습니다.</li><li>스트리밍 소스는 프로필로 데이터를 수집하거나 스트리밍 세분화를 수행할 때 초당 최대 1500개의 요청을 지원합니다.</li></ul> | 스트리밍 소스: [!DNL Kafka], [!DNL Azure Event Hubs], 및 [!DNL Amazon Kinesis] 를 사용하지 마십시오 [!DNL Data Collection Core Service] (DCCS) 경로 및 은 서로 다른 처리량 제한을 가질 수 있습니다. 다음을 참조하십시오. [소스 개요](../sources/home.md) 소스 카탈로그의 경우 데이터 수집에 사용할 수 있습니다. |

## 다음 단계

Real-Time CDP 제품 설명 문서의 기타 Experience Platform 서비스 보호, 종단 간 지연 정보 및 라이선스 정보에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Real-Time CDP 보호 기능](/help/rtcdp/guardrails/overview.md)
* [엔드 투 엔드 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 다양한 Experience Platform 서비스용.
* [Real-time Customer Data Platform (B2C 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
