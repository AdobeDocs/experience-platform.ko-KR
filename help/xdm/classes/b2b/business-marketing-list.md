---
title: XDM 비즈니스 마케팅 목록 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 XDM 비즈니스 마케팅 목록 클래스에 대한 개요를 제공합니다.
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 마케팅 ] Listclass

>[!NOTE]
>
>이 클래스는 실시간 고객 데이터 플랫폼의 B2B 버전에 액세스할 수 있는 조직에서만 사용할 수 있습니다.

[!UICONTROL XDM 비즈니스 마케팅 ] 는 마케팅 목록의 최소 필수 속성을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다. 마케팅 목록을 사용하면 제품을 구매할 가능성이 가장 큰 잠재 고객을 우선 순위로 지정할 수 있습니다.

![](../../images/classes/b2b/business-marketing-list.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 외부 소스 시스템 감사 속성]](../../data-types/external-source-system-audit-attributes.md) | 마케팅 목록이 외부 소스 시스템에서 나온 경우 이 개체는 해당 시스템의 감사 속성을 캡처합니다. |
| `marketingListKey` | [[!UICONTROL B2B 소스]](../../data-types/b2b-source.md) | 마케팅 목록 엔티티에 대한 복합 식별자입니다. |
| `_id` | 문자열 | 레코드의 고유 식별자입니다. 이 값은 `marketingListID`과 별도의 시스템에서 생성한 값입니다. |
| `marketingListDescription` | 문자열 | 마케팅 목록에 대한 설명입니다. |
| `marketingListID` | 문자열 | 마케팅 목록 엔티티에 대한 고유 ID입니다. |
| `marketingListName` | 문자열 | 마케팅 목록의 이름입니다. |
