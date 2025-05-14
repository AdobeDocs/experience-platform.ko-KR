---
title: Adobe Experience Platform의 데이터 암호화
description: Adobe Experience Platform에서 전송 중 및 유휴 상태의 데이터를 암호화하는 방법에 대해 알아봅니다.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Adobe Experience Platform의 데이터 암호화

Adobe Experience Platform은 엔터프라이즈 솔루션 전반에 걸쳐 고객 경험 데이터를 중앙 집중화하고 표준화하는 강력하고 확장 가능한 시스템입니다. Experience Platform에서 사용하는 모든 데이터는 데이터를 안전하게 유지하기 위해 전송 중이거나 사용하지 않을 때 암호화됩니다. 이 문서에서는 Experience Platform의 암호화 프로세스에 대해 자세히 설명합니다.

다음 프로세스 흐름 다이어그램은 Experience Platform이 데이터를 어떻게 수집, 암호화 및 유지하는지 보여 줍니다.

![Experience Platform에서 데이터를 수집, 암호화 및 유지하는 방법을 보여 주는 다이어그램입니다.](../images/governance-privacy-security/encryption/flow.png)

## 전송 중인 데이터 {#in-transit}

Experience Platform과 외부 구성 요소 간에 전송되는 모든 데이터는 HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)을(를) 사용하여 안전하고 암호화된 연결을 통해 수행됩니다.

일반적으로 데이터는 다음 세 가지 방법으로 Experience Platform에 가져옵니다.

- [데이터 수집](../../collection/home.md) 기능을 사용하면 웹 사이트 및 모바일 응용 프로그램에서 스테이징 및 수집 준비를 위해 Experience Platform Edge Network으로 데이터를 전송할 수 있습니다.
- [Source 커넥터](../../sources/home.md) 데이터를 Adobe Experience Cloud 응용 프로그램 및 기타 엔터프라이즈 데이터 원본에서 Experience Platform으로 직접 스트리밍합니다.
- 비 Adobe ETL(추출, 변환, 로드) 도구는 사용을 위해 데이터를 [일괄 처리 수집 API](../../ingestion/batch-ingestion/overview.md)에 보냅니다.

데이터가 시스템에 추가되고 [사용하지 않을 때 암호화됨](#at-rest)되면 Experience Platform 서비스는 다음과 같은 방법으로 데이터를 보강하고 내보냅니다.

- [대상](../../destinations/home.md)을(를) 사용하면 Adobe 응용 프로그램 및 파트너 응용 프로그램에 데이터를 활성화할 수 있습니다.
- [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko) 및 [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/ajo-home)과 같은 기본 Experience Platform 응용 프로그램에서도 데이터를 사용할 수 있습니다.

### mTLS 프로토콜 지원 {#mtls-protocol-support}

이제 mTLS(상호 전송 계층 보안)를 사용하여 [HTTP API 대상](../../destinations/catalog/streaming/http-destination.md) 및 Adobe Journey Optimizer [사용자 지정 작업](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)에 대한 아웃바운드 연결에서 보안을 강화할 수 있습니다. mTLS는 상호 인증을 위한 종단간 보안 방법으로, 정보를 공유하는 양 당사자가 데이터를 공유하기 전에 자신이 주장하는 사람임을 보장합니다. mTLS에는 TLS와 비교하여 추가 단계가 포함되어 있으며, 이 단계에서 서버는 클라이언트의 인증서를 요청하고 마지막에 검증한다.

[Adobe Journey Optimizer 사용자 지정 작업 및 Experience Platform HTTP API 대상 워크플로우와 함께 mTLS를 사용](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration)하려면 Adobe Journey Optimizer 고객 작업 UI 또는 대상 UI에 입력하는 서버 주소에 TLS 프로토콜이 비활성화되어 있고 mTLS만 활성화되어야 합니다. 해당 끝점에서 TLS 1.2 프로토콜이 여전히 활성화되어 있으면 클라이언트 인증을 위한 인증서가 전송되지 않습니다. 즉, 이러한 워크플로에서 mTLS를 사용하려면 &quot;받는 중&quot; 서버 끝점이 mTLS **only** 사용 연결 끝점이어야 합니다.

>[!IMPORTANT]
>
>mTLS를 활성화하기 위해 Adobe Journey Optimizer 사용자 지정 작업 또는 HTTP API 대상에 추가 구성이 필요하지 않습니다. 이 프로세스는 mTLS 활성화 끝점이 감지되면 자동으로 발생합니다. 각 인증서에 대한 일반 이름(CN) 및 주체 대체 이름(SAN)은 인증서의 일부로 설명서에서 사용할 수 있으며, 원할 경우 소유권 유효성 검사의 추가 계층으로 사용할 수 있습니다.
>
>2000년 5월에 게시된 RFC 2818은 주체 이름 확인을 위해 HTTPS 인증서의 CN(일반 이름) 필드를 사용하는 것을 중단합니다. 대신 &quot;dns name&quot; 유형의 &quot;SAN(주체 대체 이름)&quot;을 사용하는 것이 좋습니다.

### 인증서 다운로드 {#download-certificates}

>[!NOTE]
>
>시스템에서 유효한 공개 인증서를 사용하도록 할 책임이 있습니다. 특히 만료일이 다가오면 정기적으로 인증서를 검토하십시오. API를 사용하여 인증서가 만료되기 전에 인증서를 검색하고 업데이트합니다.

공개 mTLS 인증서에 대한 직접 다운로드 링크는 더 이상 제공되지 않습니다. 대신 [공개 인증서 끝점](../../data-governance/mtls-api/public-certificate-endpoint.md)을 사용하여 인증서를 검색합니다. 현재 공개 인증서에 액세스하는 데 지원되는 유일한 방법입니다. 이를 통해 통합에 대해 항상 유효한 최신 인증서를 받을 수 있습니다.

인증서 기반 암호화에 의존하는 통합은 API를 사용한 자동화된 인증서 검색을 지원하도록 워크플로우를 업데이트해야 합니다. 정적 링크 또는 수동 업데이트에 의존하면 만료되거나 해지된 인증서가 사용되어 통합이 실패할 수 있습니다.

#### 인증서 라이프사이클 자동화 {#certificate-lifecycle-automation}

이제 Adobe은 mTLS 통합을 위한 인증서 라이프사이클을 자동화하여 신뢰성을 향상시키고 서비스 중단을 방지합니다. 공개 인증서는 다음과 같습니다.

- 만료 60일 전에 다시 발급되었습니다.
- 만료 30일 전에 해지되었습니다.

이러한 간격은 인증서 수명을 최대 47일로 줄이는 것을 목표로 하는 [진화하는 CA/B 포럼 지침](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)에 따라 계속 짧아집니다.

이전에 이 페이지에서 링크를 사용하여 인증서를 다운로드한 경우 API를 통해 독점적으로 검색하도록 프로세스를 업데이트합니다.

## 유휴 상태 데이터 {#at-rest}

Experience Platform에서 수집되고 사용되는 데이터는 원본 또는 파일 형식과 관계없이 시스템에서 관리하는 모든 데이터가 포함된 매우 세분화된 데이터 저장소인 데이터 레이크에 저장됩니다. 데이터 레이크에서 지속되는 모든 데이터는 조직에 고유한 격리된 [[!DNL Microsoft Azure Data Lake] 저장소](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 인스턴스에서 암호화, 저장 및 관리됩니다.

사용하지 않는 데이터를 Azure Data Lake Storage에서 암호화하는 방법에 대한 자세한 내용은 [공식 Azure 설명서](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption)를 참조하세요.

## 다음 단계

이 문서는 Experience Platform에서 데이터가 암호화되는 방식에 대한 높은 수준의 개요를 제공했습니다. Experience Platform의 보안 절차에 대한 자세한 내용은 Experience League의 [거버넌스, 개인 정보 보호 및 보안에 대한 개요](./overview.md)를 참조하거나 [Experience Platform 보안 백서](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)를 참조하십시오.
