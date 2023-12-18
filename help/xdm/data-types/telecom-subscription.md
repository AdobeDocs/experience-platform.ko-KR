---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;통신;구독;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 통신 구독 데이터 유형
description: 통신 구독 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 7%

---

# [!UICONTROL 통신 구독] 데이터 유형

[!UICONTROL 통신 구독] 는 인터넷, 모바일, 미디어 또는 유선전화와 같은 특정 통신 구독 유형에 대한 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

>[!NOTE]
>
>이 문서에서는 데이터 유형에 대해 설명합니다. 같은 이름의 필드 그룹에 대해서는 [[!UICONTROL 통신 구독] 필드 그룹 참조 안내서](../field-groups/profile/telecom-subscription.md).
>
>통신 산업과 관련이 없는 구독 유형을 설명하는 경우에는 원본을 사용하십시오 [[!UICONTROL 구독] 데이터 유형](./subscription.md) 대신,

![통신 구독 구조](../images/data-types/telecom-subscription/structure.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `devices` | 오브젝트 배열 | 플랜과 연결된 장치 및/또는 액세서리 목록을 설명합니다. 다음을 참조하십시오. [아래 섹션](#devices) 각 배열 항목의 예상 구조에 대한 자세한 내용을 보려면 여기를 클릭하십시오. |
| `subscriber` | [[!UICONTROL 개인]](./person.md) | 구독 소유자를 설명합니다. |
| `ID` | 문자열 | 구독 인스턴스에 대한 고유 식별자. |
| `billingPeriod` | 문자열 | 청구 기간. |
| `billingStartDate` | 날짜 | 청구 기간 시작일. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `chargeMethod` | 문자열 | 고객에게 비용을 청구하기 위해 결제를 설정하는 방법. |
| `contractID` | 문자열 | 해당 구독을 관리하는 계약에 대한 고유 ID. |
| `country` | 문자열 | 구독 계약 및 계약 조건의 기반이 되는 국가. |
| `endDate` | 날짜 | 현재 구독 약관이 종료되는 날짜. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `paymentDueDate` | 날짜 | 구독 결제일. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `paymentMethod` | 문자열 | 자동연장 결제 방법. |
| `paymentStatus` | 문자열 | 계정의 지불 상태. |
| `planName` | 문자열 | 사람이 인식할 수 있는 구독 이름. |
| `reason` | 문자열 | 구독 사용에 대한 일반적인 멤버 의도. |
| `renew` | 문자열 | 종료일 이후 구독이 지속될 수 있는 방식에 동의. |
| `startDate` | 날짜 | 구독 시작일. 날짜 형식(시간 없음)은 [RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) 표준. |
| `status` | 문자열 | 현재 구독 상태. |
| `subscriptionCategory` | 문자열 | 이러한 유형의 구독을 최상위 수준으로 분류. |
| `subscriptionSKU` | 문자열 | 구독을 위한 SKU(Stock Keeping Unit). |
| `subscriptionSubCategory` | 문자열 | 구독의 특정 하위 범주화. |
| `term` | 정수 | 구독 용어의 숫자 값입니다. |
| `termUnitOfTime` | 문자열 | 약관 기간에 대한 시간 단위. |
| `topUp` | 문자열 | 결제 기간 동안 소모성 구독을 재구매하는 방법에 대해 합의된 약관을 설명합니다. |
| `type` | 문자열 | 구독이 적용되는 인원 수와 관련된 권한 범위. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` 는 개체의 배열이며, 각 개체는 구독과 관련된 장치 또는 액세서리를 설명합니다.

![디바이스 배열 구조](../images/data-types/telecom-subscription/devices.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `deviceFees` | 오브젝트 | 라우터, 모뎀 및 수신기 등의 항목에 대한 장치 요금을 캡처하는 개체입니다. 필요한 속성은 다음과 같습니다.<ul><li>`amount`: 다음으로 표시되는 통화 금액 `currencyCode`.</li><li>`conversionDate`: 통화 전환이 이루어진 날짜입니다.</li><li>`currencyCode`: [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 통화 코드 `amount`.</li></ul> |
| `ID` | 문자열 | 장치의 고유 ID입니다. |
| `OS` | 문자열 | 장치 운영 체제입니다. |
| `deviceInsurance` | 문자열 | 고객이 이 장치에 대한 보험을 옵트인했는지 여부를 나타냅니다. |
| `manufacturer` | 문자열 | 장치 제조업체. |
| `name` | 문자열 | 장치의 이름입니다. |
| `paymentOptions` | 문자열 | 디바이스를 할부로 결제할지 또는 소매가로 결제할지 여부를 나타냅니다. |
| `serialNumber` | 문자열 | 장치 일련 번호입니다. |
| `status` | 문자열 | 장치 상태. |
| `storageCapacity` | 문자열 | 디바이스 스토리지 용량입니다. |
| `type` | 문자열 | 디바이스 유형. |

{style="table-layout:auto"}
