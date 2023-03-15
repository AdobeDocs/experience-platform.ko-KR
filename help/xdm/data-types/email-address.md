---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;이메일 주소;xdm:emailAddress;이메일;이메일 주소;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 이메일 주소 데이터 유형
description: 이 문서에서는 이메일 주소 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!UICONTROL 이메일 주소] 데이터 유형

[!UICONTROL 이메일 주소] 이메일 주소의 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

<img src="../images/data-types/email-address.png" width="450" /><br />

| 속성 | 설명 |
| --- | --- |
| `address` | RFC2822 및 후속 표준에 정의된 이메일의 기술 주소(예: `name@domain.com`).<br><br>XDM에서 유효성 검사를 통과하려면 이메일 주소에 유효한 최상위 도메인을 포함해야 합니다. 다음을 참조하십시오 [문서](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) IANA(Internet Assigned Numbers Authority)에서 정의한 유효한 최상위 도메인의 전체 목록입니다. |
| `label` | 사용 가능한 추가 디스플레이 정보. 예를 들어 이메일에 다음과 같은 Microsoft Outlook 리치 주소 표시가 있는 경우 `John Smith smithjr@company.uk`, `John Smith` 이 필드에 배치됩니다. |
| `primary` | 개인의 기본 이메일 주소인지 여부를 나타냅니다. 프로필에는 하나만 있을 수 있습니다. `primary` 특정 시점의 이메일 주소. |
| `status` | 이메일 주소를 현재 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 항목에 대한 설명 `status`. |
| `type` | 계정과 사용자의 연계 방법(예: `work` 또는 `personal`). |

{style="table-layout:auto"}


이메일 주소 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
