---
title: 위치 스키마 필드 그룹
description: 위치 스키마 필드 그룹에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---

# [!UICONTROL 위치] 스키마 필드 그룹

[!UICONTROL Location]은(는) [[!DNL Location] 클래스](../../classes/location.md)의 표준 스키마 필드 그룹입니다. 위치에 대한 세부 정보 및 위치 정보를 캡처하는 단일 개체 유형 필드 `healthcareLocation`을(를) 제공합니다.

![필드 그룹 구조](../../images/field-groups/location.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 주소] | `address` | [[!UICONTROL 주소]](../../data-types/healthcare/address.md) | 실제 위치의 주소입니다. |
| [!UICONTROL 특성] | `characteristic` | [[!UICONTROL 코드 가능한 개념 배열]](../../data-types/healthcare/codeable-concept.md) | 위치 특성 컬렉션입니다. |
| [!UICONTROL 연락처] | `contact` | [[!UICONTROL 확장 연락처 세부 정보]](../../data-types/healthcare/extended-contact-detail.md) 배열 | 위치에 대한 연락처 세부 정보. |
| [!UICONTROL 끝점] | `endpoint` | [[!UICONTROL 참조]](../../data-types/healthcare/reference.md) 배열 | 위치에 대한 운영 서비스에 대한 액세스를 제공하는 기술 종단점입니다. |
| [!UICONTROL 양식] | `form` | [[!UICONTROL 코드 가능한 개념]](../../data-types/healthcare/codeable-concept.md) | 위치의 물리적 형식입니다. |
| [!UICONTROL 작업 시간] | `hoursOfOperation` | [[!UICONTROL 가용성]](../../data-types/healthcare/availability.md) 배열 | 일반적으로 이 위치가 열려 있는 일 및 시간(예외 포함). |
| [!UICONTROL 식별자] | `identifier` | [[!UICONTROL 식별자]](../../data-types/healthcare/identifier.md) 배열 | 위치를 식별하는 고유 코드 또는 번호입니다. |
| [!UICONTROL 조직 관리] | `managingOrganization` | [[!UICONTROL 참조]](../../data-types/healthcare/reference.md) | 프로비저닝 및 유지 관리를 담당하는 조직입니다. |
| [!UICONTROL 작동 상태] | `operationalStatus` | [[!UICONTROL 코딩]](../../data-types/healthcare/coding.md) | 위치에 대한 작동 상태입니다. |
| [!UICONTROL 위치의 일부] | `partOf` | [[!UICONTROL 참조]](../../data-types/healthcare/reference.md) | 이 위치가 속한 위치입니다. |
| [!UICONTROL 위치] | `position` | 오브젝트 | 절대 지리적 위치. Double 형식의 세 가지 속성을 포함합니다. <li>`longitude`: WGS84 데이터 기반의 경도</li> <li>`latitude`: WGS84 데이텀이 있는 위도.</li> <li>`altitude`: WGS84 데이텀이 있는 고도.</li> |
| [!UICONTROL 유형] | `type` | [[!UICONTROL 코드 가능한 개념 배열]](../../data-types/healthcare/codeable-concept.md) | 해당 위치에서 수행되는 함수 유형입니다. |
| [!UICONTROL 가상 서비스] | `virtualService` | [[!UICONTROL 가상 서비스 세부 정보]](../../data-types/healthcare/virtual-service-detail.md) 배열 | 가상 서비스의 연결 세부 정보. |
| [!UICONTROL 별칭] | `alias` | 문자열 배열 | 위치가 이거나 알려진 대체 이름 목록입니다. |
| [!UICONTROL 설명] | `description` | 문자열 | 이름 이외의 위치를 식별하는 추가 정보입니다. |
| [!UICONTROL 모드] | `mode` | 문자열 | 위치 모드입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL 이름] | `name` | 문자열 | 위치의 이름입니다. |
| [!UICONTROL 상태] | `status` | 문자열 | 위치의 상태입니다. 이 속성의 값은 다음 알려진 열거형 값 중 하나와 같아야 합니다. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
