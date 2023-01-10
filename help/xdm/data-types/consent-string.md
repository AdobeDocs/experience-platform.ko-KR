---
solution: Experience Platform
title: 동의 문자열 데이터 유형
description: 이 문서에서는 동의 문자열 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# [!UICONTROL 동의 문자열] 데이터 유형

[!UICONTROL 동의 문자열] 는 고객의 동의를 나타내는 문자열 값을 설명하는 표준 XDM 데이터 유형입니다. 여기에는 동의 문자열(예: [IAB TCF(Transparency and Consent Framework) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `consentStandard` | 문자열 | 동의 문자열에 대한 표준입니다. 이것은 동의 관리 서비스에서 설정한 동의 문자열 형식을 결정하는 데 도움이 됩니다. |
| `consentStandardVersion` | 문자열 | 동의 관리 서비스에서 설정한 동의 문자열 형식을 정확하게 정의하는 데 사용되는 동의 표준의 버전입니다. |
| `consentStringValue` | 문자열 | 동의 관리 서비스에서 제공한 전체 동의 문자열입니다. `consentStandard` 및 `consentStandardVersion` 이 문자열을 구문 분석하는 방법을 정의하는 데 도움이 됩니다. |
| `containsPersonalData` | 부울 | 이 필드가 true면 동의 집행을 위해 이 동의 문자열을 처리해야 합니다. |
| `gdprApplies` | 부울 | 이 필드가 true면 동의가 개인 데이터와 함께 오는 것입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
