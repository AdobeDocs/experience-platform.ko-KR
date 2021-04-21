---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 거버넌스, 개인정보 보호 및 보안 개요
topic-legacy: overview
description: Adobe Experience Platform은 비즈니스 방침, 법적 책임 및 개발 프로세스를 준수하기 위해 수집한 경험 데이터를 안전하게 제어할 수 있는 다양한 서비스와 툴을 제공합니다.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---

# Adobe Experience Platform의 거버넌스, 개인 정보 보호 및 보안

Adobe Experience Platform을 사용하면 데이터를 인제스트, 분석, 최적화 및 실행함으로써 고객 경험을 대폭 향상시킬 수 있습니다. 이 데이터는 방대하고 복잡하며 믿을 수 없을 정도로 소중합니다. 데이터 운영의 특성, 귀하의 사업이 운영하는 법적 관할 구역 및 데이터 사용과 관련된 조직의 정책에 따라 비즈니스 이익을 보호하기 위해 고객 경험 데이터의 수집 및 사용을 신중하게 제어하고 모니터링해야 합니다.

Experience Platform은 비즈니스 관행, 법적 책임 및 개발 프로세스를 준수하기 위해 수집한 경험 데이터를 안전하게 제어할 수 있는 다양한 서비스 및 툴을 제공합니다. 아래 섹션에서는 추가 정보를 제공하는 설명서로 연결되는 링크와 함께 이러한 각 서비스에 대한 소개를 제공합니다.

서비스는 다음 3개의 도메인으로 분류할 수 있습니다.

* [데이터 거버넌스](#governance)
* [개인 정보 보호](#privacy)
* [보안](#security)

## 데이터 거버넌스 {#governance}

데이터 거버넌스는 Experience Platform의 모든 기능과 함께 사용할 수 있는 필수적인 개념입니다. 데이터 거버넌스는 플랫폼을 통해 여정 전반에 걸쳐 데이터를 제어 및 파악할 수 있는 기능을 나타냅니다. 데이터 품질, 데이터 연결, 데이터 카탈로그 작성 등을 유지 관리할 수 있습니다.

### Adobe Experience Platform 데이터 거버넌스 {#data-governance}

플랫폼 서비스인 Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다. 데이터 사용 표시, 데이터 사용 정책, 정책 실행, 데이터 계통 등 다양한 수준에서 Experience Platform 내에서 중요한 역할을 합니다.

자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하십시오.

### 카탈로그 및 데이터 집합 {#catalog}

Catalog Service는 Platform의 데이터 위치 및 리니지에 대한 레코드 시스템입니다. Experience Platform에 인제스트된 모든 데이터가 파일 및 디렉터리로 Data Lake에 저장되지만 카탈로그는 조회 및 모니터링을 위해 해당 파일 및 디렉토리에 대한 메타데이터와 설명을 보관합니다.

카탈로그는 데이터를 데이터 집합에 구성합니다. 여기에는 포함된 데이터의 레이블과 분류하는 데 사용할 수 있는 메타데이터가 포함된 각 데이터 세트가 있습니다.

서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하십시오. Experience Platform에서 데이터 세트를 관리하는 방법에 대해 알아보려면 [데이터 집합 개요](../../catalog/datasets/overview.md)를 참조하십시오.

## 개인 정보 {#privacy}

개인 정보는 비즈니스, 국회의원 및 고객에게 매우 중요한 문제입니다. 고객으로부터 수집한 개인 데이터는 거의 모든 Experience Platform 워크플로우의 핵심이므로 Platform은 이러한 이니셔티브를 지원하는 서비스를 제공합니다.

### Adobe Experience Platform Privacy Service {#privacy-service}

유럽연합(EU)의 개인 정보 보호 규정(GDPR) 및 캘리포니아 소비자 개인 정보 보호 법(CPA)과 같은 법적 개인 정보 보호 규정에서는 해당 관할 지역 시민들에게 수집해서 저장하는 개인 데이터를 액세스하고 삭제할 수 있는 권한을 부여합니다.

Adobe Experience Platform Privacy Service은 이러한 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. Privacy Service을 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스하거나 삭제하도록 요청을 제출할 수 있으므로 법률 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md)를 참조하십시오.

### 동의 처리 {#consent}

많은 법률 개인 정보 보호 규정에서 데이터 수집, 개인화 및 기타 마케팅 사용 사례와 관련하여 적극적인 구체적인 동의에 대한 요구 사항을 도입했습니다. 이러한 요구 사항을 충족하기 위해 Experience Platform을 사용하면 개별 고객 프로파일에서 동의 정보를 캡처하고 이러한 기본 설정을 다운스트림 플랫폼 워크플로우에서 각 고객의 데이터가 사용되는 방식을 결정하는 요소로 사용할 수 있습니다.

Adobe 표준을 사용하여 고객 동의 및 선호 데이터를 처리하는 방법에 대해 알려면 Experience Platform](./consent/adobe/overview.md)의 [동의 처리에 대한 개요를 참조하십시오.

IAB 투명도 및 동의 프레임워크(TCF) 2.0에 따라 고객 동의 데이터를 처리하는 방법에 대한 자세한 내용은 플랫폼](./consent/iab/overview.md)에서 [IAB TCF 2.0 지원에 대한 개요를 참조하십시오.

## 보안 {#security}

데이터의 무결성과 보안은 비즈니스에서 없어서는 안 될 요소이며 이러한 위험을 무릅쓰려면 업계 선도적인 보안 기능이 필요합니다. 이 문제를 해결하기 위해 Platform(플랫폼)은 데이터 작업을 안전하게 보호할 수 있는 다양한 툴을 제공합니다.

### 액세스 제어 {#access-control}

Experience Platform은 Adobe Admin Console을 사용하여 다양한 플랫폼 기능에 대한 역할 기반 액세스 제어를 제공합니다. 이 기능은 Admin Console의 제품 프로필을 활용하므로 사용자에게 사용 권한 및 샌드박스를 연결합니다.

자세한 내용은 [액세스 제어 개요](../../access-control/home.md)를 참조하십시오.

### 샌드 박스 {#sandboxes}

Experience Platform은 디지털 경험 애플리케이션을 글로벌 규모로 보완하도록 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 고려해야 합니다.

개발 유연성의 필요성을 해결하기 위해 Experience Platform은 단일 플랫폼 인스턴스를 개별 가상 환경으로 분할하는 샌드박스를 제공하므로, 개발 라이프사이클을 기반으로 디지털 경험 애플리케이션을 발전시킬 수 있습니다.

자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## 다음 단계

이 문서에서는 데이터 거버넌스, 개인정보 보호 및 보안과 관련된 다양한 플랫폼 서비스 및 도구에 대한 개요를 제공합니다. 이러한 기능에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.
