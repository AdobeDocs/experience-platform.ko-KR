---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Attribution AI에서 시작하기
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Attribution AI에서 시작하기

다음 가이드는 Attribution AI 사용과 관련된 다양한 Adobe Experience Platform 서비스를 이해해야 합니다. 자습서를 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../xdm/home.md):XDM은 Adobe Experience Cloud가 Adobe Experience Platform을 기반으로 정확한 타이밍에 적합한 고객에게 올바른 메시지를 전달할 수 있는 기본 프레임워크입니다. XDM System은 경험 플랫폼을 구축하는 방법론을 통해 경험 데이터 모델 스키마를 플랫폼 서비스에서 사용할 수 있도록 운영했습니다.
- [스키마 컴포지션의](../../xdm/schema/composition.md)기본 사항:이 문서에서는 XDM(Experience Data Model) 스키마와 Adobe Experience Platform에서 사용할 스키마를 작성하기 위한 기본 요소, 원칙 및 모범 사례에 대해 소개합니다.
- [스키마 작성](../../xdm/tutorials/create-schema-ui.md):이 자습서에서는 경험 플랫폼 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.

기여도 AI를 사용하려면 데이터 세트가 XDM(Experience Data Model)의 혼합인 CEE(Consumer Experience Events) [스키마를 따르도록](../../xdm/home.md) 해야 합니다. 이 데이터를 구현하거나 변경하려면 Adobe 지원 센터(attributionai-support@adobe.com)에 문의하십시오. 미디어 지출 데이터가 있는 경우 매출 및 ROI와 같은 추가 분석을 수행할 수 있습니다. 고객 프로파일 데이터를 사용할 수 있는 경우, 크레딧을 고객 프로파일 수준에 추가로 적용할 수 있습니다.

## 용어

- **전환 이벤트:** 고객이 컨퍼런스 등록과 같이 목표를 향해 이정표를 나타내기 위해 수행하는 모든 디지털 이벤트 또는 디지털 인터랙션 추가 예로는 유료 전환, 무료 계정 등록 또는 트레이트 자격이 있습니다.

- **터치포인트:** 고객이 목표를 향해 가는 과정에서 수행하는 모든 디지털 이벤트 또는 디지털 인터랙션 구매 전 관련 마케팅 활동, 본 광고 노출 수 및 유료 검색 클릭이 그 예입니다.

## 점수 액세스 및 쿼리

>[!NOTE] 원시 점수를 쿼리하거나 액세스할 필요가 없는 경우 이 단계를 건너뛰고 [사용자 인터페이스 안내서로](./user-guide.md)진행할 수 있습니다.

기여도 AI에 대한 점수에 액세스 및 쿼리는 Snowflake를 통해 수행됩니다. 현재, Snowflake에 대한 자격 증명을 설정 및 수신하거나 Raw 데이터를 대량으로 내보내려면 attributionai-support@adobe.com에서 Adobe 지원을 이메일로 보내야 합니다.

Adobe 지원이 요청을 처리하면 Snowflake에 대한 Reader 계정 및 아래 해당 자격 증명에 대한 URL이 제공됩니다.

- 눈송이 URL
- 사용자 이름
- 암호

## 다음 단계

모든 자격 증명과 스키마를 준비했으면 Attribution AI [사용자 인터페이스 가이드를](./user-guide.md)따라 시작하십시오. 이 안내서에서는 인스턴스를 만들고 이를 교육 및 점수 책정용으로 제출하는 과정을 안내합니다.