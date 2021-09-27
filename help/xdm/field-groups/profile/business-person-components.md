---
title: XDM 비즈니스 개인 구성 요소 스키마 필드 그룹
description: 이 문서에서는 XDM 비즈니스 개인 구성 요소 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 319d508925d22e76a3d75ae473f6ea000b5c655b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 3%

---


# [!UICONTROL XDM 비즈니스 개인 구성 ] 요소스키마 필드 그룹

>[!NOTE]
>
>이 필드 그룹은 실시간 고객 데이터 플랫폼(실시간 CDP)의 B2B 버전에 액세스할 수 있는 조직에만 사용할 수 있습니다.

[!UICONTROL XDM 비즈니스 개인 구성 ] 요소는 개인 세분화에 필요한 여러 소스 레코드 및 기타 속성을 캡처하는  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 클래스에 대한 표준 스키마 필드 그룹을 나타냅니다.

실시간 CDP의 B2B 버전에서 [실시간 고객 프로필](../../../profile/home.md)을 통해 한 사용자에 대해 프로필이 작성되면 해당 프로필을 만드는 데 사용되는 정보가 여러 소스 레코드에서 제공될 수 있습니다. 예를 들어, 한 사람이 서로 다른 두 회사에 근무하는 경우, 많은 CRM 시스템에서 의도적으로 해당 사람의 복제 사본을 만들어 한 복사본이 회사 A에 연결되고 다른 한 복사본은 회사 B에 연결됩니다. 해당 데이터를 Adobe Experience Platform으로 가져올 때 이 필드 그룹을 사용하여 서로 다른 소스 레코드를 하나의 표현으로 병합합니다.

필드 그룹은 개체 배열인 루트 수준 `personComponents` 필드를 제공합니다. 배열에 있는 각 개체는 다른 소스 레코드를 나타냅니다.

![](../../images/field-groups/business-person-components.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인과 연관된 계정의 복합 식별자입니다. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 이 리드가 변환된 경우 관련 연락처에 대한 복합 식별자입니다. |
| `sourceExternalKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인 데이터가 발생한 소스 시스템의 복합 식별자입니다. |
| `sourcePersonKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 개인에 대한 복합 식별자입니다. |
| `workEmail` | [[!UICONTROL 이메일 주소]](../../data-types/b2b-source.md) | 사람의 회사 이메일 ID입니다. |
| `personGroupID` | 문자열 | 개인의 그룹 식별자입니다. |
| `personScore` | 문자열 | CRM 시스템에서 사용자에 대해 생성된 점수입니다. |
| `personSource` | 문자열 | 개인 데이터가 시작된 소스 시스템의 고유 문자열 기반 식별자입니다. |
| `personStatus` | 문자열 | 개인의 현재 마케팅 또는 판매 상태입니다. |
| `personType` | 문자열 | B2B 컨텍스트에서 개인 유형입니다. |
| `sourceAccountID` | 문자열 | 사용자와 연관된 소스 시스템의 계정에 대한 고유한 문자열 기반 식별자입니다. 이 필드는 이 사람이 근무하는 다른 회사를 찾기 위해 시스템에서 외래 키로 사용됩니다. |
| `sourceConvertedContactID` | 문자열 | 이 리드가 변환된 경우 관련 연락처에 대한 고유한 문자열 기반 식별자입니다. |
| `sourceExternalID` | 문자열 | 개인 데이터가 시작된 소스 시스템의 고유 문자열 기반 식별자입니다. |
| `sourcePersonID` | 문자열 | 개인에 대한 고유한 문자열 기반 식별자입니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
