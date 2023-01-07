---
title: Adobe Experience Platform의 데이터 암호화
description: 데이터를 전송 및 Adobe Experience Platform에서 안전하게 암호화하는 방법을 알아봅니다.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# Adobe Experience Platform의 데이터 암호화

Adobe Experience Platform은 엔터프라이즈 솔루션 전반에서 고객 경험 데이터를 중앙 집중화하고 표준화하는 강력하고 확장 가능한 시스템입니다. Platform에서 활용하는 모든 데이터는 전송 중에 암호화되어 있으며 나머지는 데이터 보안을 유지합니다. 이 문서에서는 Platform의 암호화 프로세스를 높은 수준에서 설명합니다.

다음 프로세스 흐름 다이어그램은 데이터를 수집, 암호화 및 유지하는 방법을 보여줍니다. [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## 전송 중인 데이터 {#in-transit}

플랫폼과 외부 구성 요소 간에 전송 중인 모든 데이터는 HTTPS를 사용하여 안전하고 암호화된 연결을 통해 수행됩니다 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

일반적으로 데이터는 다음 세 가지 방법으로 Platform으로 가져옵니다.

* [데이터 수집](../../collection/home.md) 웹 사이트 및 모바일 애플리케이션에서 스테이징과 수집 준비를 위해 Platform Edge Network에 데이터를 전송할 수 있습니다.
* [소스 커넥터](../../sources/home.md) Adobe Experience Cloud 애플리케이션 및 기타 엔터프라이즈 데이터 소스에서 Platform으로 직접 데이터를 스트리밍할 수 있습니다.
* 비Adobe ETL(추출, 변환, 로드) 도구는 데이터를 [배치 수집 API](../../ingestion/batch-ingestion/overview.md) 소비.

데이터를 시스템에 가져온 후 [안전하게 암호화](#at-rest)과 같은 방법으로 플랫폼 서비스에서 보호하고 시스템에서 내보낼 수 있습니다.

* [대상](../../destinations/home.md) 데이터를 Adobe 응용 프로그램 및 파트너 응용 프로그램에 활성화할 수 있습니다.
* 과 같은 기본 플랫폼 애플리케이션 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko-KR) 도 데이터를 사용할 수 있습니다.

## 데이터 중단 {#at-rest}

Platform에서 수집 및 사용하는 데이터는 원본이나 파일 형식에 관계없이 시스템에서 관리하는 모든 데이터를 포함하는 매우 세분화된 데이터 저장소인 data lake에 저장됩니다. 데이터 레이크에 지속되는 모든 데이터는 격리된 상태에서 암호화, 저장 및 관리됩니다 [[!DNL Microsoft Azure Data Lake] 스토리지](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 조직에 고유한 인스턴스.

Azure Data Lake Storage에서 사용 중인 데이터가 암호화되는 방법에 대한 자세한 내용은 [공식 Azure 설명서](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 다음 단계

이 문서에서는 Platform에서 데이터가 암호화되는 방법에 대한 높은 수준의 개요를 제공합니다. Platform의 보안 절차에 대한 자세한 내용은 [거버넌스, 개인 정보 및 보안](./overview.md) Experience League 시 또는 [플랫폼 보안 백서](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
