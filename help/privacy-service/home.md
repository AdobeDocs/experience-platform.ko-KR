---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform 개인 정보 보호 서비스
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Adobe Experience Platform 개인 정보 보호 서비스 개요

더 나은 고객 경험을 제공하려면 고객의 개인 데이터를 수집하여 저장해야 합니다. 이 데이터를 사용하는 경우 고객의 개인 정보를 이해하고 존중해야 합니다. 새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다.

Adobe Experience Platform 개인 정보 보호 서비스는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 개인 정보 보호 서비스를 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스하고 삭제할 수 있는 요청을 제출하여 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

## 개인 정보 서비스를 사용해야 하는 이유

개인 정보 보호 서비스는 비즈니스가 고객의 개인 데이터를 관리하는 데 필요한 기본적인 변화에 대응하여 개발되었습니다. 개인정보 보호 서비스의 주된 목적은 데이터 개인 정보 보호 규정 준수를 자동화하는 것입니다. 이러한 규정을 위반하면 중대한 벌금을 내고 비즈니스 데이터 운영을 방해할 수 있습니다.

### 개인 정보 보호 서비스 및 GDPR

개인 [정보 보호 규정](https://eugdpr.org/) (GDPR)은 액세스 권한 **및** 잊혀질 권리 등 유럽 연합 **회원에게 새로운 몇 가지 데이터**&#x200B;개인정보 보호 권한을도입했습니다. 즉, 귀사에서 개인 데이터를 수집한 모든 EU 시민이 언제든지 해당 데이터에 액세스하거나 삭제를 요청할 수 있습니다. 이러한 요청을 30일 이내에 이행하지 않으면 조직에 수백만 달러의 벌금을 부과할 수 있습니다.

개인 정보 보호 서비스는 GDPR에 대한 액세스 및 삭제 요청을 지원하고 CPA 규정에 따른 요청과 별도로 추적합니다. 자세한 내용은 [GDPR FAQ](gdpr/faq.md) 및 [용어](gdpr/terminology.md) 문서를참조하십시오.

### 개인 정보 보호 서비스 및 CPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. CPA는 캘리포니아 거주자에게 개인 데이터에 액세스하고 삭제할 수 있는 권리, 개인 데이터의 판매 또는 공개 여부, 그리고 제3자에게 자신의 데이터를 판매하는 것을 거부할 수 있는 권리 등 새로운 데이터 개인정보 보호 권한을 제공합니다.

개인 정보 보호 서비스는 CPA 규정에 대한 액세스 및 삭제 요청을 지원하고 GDPR 요청과는 별도로 추적합니다. 또한 개인 정보 보호 서비스는 Experience Cloud 애플리케이션을 지원하는 옵트아웃 요청 전송을 지원합니다. 자세한 내용은 [CPA](ccpa/faq.md) FAQ를 참조하십시오.

## 개인정보 보호 서비스를 사용하여 개인 정보 작업 요청을 관리하는 방법

개인 정보 보호 서비스는 고객의 개인 데이터에 액세스/삭제 또는 판매 거부( **개인 정보 보호라고도**&#x200B;함)를 요청하는 고객의 요청을 관리할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다. 또한 이 서비스는 Experience Cloud 응용 프로그램과 관련된 개인 정보 작업의 상태 및 결과를 볼 수 있도록 해주는 중앙 감사 및 로깅 메커니즘을 제공합니다.

>[!NOTE] 옵트아웃 요청은 현재 개인정보 보호 서비스 API에서만 지원됩니다.

### API 사용

Privacy [Service API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 사용하면 RESTful API 호출을 사용하여 개인 정보 작업을 만들고 관리할 수 있으므로 Experience Cloud 응용 프로그램에 대한 개인 정보 보호 규정 준수에 프로그래밍 방식으로 액세스할 수 있습니다. API 사용 방법에 대한 자세한 내용은 Privacy Service API [개발자 안내서를](api/getting-started.md)참조하십시오.

### UI 사용

개인 정보 서비스 UI를 사용하면 그래픽 인터페이스를 사용하여 개인 정보 작업을 만들고 모니터링할 수 있습니다. UI에는 **모든 활성** 요청의 상태를 시각적으로 표시하는 상태 보고서 위젯이 포함되어 있으며, 기본 제공 요청 빌더를 사용하거나 JSON **파일을 업로드하여 새 요청을 만들** 수 있습니다. UI 사용에 대한 자세한 내용은 개인 정보 서비스 [사용 안내서를](ui/overview.md)참조하십시오.