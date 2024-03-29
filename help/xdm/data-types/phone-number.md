---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;전화번호;xdm:phoneNumber;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 전화번호 데이터 유형
description: 전화번호 XDM 데이터 유형에 대해 알아봅니다.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# [!UICONTROL 전화 번호] 데이터 유형

[!UICONTROL 전화 번호] 는 전화번호에 대한 세부 정보를 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 속성 | 설명 |
| --- | --- |
| `extension` | 개인 교환, 운영자 또는 스위치보드 호출 시 사용되는 내부 전화번호. |
| `number` | 전화번호. 전화번호는 문자열이고 대괄호와 같은 의미 있는 문자를 포함할 수 있습니다 `()`, 하이픈 `-`, 또는 확장과 같은 서브다이얼 식별자를 보여 주는 문자 `x` 예를 들어, `1-353(0)18391111` 또는 `+613 9403600x1234`. |
| `primary` | 개인의 기본 전화 번호인지 여부를 나타내는 부울 값입니다. 주소 또는 이메일 주소와 달리 기본 전화번호는 여러 개일 수 있습니다(통신 채널당 하나). 통신 채널은 형식(상위 속성의 이름으로 표시됨)으로 정의됩니다. `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, 및 `fax`. |
| `status` | 현재 전화 번호를 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 상태에 대한 설명. |
| `validity` | 전화번호에 대한 기술적 수정 수준. |

{style="table-layout:auto"}

전화 번호 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
