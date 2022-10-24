---
title: XDM 비즈니스 개인 구성 요소 스키마 필드 그룹
description: 이 문서에서는 XDM 비즈니스 개인 구성 요소 스키마 필드 그룹에 대한 개요를 제공합니다.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# [!UICONTROL XDM 비즈니스 개인 구성 요소] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 개인 구성 요소] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md) 이 경우 한 사람에 대한 여러 소스 레코드 및 개인 세분화에 필요한 기타 속성을 캡처합니다.

을(를) 통해 사용자에 대한 프로필을 만들 때 [실시간 고객 프로필](../../../profile/home.md) Real-Time CDP B2B 버전에서 해당 프로필을 만드는 데 사용되는 정보는 여러 소스 레코드에서 제공될 수 있습니다. 예를 들어, 한 사람이 서로 다른 두 회사에 근무하는 경우, 많은 CRM 시스템에서 의도적으로 해당 사람의 복제 사본을 만들어 한 복사본이 회사 A에 연결되고 다른 한 복사본은 회사 B에 연결됩니다. 해당 데이터를 Adobe Experience Platform으로 가져올 때 이 필드 그룹을 사용하여 서로 다른 소스 레코드를 하나의 표현으로 병합합니다.

필드 그룹은 루트 수준을 제공합니다 `personComponents` 필드 - 객체 배열입니다. 배열에 있는 각 개체는 다른 소스 레코드를 나타냅니다.

>[!IMPORTANT]
>
>에 설명된 대로 수집 패턴을 따라야 합니다. [소스 설명서](../../../rtcdp/sources/b2b.md). 다른 필드 매핑 방법은 작동하지 않을 수 있습니다.
>
>예를 들어 `personComponents` 배열은 표준 수집 패턴 동안 개별적으로 제출된 다음 플랫폼별로 배열에 추가됩니다. 객체 배열을 비즈니스 개인 구성 요소에 수동으로 추가하면 오류가 반환됩니다.
>B2B 데이터에 대한 스키마를 생성할 때 자동 생성 유틸리티를 사용해야 합니다. 사용 방법에 대한 지침은 설명서를 참조하십시오 [B2B 네임스페이스 및 스키마 자동 생성 유틸리티](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). 자동 생성 유틸리티를 사용하지 않고 데이터 모델을 수동으로 매핑하려면 [Adobe Real-time Customer Data Platform B2B Edition XDM 클래스](../../../rtcdp/schemas/b2b.md) 데이터를 매핑하기 전에
>
>자세한 내용은 [엔드 투 엔드 자습서](../../../rtcdp/b2b-tutorial.md) 를 참조하십시오.

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
