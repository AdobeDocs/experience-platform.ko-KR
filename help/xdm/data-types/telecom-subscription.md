---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;통신;가입;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 통신 구독 데이터 유형
description: 이 문서에서는 XDM(Telecom Subscription Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 10%

---

# [!UICONTROL 통신 구독] 데이터 유형

[!UICONTROL 통신 구독] 는 인터넷, 모바일, 미디어 또는 유선선과 같은 특정 통신 구독 유형에 대한 세부 사항을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

>[!NOTE]
>
>이 문서에서는 데이터 유형을 설명합니다. 같은 이름의 필드 그룹에 대해서는 [[!UICONTROL 통신 구독] 필드 그룹 참조 안내서](../field-groups/profile/telecom-subscription.md).
>
>통신 산업과 관련이 없는 구독 유형을 설명하는 경우 일반 을 사용하십시오 [[!UICONTROL 구독] 데이터 유형](./subscription.md) 을 가리키도록 업데이트하는 것이 좋습니다.

![통신 가입 구조](../images/data-types/telecom-subscription/structure.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `devices` | 개체 배열 | 계획과 연관된 장치 및/또는 액세서리 목록을 설명합니다. 자세한 내용은 [아래 섹션](#devices) 각 배열 항목의 예상 구조에 대한 자세한 내용을 참조하십시오. |
| `subscriber` | [[!UICONTROL 사람]](./person.md) | 구독 소유자를 설명합니다. |
| `ID` | 문자열 | 구독 인스턴스에 대한 고유 식별자입니다. |
| `billingPeriod` | 문자열 | 청구 사이의 기간입니다. |
| `billingStartDate` | 날짜 | 청구 기간이 시작되는 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `chargeMethod` | 문자열 | 대금 청구가 고객에게 부과되도록 설정된 방식입니다. |
| `contractID` | 문자열 | 이 구독을 제어하는 계약에 대한 고유 ID입니다. |
| `country` | 문자열 | 구독 계약 및 계약 조건이 속한 국가입니다. |
| `endDate` | 날짜 | 현재 구독 기간이 끝나는 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `paymentDueDate` | 날짜 | 구독 지급 마감일. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `paymentMethod` | 문자열 | 반복 지급에 대한 결제 방법 |
| `paymentStatus` | 문자열 | 계산서의 지급 상태입니다. |
| `planName` | 문자열 | 사용자가 읽을 수 있는 구독의 이름입니다. |
| `reason` | 문자열 | 회원이 구독을 사용하기 위한 일반적인 의도 |
| `renew` | 문자열 | 최종 날짜 이후에 구독을 계속할 수 있는 합의된 방법입니다. |
| `startDate` | 날짜 | 구독이 시작되는 날짜입니다. 날짜 형식(시간 없이)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `status` | 문자열 | 구독의 현재 상태입니다. |
| `subscriptionCategory` | 문자열 | 이 유형의 구독에 대한 기본 최상위 분류입니다. |
| `subscriptionSKU` | 문자열 | 구독에 대한 SKU(재고 유지 단위)입니다. |
| `subscriptionSubCategory` | 문자열 | 구독의 특정 하위 분류입니다. |
| `term` | 정수 | 구독 용어의 숫자 값입니다. |
| `termUnitOfTime` | 문자열 | 기간 시간 단위입니다. |
| `topUp` | 문자열 | 청구 기간 동안 가입의 소모성 측면을 다시 구매하는 방법에 대해 합의된 약관에 대해 설명합니다. |
| `type` | 문자열 | 구독이 적용되는 사람 수와 관련된 자격 범위. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` 는 구독과 연결된 장치 또는 액세서리를 각 개체에서 설명하는 개체 배열입니다.

![디바이스 어레이 구조](../images/data-types/telecom-subscription/devices.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `deviceFees` | 오브젝트 | 라우터, 모뎀 및 수신기와 같은 항목에 대한 장치 비용을 캡처하는 객체입니다. 다음 속성이 필요합니다.<ul><li>`amount`: 으로 표시되는 통화 금액입니다. `currencyCode`.</li><li>`conversionDate`: 통화 전환이 수행된 날짜입니다.</li><li>`currencyCode`: 다음 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 에 대한 통화 코드 `amount`.</li></ul> |
| `ID` | 문자열 | 장치의 고유 ID입니다. |
| `OS` | 문자열 | 장치 운영 체제입니다. |
| `deviceInsurance` | 문자열 | 고객이 이 장치의 보험에 가입했는지 여부를 나타냅니다. |
| `manufacturer` | 문자열 | 장치 제조업체입니다. |
| `name` | 문자열 | 장치의 이름입니다. |
| `paymentOptions` | 문자열 | 장치가 할부로 지급될지 또는 전체 소매 가격으로 지급되는지를 나타냅니다. |
| `serialNumber` | 문자열 | 장치 일련 번호입니다. |
| `status` | 문자열 | 장치 상태입니다. |
| `storageCapacity` | 문자열 | 디바이스 스토리지 용량 |
| `type` | 문자열 | 장치 유형입니다. |

{style=&quot;table-layout:auto&quot;}
