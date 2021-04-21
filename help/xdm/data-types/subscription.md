---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;구독;데이터 유형;데이터 유형;data-type;data type
solution: Experience Platform
title: 구독 데이터 유형
topic-legacy: overview
description: 이 문서에서는 XDM(Subscription Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 9%

---

# [!UICONTROL Subscription] 데이터 유형

[!UICONTROL Subscription] 는 시간 또는 사용을 기반으로 소프트웨어, 서비스 또는 제품에 대한 라이센스 권한을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | 구독에 연결된 장치에 대한 세부 사항을 설명합니다. |
| `environment` | [[!UICONTROL Environment]](./environment.md) | 특히 네트워크 또는 소프트웨어 버전과 같은 임시 정보를 자세히 설명하면서 이벤트 관찰이 발생한 주변 상황에 대한 정보를 포함합니다. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | 개별 사용자에 대해 설명합니다. 또한 고객, 담당자 또는 소유자와 같은 다양한 역할을 수행하는 사람을 나타낼 수 있습니다. |
| `SKU` | 문자열 | 제품의 고유 식별자인 SKU(재고 관리 단위). |
| `billingPeriod` | 문자열 | 청구 사이의 기간입니다. |
| `billingStartDate` | Date | 첫 번째 어음의 만기가 되는 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준을 따라야 합니다. |
| `category` | 문자열 | 이 유형의 구독에 대한 기본 최상위 분류입니다. |
| `chargeMethod` | 문자열 | 고객에게 요금을 부과하기 위한 결제 방식 |
| `contractID` | 문자열 | 이 구독을 관할하는 계약의 고유 ID. |
| `country` | 문자열 | 가입 계약 및 계약 조건이 뿌리 깊게 되어 있는 국가. |
| `endDate` | 날짜 | 현재 구독 기간이 끝나는 날짜. 날짜 형식(시간 없이)은 [RFC 3339, 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준을 따라야 합니다. |
| `paymentMethod` | 문자열 | 반복 지급에 대한 지불 방법. |
| `paymentStatus` | 문자열 | 계정의 지불 상태. |
| `planName` | 문자열 | 구독의 사람이 읽을 수 있는 이름입니다. |
| `reason` | 문자열 | 회원이 가입 사용에 대해 가지는 일반적인 의도. |
| `renew` | 문자열 | 종료일 이후에 구독을 계속할 수 있는 합의된 방법입니다. |
| `revision` | 문자열 | 동일한 이름과 카테고리 계층 구조 구독 간의 ID. |
| `startDate` | 날짜 | 구독이 시작된 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준을 따라야 합니다. |
| `status` | 문자열 | 구독의 현재 상태입니다. |
| `subCategory` | 문자열 | 가입의 특정 하위 분류. |
| `term` | 정수 | 구독 용어의 숫자 값입니다. |
| `termUnitOfTime` | 문자열 | 기간 단위의 시간. |
| `topUp` | 문자열 | 청구 기간 동안 가입의 소비자 측면 재구매 방법에 대해 합의된 조건을 설명합니다. |
| `type` | 문자열 | 구독으로 적용되는 사람 수와 관련된 권한 부여 범위. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
