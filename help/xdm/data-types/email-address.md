---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;이메일 주소;xdm:emailAddress;이메일 주소;데이터 유형;데이터 유형;
solution: Experience Platform
title: 이메일 주소 데이터 유형
topic-legacy: overview
description: 이 문서에서는 이메일 주소 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---

# [!UICONTROL 이메일 ] 주소 데이터 유형

[!UICONTROL 이메일 ] 주소는 이메일 주소의 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/email-address.png" width="450" /><br />

| 속성 | 설명 |
| --- | --- |
| `address` | RFC2822 및 후속 표준(예: `name@domain.com`)에 일반적으로 정의된 전자 메일의 기술 주소입니다. |
| `label` | 사용 가능한 추가 표시 정보. 예를 들어 전자 메일에 `John Smith smithjr@company.uk` 의 Microsoft Outlook 리치 주소가 표시된다면 `John Smith` 이 필드에 배치됩니다. |
| `primary` | 개인의 기본 이메일 주소인지 여부를 나타냅니다. 특정 시점에 프로필에 하나의 `primary` 이메일 주소만 있을 수 있습니다. |
| `status` | 전자 메일 주소를 현재 사용할 수 있는지 여부를 나타냅니다 |
| `statusReason` | 현재 `status`에 대한 설명입니다. |
| `type` | 계정이 사람과 관련된 방법(예: `work` 또는 `personal`). |

{style=&quot;table-layout:auto&quot;}


이메일 주소 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
