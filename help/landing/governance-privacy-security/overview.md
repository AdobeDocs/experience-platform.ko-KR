---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 거버넌스, 개인 정보 및 보안 개요
description: Adobe Experience Platform은 비즈니스 작업, 법적 의무 및 개발 프로세스를 준수하기 위해 수집된 경험 데이터를 자신 있게 제어할 수 있는 몇 가지 서비스 및 도구를 제공합니다.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# Adobe Experience Platform의 거버넌스, 개인 정보 및 보안

Adobe Experience Platform을 사용하면 데이터를 수집, 분석, 최적화 및 처리하여 고객 경험을 크게 향상시킬 수 있습니다. 이 데이터는 거대하고 복잡하며 믿을 수 없을 만큼 중요합니다. 데이터 운영, 비즈니스가 운영하는 법적 관할 구역, 데이터 사용과 관련된 조직 정책에 따라 비즈니스 이익을 보호하기 위해 고객 경험 데이터의 수집 및 사용을 신중하게 제어하고 모니터링해야 합니다.

Experience Platform은 비즈니스 작업, 법적 의무 및 개발 프로세스를 준수하기 위해 수집된 경험 데이터를 자신 있게 제어할 수 있는 몇 가지 서비스 및 도구를 제공합니다. 아래 섹션에서는 이러한 각 서비스에 대한 소개와 추가 정보를 위한 설명서 링크를 제공합니다.

서비스는 다음 세 가지 도메인으로 분류할 수 있습니다.

* [데이터 거버넌스](#governance)
* [개인정보 보호](#privacy)
* [보안](#security)

## 데이터 거버넌스 {#governance}

데이터 거버넌스는 Experience Platform의 모든 기능과 결합되는 필수 개념입니다. 데이터 거버넌스는 플랫폼을 통해 여정 전체에서 데이터를 제어하고 파악하는 기능을 나타냅니다. 데이터 품질, 데이터 계보, 데이터 카탈로그 작성 등을 관리합니다.

### Adobe Experience Platform 데이터 거버넌스 {#data-governance}

Adobe Experience Platform 데이터 거버넌스는 플랫폼 서비스로서 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하도록 합니다. 데이터 사용 레이블 지정, 데이터 사용 정책, 정책 적용, 데이터 계보 등 다양한 수준에서 Experience Platform 내에서 주요 역할을 합니다.

자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md) 추가 정보.

### 카탈로그 및 데이터 세트 {#catalog}

카탈로그 서비스는 플랫폼 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 파일 및 디렉터리로 데이터 레이크에 저장되지만 카탈로그에는 조회 및 모니터링을 위해 해당 파일 및 디렉토리의 메타데이터와 설명이 저장됩니다.

카탈로그에서는 수집된 데이터를 데이터 세트로 분류하고 이 데이터 세트에 포함된 데이터에 레이블을 지정하고 분류하는 데 사용할 수 있는 메타데이터가 포함된 각 데이터 세트를 구성합니다.

자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md) 를 참조하십시오. Experience Platform에서 데이터 세트를 관리하는 방법에 대해 알아보려면 [데이터 세트 개요](../../catalog/datasets/overview.md).

## 개인정보 보호 {#privacy}

개인 정보는 비즈니스, 국회의원 및 고객에게 중요한 문제입니다. 고객으로부터 수집한 개인 데이터는 거의 모든 Experience Platform 워크플로우의 핵심이므로 Platform은 이러한 이니셔티브를 지원하는 서비스를 제공합니다.

### Adobe Experience Platform Privacy Service {#privacy-service}

유럽 연합의 GDPR(General Data Protection Regulation) 및 CCPA(California Consumer Privacy Act)와 같은 법적 개인 정보 보호 규정에서는 관할 구역 내의 시민들에게 수집하여 저장하는 개인 데이터에 대한 액세스 및 삭제 권한을 부여합니다.

Adobe Experience Platform Privacy Service은 이러한 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. Privacy Service을 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터에 액세스하거나 삭제하기 위한 요청을 제출할 수 있으므로, 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수하도록 도와줍니다.

자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md) 추가 정보.

### 동의 처리 {#consent}

많은 법률 개인 정보 보호 규정에서 데이터 수집, 개인화 및 기타 마케팅 사용 사례와 관련하여 활성 및 특정 동의에 대한 요구 사항을 도입했습니다. 이러한 요구 사항을 충족하기 위해 Experience Platform을 사용하면 개별 고객 프로필에서 동의 정보를 캡처하고 이러한 환경 설정을 다운스트림 플랫폼 워크플로우에서 각 고객의 데이터가 사용되는 방식에 대한 결정 요소로 사용할 수 있습니다.

Adobe 표준을 사용하여 고객 동의 및 기본 설정 데이터를 처리하는 방법에 대해 알려면 [Experience Platform의 동의 처리](./consent/adobe/overview.md).

IAB TCF(Transparency and Consent Framework) 2.0에 따라 고객 동의 데이터를 처리하는 방법에 대한 자세한 내용은 [플랫폼에서 IAB TCF 2.0 지원](./consent/iab/overview.md).

## 보안 {#security}

데이터의 무결성과 보안은 비즈니스에 필수적이며, 이러한 위험에는 업계 최고의 보안 기능이 필요합니다. 이러한 과제를 해결하기 위해 Platform은 데이터 작업을 보호하는 데 도움이 되는 몇 가지 도구를 제공합니다.

### 데이터 암호화

모든 플랫폼 데이터는 전송 및 중단 시 암호화됩니다. 다음 문서를 참조하십시오. [플랫폼의 데이터 암호화](./encryption.md) 추가 정보.

### 액세스 제어 {#access-control}

Experience Platform은 Adobe Admin Console을 사용하여 다양한 플랫폼 기능에 대한 역할 기반 액세스 제어를 제공합니다. 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다.

자세한 내용은 [액세스 제어 개요](../../access-control/home.md) 추가 정보.

### 샌드박스 {#sandboxes}

Experience Platform은 글로벌 규모로 디지털 경험 애플리케이션을 보강하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 운영하고 있으며 운영 규정을 준수하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 충족해야 합니다.

개발 유연성의 필요성을 해결하기 위해, Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스 를 제공하여 자체 개발 라이프사이클을 기반으로 디지털 경험 애플리케이션을 발전시킵니다.

자세한 내용은 [샌드박스 개요](../../sandboxes/home.md) 추가 정보.

## 다음 단계

이 문서에서는 데이터 거버넌스, 개인 정보 보호 및 보안과 관련된 다양한 플랫폼 서비스 및 도구에 대한 개요를 제공합니다. 이러한 기능에 대한 자세한 내용은 이 안내서 전체에서 연결된 설명서를 참조하십시오.
