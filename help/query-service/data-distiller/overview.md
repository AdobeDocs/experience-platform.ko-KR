---
title: 데이터 Distiller 개요
description: 라이선스 자격과 관련된 쿼리 서비스 데이터의 데이터 Distiller 사용 제한에 대한 요약입니다.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 데이터 Distiller 개요

Data Distiller은 Adobe Experience Platform의 기능 하위 집합을 포함하는 패키지 오퍼링입니다. Data Distiller을 사용하면 쿼리 서비스에서 일괄 쿼리를 실행하여 실시간 고객 프로필 또는 분석 사용 사례에 대한 수집 후 데이터 준비(예: 청소, 셰이핑 및 조작)를 수행할 수 있습니다. Data Distiller의 사용은 플랫폼 기반 애플리케이션에 대한 권한 부여에 따라 달라집니다.

## 라이선스 사용 {#license-usage}

다음  [데이터 Distiller 라이선스 사용 대시보드](./license-usage.md) 는 Data Distiller 계산 시간을 구매하면 사용할 수 있습니다. 라이선스 사용 대시보드는 권한이 부여된 컴퓨팅 시간 소비를 모니터링하는 데 도움이 됩니다. 다음을 참조하십시오. [데이터 Distiller 라이선스 사용 문서](./license-usage.md) 조직의 Query Service 라이선스 사용에 대한 중요한 정보를 보려면

## 범위 지정 매개 변수 {#scoping-parameters}

범위 지정 매개 변수는 필요한 설정의 범위와 관련된 사용 제한이며 라이선스 능력에 따라 정의됩니다. 추가 기능이 없는 경우 Data Distiller의 범위 지정 매개 변수는 다음과 같습니다.

* **시간 계산**: PSQL 또는 쿼리 서비스 API를 사용하여 모든 샌드박스(예약됨 또는 다른 날짜)에서 실행되는 배치 쿼리를 실행하여 데이터를 스캔하고 쓸 수 있습니다. 이 작업에서는 라이선스 계약의 범위 프로세스에서 결정된 연간 할당된 컴퓨팅 시간을 사용합니다. 총 계산 시간은 모든 샌드박스에 누적됩니다.
* **데이터 수집됨**: Data Distiller을 사용하여 Adobe Experience Platform에 수집된 데이터는 Adobe Real-time Customer Data Platform, Customer Journey Analytics 및/또는 Adobe Journey Optimizer에 대한 당시 라이선스에 설명된 제한을 따릅니다.
* **데이터 레이크 스토리지**: Adobe Real-time Customer Data Platform, Customer Journey Analytics 및/또는 Adobe Journey Optimizer에 대한 당시 현재 라이선스에 제공된 데이터 레이크 저장소도 데이터 Distiller과 함께 사용할 수 있습니다. Data Lake Storage는 공유 기능입니다.
* **쿼리 서비스 사용자**: Adobe Real-time Customer Data Platform, Customer Journey Analytics 및/또는 Adobe Journey Optimizer에 대한 당시 현재 라이선스에 자세히 설명된 쿼리 서비스 사용자의 수도 Data Distiller과 함께 사용할 수 있습니다. 쿼리 서비스 사용자는 공유 기능입니다.

## 가드레일

다음을 참조하십시오. [쿼리 서비스 보호 기능](../guardrails.md) 라이선스 자격과 관련하여 쿼리 서비스 데이터의 기본 사용 제한에 대한 문서입니다.

## 정적 제한

정적 제한은 Adobe Experience Platform 활성화의 기능 경계와 관련된 사용 제한입니다. [Adobe Experience Platform 활성화에 대한 추가 정보](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) 은 Adobe 도움말 문서에서 찾을 수 있습니다. 데이터 Distiller 정적 제한에 대한 요약이 아래에 나열되어 있습니다. 자세한 내용은 쿼리 서비스 보호 문서를 참조하십시오.

* **일괄 쿼리**: 예약된 일괄 처리 쿼리가 24시간 후 시간 초과됩니다.
* **쿼리 서비스**: 다음 용도로 쿼리 서비스를 사용할 수 있습니다.
   * 데이터 분석을 위한 SQL 쿼리를 실행하고 수집 후 데이터 준비(정리, 셰이핑 및 조작)를 수행합니다.
   * SQL 쿼리를 실행하여 BI 도구에 직접 표시되는 롤업 지표를 만들려면.
   * Adobe Experience Platform 내의 데이터를 신속하게 검사합니다.
   * 데이터에서 의미 있는 통찰력을 생성하기 위해
* **보고 API 호출**: Reporting API를 사용하여 집계된 데이터에서 쿼리가 실행되도록 하려면 리소스가 충분히 있어야 효율적으로 실행할 수 있습니다. 여기에는 Real-time Customer Data Platform에서 제공하는 쿼리와 같은 기존 데이터 모델을 개선하는 쿼리가 포함됩니다. 보고 API는 각 쿼리에 동시 슬롯을 할당하여 리소스 사용률을 추적합니다. 최대 4개의 보고 API 호출을 동시에 사용할 수 있습니다. BI 도구를 통해 보고 API에 액세스하고 더 많은 동시 슬롯이 필요한 경우 BI 서버가 필요합니다.


