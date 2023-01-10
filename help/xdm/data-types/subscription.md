---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;구독;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 구독 데이터 유형
description: 이 문서에서는 XDM(구독 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---

# [!UICONTROL 구독] 데이터 유형

[!UICONTROL 구독] 는 시간 또는 사용을 기반으로 하여 사용되는 소프트웨어, 서비스 또는 제품에 대한 라이선스 권한을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `device` | [[!UICONTROL 디바이스]](./device.md) | 구독에 연결된 장치에 대한 세부 사항을 설명합니다. |
| `environment` | [[!UICONTROL 환경]](./environment.md) | 이벤트 관찰이 발생한 주변 상황에 대한 정보를 포함하며, 특히 네트워크 또는 소프트웨어 버전과 같은 임시 정보를 자세히 설명합니다. |
| `subscriber` | [[!UICONTROL 사람]](./person.md) | 개별 개인을 설명합니다. 고객, 연락처 또는 소유자와 같은 다양한 역할을 수행하는 사람도 나타낼 수 있습니다. |
| `SKU` | 문자열 | 제품의 고유 식별자인 SKU(재고 관리 단위)입니다. |
| `billingPeriod` | 문자열 | 청구 사이의 기간입니다. |
| `billingStartDate` | 날짜 | 첫 번째 어음의 만기 일자입니다. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `category` | 문자열 | 이 유형의 구독에 대한 기본 최상위 분류입니다. |
| `chargeMethod` | 문자열 | 대금 청구가 고객에게 부과되도록 설정된 방식입니다. |
| `contractID` | 문자열 | 이 구독을 제어하는 계약에 대한 고유 ID입니다. |
| `country` | 문자열 | 구독 계약 및 계약 조건이 속한 국가입니다. |
| `endDate` | 날짜 | 현재 구독 기간이 끝나는 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `paymentMethod` | 문자열 | 반복 지급에 대한 결제 방법 |
| `paymentStatus` | 문자열 | 계산서의 지급 상태입니다. |
| `planName` | 문자열 | 사용자가 읽을 수 있는 구독의 이름입니다. |
| `reason` | 문자열 | 회원이 구독을 사용하기 위한 일반적인 의도 |
| `renew` | 문자열 | 최종 날짜 이후에 구독을 계속할 수 있는 합의된 방법입니다. |
| `revision` | 문자열 | 동일한 이름과 카테고리 계층 구조의 구독 간의 식별. |
| `startDate` | 날짜 | 구독이 시작되는 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `status` | 문자열 | 구독의 현재 상태입니다. |
| `subCategory` | 문자열 | 구독의 특정 하위 분류입니다. |
| `term` | 정수 | 구독 용어의 숫자 값입니다. |
| `termUnitOfTime` | 문자열 | 기간 시간 단위입니다. |
| `topUp` | 문자열 | 청구 기간 동안 가입의 소모성 측면을 다시 구매하는 방법에 대해 합의된 약관에 대해 설명합니다. |
| `type` | 문자열 | 구독이 적용되는 사람 수와 관련된 자격 범위. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
