---
title: Adobe Experience Platform의 데이터 암호화
description: Adobe Experience Platform에서 전송 중 및 유휴 상태의 데이터를 암호화하는 방법에 대해 알아봅니다.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# Adobe Experience Platform의 데이터 암호화

Adobe Experience Platform은 엔터프라이즈 솔루션 전반에 걸쳐 고객 경험 데이터를 중앙 집중화하고 표준화하는 강력하고 확장 가능한 시스템입니다. Platform에서 사용하는 모든 데이터는 데이터를 안전하게 유지하기 위해 전송 중이거나 사용하지 않을 때 암호화됩니다. 이 문서에서는 Platform의 암호화 프로세스에 대해 자세히 설명합니다.

다음 프로세스 흐름 다이어그램은에서 데이터를 어떻게 수집, 암호화 및 지속하는지를 보여 줍니다. [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## 전송 중인 데이터 {#in-transit}

플랫폼과 모든 외부 구성 요소 간에 전송되는 모든 데이터는 HTTPS를 사용하여 안전하고 암호화된 연결을 통해 수행됩니다 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

일반적으로 데이터는 다음 세 가지 방법으로 플랫폼에 가져옵니다.

* [데이터 수집](../../collection/home.md) 기능을 사용하면 웹 사이트 및 모바일 애플리케이션에서 데이터를 Platform Edge Network로 전송하여 수집을 위한 준비 및 준비를 할 수 있습니다.
* [소스 커넥터](../../sources/home.md) Adobe Experience Cloud 애플리케이션 및 기타 엔터프라이즈 데이터 소스에서 플랫폼으로 직접 데이터를 스트리밍합니다.
* Adobe이 아닌 ETL(추출, 변환, 로드) 도구에서 [일괄 처리 수집 API](../../ingestion/batch-ingestion/overview.md) 소비용입니다.

데이터를 시스템으로 가져온 후 [사용하지 않을 때 암호화](#at-rest)그런 다음 Platform 서비스로 보강하고 다음 방법으로 시스템에서 가져올 수 있습니다.

* [대상](../../destinations/home.md) 을 사용하면 Adobe 애플리케이션 및 파트너 애플리케이션에 데이터를 활성화할 수 있습니다.
* 과 같은 기본 플랫폼 애플리케이션 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 또한 데이터를 사용할 수 있습니다.

## 유휴 상태 데이터 {#at-rest}

Platform에서 수집 및 사용하는 데이터는 원본 또는 파일 형식에 관계없이 시스템에서 관리하는 모든 데이터가 포함된 매우 세분화된 데이터 저장소인 데이터 레이크에 저장됩니다. 데이터 레이크에서 지속되는 모든 데이터는 격리된 위치에서 암호화, 저장 및 관리됩니다 [[!DNL Microsoft Azure Data Lake] 스토리지](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 조직에 고유한 인스턴스.

사용하지 않는 데이터를 Azure Data Lake Storage에서 암호화하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [공식 Azure 설명서](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 다음 단계

이 문서는 Platform에서 데이터가 암호화되는 방식에 대한 높은 수준의 개요를 제공했습니다. Platform의 보안 절차에 대한 자세한 내용은 [거버넌스, 개인 정보 보호 및 보안](./overview.md) Experience League 시 또는 [플랫폼 보안 백서](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
