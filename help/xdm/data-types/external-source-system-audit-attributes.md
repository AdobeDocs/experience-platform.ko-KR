---
title: 외부 소스 시스템 감사 속성 데이터 유형
description: 이 문서에서는 외부 소스 시스템 감사 속성 XDM(Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: a7e6ebfe09566e6e027b13efc95dda97ff8f0315
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 15%

---

# [!UICONTROL 외부 소스 시스템 감사 속성] 데이터 유형

[!UICONTROL 외부 소스 시스템 감사 속성]은 외부 소스 시스템에 대한 감사 세부 정보를 캡처하는 표준 Experience Data Model(XDM) 데이터 유형입니다.

![](../images/data-types/external-source-system-audit-attributes.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B 소스]](./b2b-source.md) | 감사에 사용되는 소스의 합성 식별자. |
| `createdBy` | 문자열 | 이 레코드를 만든 사용자의 이름입니다. |
| `createdDate` | DateTime | 해당 레코드가 생성된 날짜입니다. |
| `externalID` | 문자열 | 소스에 대한 외부 고유 식별자. 이 값은 필요한 경우 식별 및 중복 제거에 도움이 됩니다. |
| `lastActivityDate` | DateTime | 소스 시스템의 마지막 활동 날짜입니다. |
| `lastReferencedDate` | DateTime | 소스 시스템에 대해 마지막으로 참조된 날짜입니다. |
| `lastUpdatedBy` | 문자열 | 이 레코드를 마지막으로 업데이트한 사람의 이름입니다. |
| `lastUpdatedDate` | DateTime | 소스 시스템의 마지막 업데이트 날짜. |
| `lastViewedDate` | DateTime | 소스 시스템의 마지막 조회 날짜입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
