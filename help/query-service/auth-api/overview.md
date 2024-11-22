---
title: Data Distiller Authorization API 안내서
description: Data Distiller 인증 API를 사용하여 SQL을 통한 보안 연결에 네트워크 기반 IP 제한을 적용하는 방법에 대해 알아봅니다. 이 API를 사용하여 Adobe Experience Platform 데이터에 대한 데이터 액세스 제어를 강화합니다.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: 804eeb4ec976cf41fdd450bd8f307499c3ebae03
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---

# Data Distiller Authorization API 안내서

>[!AVAILABILITY]
>
>이 기능은 Data Distiller 추가 기능을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

Data Distiller Authorization API를 사용하여 IP 기반 제한을 적용합니다. 이러한 측정값을 적용하면 승인된 네트워크와 클라이언트 컴퓨터만 Adobe Experience Platform의 SQL을 통해 데이터에 액세스할 수 있습니다. 이러한 제어 기능을 통해 엄격한 보안 표준을 충족하는 동시에 실시간 액세스 모니터링 및 경고 기능을 제공할 수 있습니다.

이 API를 사용하면 SQL 인터페이스를 통해 데이터에 액세스하기 위한 IP 제한을 구성, 적용 및 모니터링할 수 있습니다. 이 문서에서는 API의 핵심 기능, 엔드포인트 기능 및 향후 기능에 대한 높은 수준의 개요를 제공합니다.

## 주요 기능

다음 기능을 사용하면 IP 기반 액세스 제한을 정의하고, 액세스 시도를 모니터링하며, 쿼리 서비스에 대한 네트워크 보안 설정을 사용자 지정할 수 있습니다.

- **네트워크 기반 데이터 액세스 제어 정의**: 쿼리 서비스 액세스에 허용된 IP 범위를 지정합니다. 이 제한은 특히 BI(Business Intelligence) 도구, 데이터베이스 클라이언트 또는 JDBC와 같은 프로그래밍 인터페이스를 통해 수행되는 연결을 포함한 SQL 데이터베이스 연결에 적용됩니다.
- **포괄적인 모니터링 및 경고 활성화**: 거부된 연결을 포함한 모든 액세스 시도가 기록되고 실시간 추적을 위해 [Adobe Experience Platform 감사 로그](../../landing/governance-privacy-security/audit-logs/overview.md)에 전송됩니다. 이 기능을 사용하여 액세스 패턴을 모니터링하고 잠재적인 보안 위반을 감지합니다.
- **유연한 IP 제한 구성**: 개별 IP 및 CIDR 블록 형식 모두에서 허용되는 IP를 지정하십시오. 이러한 설정은 샌드박스마다 적용되므로 네트워크 제한을 특정 보안 요구 사항에 맞게 조정할 수 있습니다.

## 감사 및 모니터링 기능

보안 데이터 액세스 사례를 지원하기 위해 Query Service는 Experience Platform에 액세스하거나 액세스하려는 모든 클라이언트 IP를 기록합니다. 거부된 연결을 포함한 감사 이벤트는 플랫폼 감사 로그로 전송됩니다. 이를 통해 다음을 수행할 수 있습니다.

- **실시간 모니터링**: IP 기반 액세스 패턴을 추적하여 준수 여부를 확인합니다.
- **권한 없는 액세스에 대한 경고**: 권한 없는 IP에서 액세스 시도를 식별하고 응답합니다.

자세한 내용은 [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md)를 참조하세요.

## 다음 단계

필수 헤더 및 API 호출 규칙을 포함한 필수 설정 단계에 대해 [시작 안내서](./getting-started.md)를 검토하여 Data Distiller 인증 API를 시작하십시오. 그런 다음 보안 데이터 액세스를 구성하고 관리하기 위해 [IP 액세스](./ip-access.md) 및 [IP 유효성 검사](./validate.md)에서 끝점별 안내서를 살펴보십시오.

보다 쉬운 통합, 테스트 및 탐색을 위해 표준화되고 기계가 읽을 수 있는 형식을 보려면 [데이터 Distiller Authorization OpenAPI 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)를 참조하세요.

반환된 각 데이터 세트에 대한 다양한 응답 매개 변수에 대한 자세한 내용은 [데이터 세트 API 개발자 설명서](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets)를 참조하십시오.
