---
title: XDM 비즈니스 사용자 구성 요소 스키마 필드 그룹
description: XDM 비즈니스 사용자 구성 요소 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# [!UICONTROL XDM 비즈니스 사용자 구성 요소] 스키마 필드 그룹

[!UICONTROL XDM 비즈니스 사용자 구성 요소]는 사용자에 대한 여러 소스 레코드와 사용자 세분화에 필요한 기타 특성을 캡처하는 [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md)에 대한 표준 스키마 필드 그룹입니다.

Real-Time CDP의 B2B edition에서 [실시간 고객 프로필](../../../profile/home.md)을 통해 사용자에 대한 프로필을 만드는 경우 해당 프로필을 만드는 데 사용되는 정보는 여러 소스 레코드에서 제공될 수 있습니다. 예를 들어 한 사람이 두 개의 다른 회사에 근무하는 경우 많은 CRM 시스템에서 의도적으로 해당 사람의 복사본을 만들어 한 복사본은 회사 A에 연결되고 다른 복사본은 회사 B에 연결됩니다. 해당 데이터를 Adobe Experience Platform으로 가져올 때 이 필드 그룹을 사용하여 서로 다른 소스 레코드를 단일 표현으로 병합합니다.

필드 그룹은 개체 배열인 루트 수준 `personComponents` 필드를 제공합니다. 배열의 각 개체는 다른 소스 레코드를 나타냅니다.

>[!IMPORTANT]
>
>[소스 설명서](../../../rtcdp/sources/b2b.md)에 설명된 대로 수집 패턴을 따라야 합니다. 다른 필드 매핑 방법은 작동하지 않을 수 있습니다.
>
>예를 들어, 표준 수집 패턴 동안 `personComponents` 배열의 각 개체가 개별적으로 제출된 다음 Experience Platform에서 배열에 추가됩니다. 비즈니스 사용자 구성 요소에 수동으로 개체 배열을 추가하면 오류가 반환됩니다.
>B2B 데이터에 대한 스키마를 생성할 때 자동 생성 유틸리티를 사용해야 합니다. [B2B 네임스페이스 및 스키마 자동 생성 유틸리티](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)를 사용하는 방법에 대한 지침은 설명서를 참조하십시오. 자동 생성 유틸리티를 사용하지 않고 데이터 모델을 수동으로 매핑하려면 데이터를 매핑하기 전에 [Adobe Real-Time Customer Data Platform B2B edition XDM 클래스](../../../rtcdp/schemas/b2b.md)에 대한 설명서를 읽어 보십시오.
>
>B2B 데이터의 권장 워크플로에 대한 자세한 내용은 [전체 튜토리얼](../../../rtcdp/b2b-tutorial.md)을 참조하세요.

![](../../images/field-groups/business-person-components.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 사용자와 연계된 계정에 대한 합성 식별자. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 해당 잠재 고객이 전환된 경우 관련 연락처에 대한 복합 식별자. |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 사용자 데이터가 시작된 소스 시스템의 복합 식별자. |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 개인용 복합 식별자. |
| `workEmail` | [[!UICONTROL 전자 메일 주소]](../../data-types/b2b-source.md) | 개인용 회사 이메일 ID. |
| `personGroupID` | 문자열 | 개인용 그룹 식별자. |
| `personScore` | 문자열 | CRM 시스템에서 생성된 개인용 스코어. |
| `personSource` | 문자열 | 사용자 데이터가 시작된 소스 시스템에 대한 고유한 문자열 기반 식별자입니다. |
| `personStatus` | 문자열 | 개인의 현재 마케팅 또는 판매 상태. |
| `personType` | 문자열 | B2B 컨텍스트의 개인 유형. |
| `sourceAccountID` | 문자열 | 사용자와 연계된 소스 시스템 내 계정에 대한 고유한 문자열 기반 식별자. 이 필드는 시스템에서 이 사용자가 근무하는 다른 회사를 조회하기 위한 외래 키로 사용됩니다. |
| `sourceConvertedContactID` | 문자열 | 잠재 고객이 전환된 경우 관련 연락처에 대한 고유 문자열 기반 식별자. |
| `sourceExternalID` | 문자열 | 개인 데이터의 출처가 되는 소스 시스템에 대한 고유한 문자열 기반 식별자입니다. |
| `sourcePersonID` | 문자열 | 사용자에 대한 고유한 문자열 기반 식별자. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
