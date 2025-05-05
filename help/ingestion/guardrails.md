---
keywords: Experience Platform;문제 해결;보호;지침;
title: 데이터 수집 보호
description: Adobe Experience Platform에서의 데이터 수집을 위한 보호 기능에 대해 알아봅니다.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: a862e532382472eadf29aee2568c550b1a71211a
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# 데이터 수집 보호

>[!IMPORTANT]
>
>일괄 처리 및 스트리밍 수집에 대한 보호는 일반적으로 샌드박스 수준이 아닌 조직 수준에서 계산됩니다. 즉, 샌드박스당 데이터 사용량이 전체 조직에 해당하는 총 라이선스 사용 권한에 바인딩됩니다. 또한 개발 샌드박스의 데이터 사용은 총 프로필의 10%로 제한됩니다. 라이선스 사용 권한에 대한 자세한 내용은 [데이터 관리 모범 사례 가이드](../landing/license-usage-and-guardrails/data-management-best-practices.md)를 참조하세요.

가드레일은 Adobe Experience Platform에서 데이터 및 시스템 사용, 성능 최적화 및 오류나 예기치 않은 결과의 회피를 위한 지침을 제공하는 임계값입니다. 보호 기능은 라이선스 권한과 관련하여 데이터 사용 또는 소비 및 처리를 의미할 수 있습니다.

>[!IMPORTANT]
>
>이 보호 기능 페이지 외에 실제 사용 제한에 대해 판매 주문에서 라이선스 자격 및 해당 [제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions.html)을(를) 확인하십시오.

이 문서에서는 Adobe Experience Platform의 데이터 수집을 위한 보호 기능에 대한 지침을 제공합니다.

## 일괄 처리 수집 보호 기능

다음 표에서는 [일괄 처리 수집 API](./batch-ingestion/overview.md) 또는 소스를 사용할 때 고려해야 할 경고에 대해 설명합니다.

| 수집 유형 | 가이드라인 | 참고 |
| --- | --- | --- |
| 일괄 처리 수집 API를 사용한 데이터 레이크 수집 | <ul><li>일괄 처리 수집 API를 사용하여 시간당 최대 20GB의 데이터를 데이터 레이크로 수집할 수 있습니다.</li><li>배치당 최대 파일 수는 1500개입니다.</li><li>최대 배치 크기는 100GB입니다.</li><li>행당 최대 속성 또는 필드 수는 10000.</li><li>사용자당 분당 최대 배치 수는 2000개입니다.</li></ul> | |
| 일괄 처리 소스를 사용한 데이터 레이크 수집 | <ul><li>[!DNL Azure Blob], [!DNL Amazon S3] 및 [!DNL SFTP]과(와) 같은 일괄 처리 수집 소스를 사용하여 시간당 최대 200GB의 데이터를 데이터 레이크로 수집할 수 있습니다.</li><li>배치 크기는 256MB에서 100GB 사이여야 합니다. 압축되지 않은 데이터와 압축된 데이터 모두에 적용됩니다. 압축된 데이터가 데이터 레이크에서 압축되지 않은 경우 이러한 제한 사항이 적용됩니다.</li><li>배치당 최대 파일 수는 1500개입니다.</li><li>파일 또는 폴더의 최소 크기는 1바이트입니다. 0바이트 크기 파일 또는 폴더는 수집할 수 없습니다.</li></ul> | 데이터 수집에 사용할 수 있는 소스 카탈로그의 경우 [소스 개요](../sources/home.md)를 읽어 보십시오. |
| 프로필에 일괄 처리 수집 | <ul><li>레코드 클래스의 최대 크기는 100KB(하드)입니다.</li><li>ExperienceEvent 클래스의 최대 크기는 10KB(하드)입니다.</li></ul> | |
| 하루에 수집된 프로필 또는 ExperienceEvent 배치 수 | **하루에 수집되는 프로필 또는 ExperienceEvent 일괄 처리의 최대 수는 샌드박스당 90개입니다.** 이는 매일 수집된 프로필 및 ExperienceEvent 배치의 합계가 90개를 초과할 수 없음을 의미합니다. 추가 배치를 수집하면 시스템 성능에 영향을 줍니다. | 이는 소프트 제한입니다. 소프트 제한을 넘어설 수 있지만 소프트 제한은 시스템 성능에 대한 권장 지침을 제공합니다. 또한 이 가드레일은 조직 단위가 아닌 **샌드박스 단위** 단위로 이루어집니다. |
| 암호화된 데이터 수집 | 단일 암호화 파일의 최대 지원 크기는 1GB입니다. 예를 들어 단일 데이터 흐름 실행에서 2GB 이상의 데이터를 수집할 수 있지만 데이터 흐름 실행의 개별 파일이 1GB를 초과할 수는 없습니다. | 암호화된 데이터를 수집하는 과정은 일반 데이터 수집보다 시간이 더 오래 걸릴 수 있다. 자세한 내용은 [암호화된 데이터 수집 API 안내서](../sources/tutorials/api/encrypt-data.md)를 참조하십시오. |
| 일괄 처리 수집 업데이트 | 업데이트 일괄 처리 수집은 일반 일괄 처리보다 최대 10배 느릴 수 있으므로, 효율적인 런타임과 샌드박스에서 다른 일괄 처리가 처리되지 않도록 **업데이트 일괄 처리를 2백만 개 기록 미만으로 유지**&#x200B;해야 합니다. | 200만 개의 레코드를 초과하는 일괄 처리를 수집할 수 있지만 작은 샌드박스의 한계로 인해 수집 시간이 상당히 길어집니다. |

{style="table-layout:auto"}

## 스트리밍 수집 보호 기능

스트리밍 수집을 위한 보호 기능에 대한 자세한 내용은 [스트리밍 수집 개요](./streaming-ingestion/overview.md)를 참조하십시오.

## 스트리밍 소스 보호 기능

다음 표에서는 스트리밍 소스 사용 시 고려해야 할 가드레일에 대해 설명합니다.

| 수집 유형 | 가이드라인 | 참고 |
| --- | --- | --- |
| 스트리밍 소스 | <ul><li>최대 레코드 크기는 1MB이며 권장 크기는 10KB입니다.</li><li>스트리밍 소스는 데이터 레이크로 수집할 때 초당 4000~5000개의 요청을 지원합니다. 이는 기존 소스 연결뿐만 아니라 새로 생성된 소스 연결 모두에 적용됩니다. **참고**: 스트리밍 데이터가 데이터 레이크로 완전히 처리되려면 최대 30분이 걸릴 수 있습니다.</li><li>스트리밍 소스는 프로필로 데이터를 수집하거나 스트리밍 세분화를 수행할 때 초당 최대 1500개의 요청을 지원합니다.</li></ul> | [!DNL Kafka], [!DNL Azure Event Hubs] 및 [!DNL Amazon Kinesis]과(와) 같은 스트리밍 원본은 [!DNL Data Collection Core Service]&#x200B;(DCCS) 경로를 사용하지 않으며 다른 처리량 제한을 가질 수 있습니다. 데이터 수집에 사용할 수 있는 소스 카탈로그는 [소스 개요](../sources/home.md)를 참조하십시오. |

{style="table-layout:auto"}

## 다음 단계

Real-Time CDP 제품 설명 문서의 기타 Experience Platform 서비스 보호, 종단 간 지연 정보 및 라이선스 정보에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Real-Time CDP 보호 기능](/help/rtcdp/guardrails/overview.md)
* 다양한 Experience Platform 서비스에 대한 [전체 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=ko#end-to-end-latency-diagrams).
* [Real-Time Customer Data Platform(B2C 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform(B2P - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform(B2B - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
