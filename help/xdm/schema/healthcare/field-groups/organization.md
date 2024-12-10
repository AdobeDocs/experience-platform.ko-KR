---
title: 조직 스키마 필드 그룹
description: 조직 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 6%

---

# [!UICONTROL 조직] 스키마 필드 그룹

[!UICONTROL 조직]은(는) [[!DNL XDM Individual Profile] 클래스](../../../classes/individual-profile.md) 및 [[!DNL Provider class]](../../../classes/provider.md)에 대한 표준 스키마 필드 그룹입니다. 공용 목적을 가진 사람 또는 조직의 그룹화에 대한 정보가 포함된 단일 개체 유형 필드 `healthcareOrganization`을(를) 제공합니다.

![필드 그룹 구조](../../../images/healthcare/field-groups/organization/organization.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| ---| --- | --- | --- |
| [!UICONTROL 연락처 정보] | `contact` | [[!UICONTROL 확장 연락처 세부 정보]](../data-types/extended-contact-detail.md) 배열 | 특정 조직에서 사용할 수 있는 통신 장치의 연락처 세부 정보. 여기에는 주소, 전화 번호, 팩스 번호, 모바일 번호, 이메일 주소 및 웹 사이트가 포함될 수 있습니다. |
| [!UICONTROL 끝점] | `endpoint` | [[!UICONTROL 참조]](../data-types/reference.md) 배열 | 조직을 위해 운영되는 서비스에 대한 액세스를 제공하는 기술 엔드포인트. |
| [!UICONTROL 식별자] | `indentifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 여러 개별 시스템에서 조직을 식별하는 데 사용되는 식별자입니다. |
| [!UICONTROL 조직의 일부] | `partOf` | [[!UICONTROL 참조]](../data-types/reference.md) | 이 조직이 속한 조직입니다. |
| [!UICONTROL 자격] | `qualification` | 오브젝트 배열 | 조직의 서비스 제공을 승인 및/또는 보증하는 공식 인증, 인증, 교육, 지정 및 라이선스. 자세한 내용은 아래 [섹션](#qualification)을 참조하세요. |
| [!UICONTROL 유형] | `type` | [[!UICONTROL 코드 가능한 개념 배열]](../data-types/codeable-concept.md) | 해당 조직의 종류. |
| [!UICONTROL 활성] | `active` | 부울 | 조직의 레코드가 여전히 활성 상태인지 여부. |
| [!UICONTROL 별칭] | `alias` | 문자열 배열 | 조직을 과거에 또는 라고 했던 대체 이름 목록입니다. |
| [!UICONTROL 설명] | `description` | 문자열 | 올바른 조직을 선택하도록 일반 컨텍스트를 제공하는 데 도움이 되는 조직에 대한 설명입니다. |
| [!UICONTROL 이름] | `name` | 문자열 | 조직과 연관된 이름입니다. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification`은(는) 개체 배열로 제공됩니다. 각 객체의 구조는 아래에 설명되어 있습니다.

![자격 구조](../../../images/healthcare/field-groups/organization/qualification.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 코드] | `code` | [[!UICONTROL 코드 가능한 개념]](../data-types/codeable-concept.md) | 자격의 코드화된 표현. |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../data-types/identifier.md) 배열 | 해당 조직의 해당 자격에 할당된 식별자. |
| [!UICONTROL 발급자] | `issuer` | [[!UICONTROL 참조]](../data-types/reference.md) | 자격을 규제하고 발급하는 조직. |
| [!UICONTROL 기간] | `period` | [[!UICONTROL 기간]](../data-types/period.md) | 자격이 유효한 기간. |
