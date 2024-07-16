---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;전화번호;xdm:phoneNumber;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 전화번호 데이터 유형
description: 전화번호 XDM 데이터 유형에 대해 알아봅니다.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 16%

---

# [!UICONTROL 전화 번호] 데이터 형식

[!UICONTROL 전화 번호]은(는) 전화 번호의 세부 정보를 설명하는 표준 XDM 데이터 형식입니다.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 속성 | 설명 |
| --- | --- |
| `extension` | 개인 교환, 연산자나 스위치보드 호출 시 시용되는 내부 전화번호. |
| `number` | 전화번호. 전화번호는 문자열이고 대괄호 `()`, 하이픈 `-`과(와) 같은 의미 있는 문자 또는 확장 `x`(예: `1-353(0)18391111` 또는 `+613 9403600x1234`)와 같은 서브다이얼 식별자를 보여 주는 문자를 포함할 수 있습니다. |
| `primary` | 개인의 기본 전화 번호인지 여부를 나타내는 부울 값입니다. 주소 또는 이메일 주소와 달리 기본 전화번호는 여러 개일 수 있습니다(통신 채널당 하나). 통신 채널은 `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` 및 `fax` 형식으로 정의됩니다. |
| `status` | 현재 전화 번호를 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 상태에 대한 설명. |
| `validity` | 전화번호에 대한 기술적 수정 수준. |

{style="table-layout:auto"}

전화 번호 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
