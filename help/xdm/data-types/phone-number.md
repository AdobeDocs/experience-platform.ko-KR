---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;phoneNumber;xdm:phoneNumber;data-type;data-type;data type
solution: Experience Platform
title: 전화 번호 데이터 유형
topic: overview
description: 이 문서에서는 전화 번호 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# [!UICONTROL 전화 ] 번호 데이터 유형

[!UICONTROL 전화 ] 번호는 전화 번호의 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 속성 | 설명 |
| --- | --- |
| `extension` | 개인 교환, 운영자 또는 스위치보드에서 전화하는 데 사용되는 내부 전화 번호입니다. |
| `number` | 전화 번호입니다. 전화 번호는 문자열이며 `()`, 하이픈 `-`, 또는 `1-353(0)18391111` 또는 `+613 9403600x1234` 등과 같은 하위 전화 거는 식별자를 나타내는 문자 등의 의미 있는 문자를 포함할 수 있습니다.`x` |
| `primary` | 개인의 기본 전화 번호인지 여부를 나타내는 부울 값입니다. 주소 또는 이메일 주소와 달리 여러 개의 기본 전화 번호가 있을 수 있습니다.통신 채널당 1개 통신 채널은 유형(상위 속성의 이름으로 표시됨)으로 정의됩니다.`textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` 및 `fax`. |
| `status` | 전화 번호를 현재 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 상태에 대한 설명입니다. |
| `validity` | 전화 번호의 기술적 정확도. |

전화 번호 데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)