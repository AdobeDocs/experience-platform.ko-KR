---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;구독;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 구독 데이터 유형
description: 구독 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 28%

---

# [!UICONTROL 구독] 데이터 형식

[!UICONTROL 구독]은(는) 시간이나 사용에 따라 사용되는 소프트웨어, 서비스 또는 제품에 대해 라이선스가 부여된 권한을 설명하는 표준 XDM(Experience Data Model) 데이터 형식입니다.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `device` | [[!UICONTROL 장치]](./device.md) | 구독과 연결된 장치에 대한 세부 정보를 설명합니다. |
| `environment` | [[!UICONTROL 환경]](./environment.md) | 이벤트 관찰 시 주변에서 발생한 임시 상황에 대한 세부 정보(예: 네트워크 또는 소프트웨어 버전)를 포함합니다. |
| `subscriber` | [[!UICONTROL 사용자]](./person.md) | 개별 개인을 설명합니다. 고객, 연락처 또는 소유자 등 다양한 역할을 수행하는 사람을 나타낼 수도 있습니다. |
| `SKU` | 문자열 | 제품에 대한 고유 식별자인 SKU(Stock Keeping Unit). |
| `billingPeriod` | 문자열 | 청구 기간. |
| `billingStartDate` | 날짜 | 첫 번째 청구서 기한일. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준을 따라야 합니다. |
| `category` | 문자열 | 이러한 유형의 구독을 최상위 수준으로 분류. |
| `chargeMethod` | 문자열 | 고객에게 비용을 청구하기 위해 결제를 설정하는 방법. |
| `contractID` | 문자열 | 해당 구독을 관리하는 계약에 대한 고유 ID. |
| `country` | 문자열 | 구독 계약과 계약 조건의 기반이 되는 국가. |
| `endDate` | 날짜 | 현재 구독 약관이 종료되는 날짜. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준을 따라야 합니다. |
| `paymentMethod` | 문자열 | 자동연장 결제 방법 |
| `paymentStatus` | 문자열 | 계정의 지불 상태. |
| `planName` | 문자열 | 사람이 인식할 수 있는 구독 이름. |
| `reason` | 문자열 | 구독 사용에 대한 일반적인 멤버 의도. |
| `renew` | 문자열 | 종료일 이후 구독이 계속 지속될 수 있는 방식에 동의. |
| `revision` | 문자열 | 동일한 이름을 가진 구독과 범주 계층 사이를 식별. |
| `startDate` | 날짜 | 구독 시작일. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준을 따라야 합니다. |
| `status` | 문자열 | 현재 구독 상태. |
| `subCategory` | 문자열 | 구독의 특정 하위 범주화. |
| `term` | 정수 | 구독 용어의 숫자 값입니다. |
| `termUnitOfTime` | 문자열 | 약관 기간에 대한 시간 단위. |
| `topUp` | 문자열 | 결제 기간 동안 소모성 구독을 재구매하는 방법에 대해 합의된 약관을 설명합니다. |
| `type` | 문자열 | 구독의 적용을 받는 인원 수와 관련된 권한 범위. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
