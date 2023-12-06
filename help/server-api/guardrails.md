---
title: Edge Network Server API의 성능 보호 기능
description: 최적의 성능 보호 내에서 서버 API를 사용하는 방법에 대해 알아봅니다.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---


# Edge Network Server API의 성능 보호 기능

## 개요 {#overview}

성능 보호는 서버 API 사용 사례와 관련된 사용 제한을 정의합니다. 이 문서에 설명된 성능 가드레일을 초과하면 성능이 저하될 수 있습니다.

Adobe은 사용 제한 초과로 인한 성능 저하의 책임이 없습니다. 성능 가드레일을 지속적으로 초과하는 고객은 성능 저하를 방지하기 위해 추가 처리 용량을 요청할 수 있습니다.

## 정의

* **사용 가능** 은 5분 간격으로 오류와 함께 실패하지 않고 프로비저닝된 Edge Network API와만 관련된 Experience Platform Edge Network에서 처리된 요청의 백분율로 계산됩니다. 테넌트가 주어진 5분 간격으로 요청을 수행하지 않은 경우 해당 간격은 100%로 간주됩니다.
* **월별 가동 시간 비율** 주어진 지역에 대해 한 달에 있는 5분 간격 모두에 대한 가용성의 평균으로 계산됩니다.
* An **업스트림** 는 Adobe 서버측 전달, Adobe Edge 세그멘테이션 또는 Adobe Target과 같은 특정 데이터스트림에 대해 활성화된 Edge Network 뒤의 서비스입니다.
* A **요청 단위** 는 데이터 스트림에 대해 구성된 요청 및 하나의 업스트림에 대한 8KB 조각에 해당합니다.
* A **요청** 은 고객 소유 애플리케이션에서 로 보내는 단일 메시지입니다. [!DNL Server API]. 요청에는 하나 이상의 요청 단위가 포함될 수 있습니다.
* An **오류** 은(는) Edge 네트워크로 인해 실패하는 모든 요청입니다 [내부 서비스 오류](error-handling.md).

## 서비스 제한

모든 데이터 스트림은 특정 사용 제한을 적용하여 주로 동시에 전송할 수 있는 이벤트 수, 크기 및 이러한 요청이 라우팅되는 업스트림 서비스 수를 제어합니다.

### 요청 단위

모든 제한이 다음에 걸쳐 적용되고 표준화됨: **요청 단위(RU)**&#x200B;로 정의됨 **8KB 조각** 데이터 스트림에 구성된 하나의 업스트림 서비스로 이동하는 요청.

#### 예시

| 데이터스트림당 구성된 업스트림 | 평균 요청 크기 | 요청 단위 |
| --- | --- | --- |
| 1(Adobe 플랫폼) | 8KB(조각 1개) | 1 |
| 2 (Adobe 플랫폼, Adobe Target) | 8KB(조각 1개) | 2 |
| 2 (Adobe 플랫폼, Adobe Target) | 16KB(조각 2개) | 4 |
| 2 (Adobe 플랫폼, Adobe Target) | 64KB(조각 8개) | 16 |

### 요청 단위 제한

아래 표는 기본 제한 값을 보여 줍니다. 더 높은 요청 단위 제한이 필요한 경우 계정 담당자에게 문의하십시오.

| 엔드포인트 | 초당 요청 단위 |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### HTTP 요청 크기 제한

| 페이로드 형식 | 요청의 최대 크기 | 최대 8KB 요청 조각 |
| --- | --- | --- |
| JSON 일반 텍스트 | 64KB | 8 |


>[!NOTE]
>
>페이로드 자체에 따라 이진 형식은 일반적으로 20~40% 더 컴팩트하므로 일반 텍스트 JSON에서보다 더 많은 데이터를 푸시할 수 있습니다. 데이터 스트림에 더 많은 용량이 필요한 경우 고객 지원 센터 담당자에게 문의하십시오.

## 다음 단계

Real-Time CDP 제품 설명 문서의 기타 Experience Platform 서비스 보호, 종단 간 지연 정보 및 라이선스 정보에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Real-Time CDP 보호 기능](/help/rtcdp/guardrails/overview.md)
* [엔드 투 엔드 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 다양한 Experience Platform 서비스용.
* [Real-time Customer Data Platform (B2C 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
