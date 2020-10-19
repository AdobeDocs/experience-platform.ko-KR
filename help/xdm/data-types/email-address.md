---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: 이메일 주소 데이터 유형
topic: overview
description: 이 문서에서는 이메일 주소 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---


# [!UICONTROL 이메일 주소] 데이터 유형

[!UICONTROL 이메일 주소] 는 이메일 주소의 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/email-address.png" width="450" /><br />

| 속성 | 설명 |
| --- | --- |
| `address` | RFC2822 및 후속 표준(예:)에 일반적으로 정의된 이메일의 기술 `name@domain.com`주소입니다. |
| `label` | 사용 가능한 추가 표시 정보. 예를 들어, 이메일에 Microsoft Outlook의 리치 주소 표시 `John Smith smithjr@company.uk`가 있는 경우 이 필드에 `John Smith` 배치됩니다. |
| `primary` | 개인의 기본 이메일 주소인지 여부를 나타냅니다. 특정 시점에 프로필에는 하나의 `primary` 이메일 주소만 있을 수 있습니다. |
| `status` | 이메일 주소를 현재 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 설명 `status`. |
| `type` | 계정과 사람(예: `work` 또는 `personal`)의 관계. |


이메일 주소 데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)