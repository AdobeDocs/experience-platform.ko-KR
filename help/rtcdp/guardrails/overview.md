---
title: Real-Time CDP 가드 레일
description: Real-Time CDP의 다양한 서비스 및 영역에서 데이터 가드레일에 대해 알아봅니다.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: af37aca17f4b365b52215b8c886e733f00c4a4e8
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# Real-Time CDP 가드 레일

가드레일은 Real-Time CDP에서 데이터 및 시스템 사용, 성능 최적화 및 오류나 예기치 않은 결과의 회피를 위한 지침을 제공하는 임계값입니다. 보호 기능은 라이선스 권한과 관련하여 데이터 사용 또는 소비 및 처리를 의미할 수 있습니다.

여기에서 시작하여 아래 링크를 따라 Real-Time CDP의 다양한 서비스 및 영역에서 발생하는 모든 보호 기능에 대해 알아보십시오.

* [데이터 수집 보호](/help/ingestion/guardrails.md)
* [다음을 위한 보호 기능 [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [의 보호 기능 [!DNL Real-Time Customer Profile] 데이터 및 세분화](/help/profile/guardrails.md)
* [의 보호 기능 [!DNL Identity Service] 데이터](/help/identity-service/guardrails.md)
* [의 보호 기능 [!DNL Query Service]](/help/query-service/guardrails.md)
* [대상을 통한 데이터 활성화 보호](/help/destinations/guardrails.md)
* [Real-Time CDP B2B 보호](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>또한 다음을 방문하십시오. [digital experience 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) 추가 정보: [엔드 투 엔드 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 다양한 Experience Platform 서비스용.


## 보호 유형 {#guardrail-types}

모든 Real-Time CDP 영역 및 서비스에 대한 두 가지 보호 유형은 다음과 같습니다.

| 보호 유형 | 설명 |
|----------|---------|
| **성능 보호(소프트 제한)** | 성능 보호는 사용 사례의 범위와 관련된 사용 제한입니다. 성능 가드레일을 초과하면 성능 저하 및 지연이 발생할 수 있습니다. Adobe은 이러한 성능 저하의 원인이 아닙니다. 성능 가드레일을 지속적으로 초과하는 고객은 성능 저하를 방지하기 위해 추가 용량의 라이센스를 선택할 수 있습니다. |
| **시스템 시행 보호(하드 제한)** | 시스템에서 적용되는 가드레일은 Real-Time CDP UI 또는 API에 의해 적용됩니다. 이는 UI 및 API가 귀하를 차단하거나 오류를 반환하므로 초과할 수 없는 제한입니다. |

{style="table-layout:auto"}

## Real-Time CDP 라이선싱 및 권한 부여 정보 {#product-descriptions}

또한 구입한 Real-Time CDP 버전 및 계층을 기반으로 하는 라이선스 및 자격 정보는 아래 제품 설명 링크를 참조하십시오.

* [모든 Adobe 제품 설명](https://helpx.adobe.com/legal/product-descriptions.html)
* [Real-time Customer Data Platform (B2C 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## 기타 Experience Platform 애플리케이션의 보호 기능  {#guardrails-other-aep-apps}

다른 Experience Platform 애플리케이션에도 유사한 보호 기능이 있습니다. 자세한 내용은 아래 링크를 참조하십시오.

* [Adobe Journey Optimizer 보호 기능](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Customer Journey Analytics 보호](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## 다음 단계

Real-Time CDP의 다양한 영역과 서비스에 적용되는 가드레일을 이해한 후에는 [Real-Time CDP 구현의 샘플 사용 사례](/help/rtcdp/get-started.md).
