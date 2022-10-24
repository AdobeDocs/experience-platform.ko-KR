---
title: 외부 소스 시스템 감사 속성 데이터 유형
description: 이 문서에서는 XDM(외부 소스 시스템 감사 속성 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 3%

---

# [!UICONTROL 외부 소스 시스템 감사 속성] 데이터 유형

>[!NOTE]
>
>이 데이터 유형은 Adobe Real-time Customer Data Platform의 B2B 버전에 액세스할 수 있는 조직에만 사용할 수 있습니다.

[!UICONTROL 외부 소스 시스템 감사 속성] 는 외부 소스 시스템에 대한 감사 세부 사항을 캡처하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

![](../images/data-types/external-source-system-audit-attributes.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B 소스]](./b2b-source.md) | 감사에 사용되는 소스의 복합 식별자입니다. |
| `createdBy` | 문자열 | 이 레코드를 만든 사용자의 이름입니다. |
| `createdDate` | DateTime | 이 레코드를 만든 날짜입니다. |
| `externalID` | 문자열 | 소스의 외부 고유 식별자입니다. 이 값은 필요한 경우 식별하고 중복 제거하는 데 사용됩니다. |
| `lastActivityDate` | DateTime | 소스 시스템의 마지막 활동 날짜입니다. |
| `lastReferencedDate` | DateTime | 소스 시스템의 마지막 참조 날짜입니다. |
| `lastUpdatedBy` | 문자열 | 이 레코드를 마지막으로 업데이트한 사람의 이름입니다. |
| `lastUpdatedDate` | DateTime | 소스 시스템에 대해 마지막으로 업데이트된 날짜입니다. |
| `lastViewedDate` | DateTime | 소스 시스템에 대해 마지막으로 본 날짜입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
