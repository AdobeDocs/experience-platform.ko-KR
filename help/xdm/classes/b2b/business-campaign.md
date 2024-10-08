---
title: XDM 비즈니스 캠페인 클래스
description: 경험 데이터 모델(XDM)의 XDM 비즈니스 캠페인 클래스에 대해 알아봅니다.
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL XDM 비즈니스 캠페인] 클래스

>[!IMPORTANT]
>
>이 클래스는 [Adobe Real-time Customer Data Platform B2B 에디션](../../../rtcdp/b2b-overview.md)에 액세스할 수 있는 조직에서 사용하기 위한 것입니다. 이 클래스가 [실시간 고객 프로필](../../../profile/home.md)에 참여하려면 Real-Time CDP B2B 에디션에 액세스할 수 있어야 합니다.

[!UICONTROL XDM 비즈니스 캠페인]은(는) 비즈니스 캠페인의 최소 필요 속성을 캡처하는 표준 경험 데이터 모델(XDM) 클래스입니다.

![UI에 표시되는 XDM 비즈니스 캠페인 클래스의 구조](../../images/classes/b2b/business-campaign.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 캠페인 엔티티에 대한 복합 식별자. |
| `extSourceSystemAudit` | [[!UICONTROL 외부 Source 시스템 감사 특성]](../../data-types/external-source-system-audit-attributes.md) | 캠페인이 외부 소스 시스템에서 온 경우 이 객체는 해당 시스템에 대한 감사 속성을 캡처합니다. |
| `_id` | 문자열 | 레코드에 대한 고유 식별자. `campaignID`과(와) 별개인 시스템 생성 값입니다. |
| `campaignDescription` | 문자열 | 캠페인에 대한 설명. |
| `campaignID` | 문자열 | 캠페인 엔티티에 대한 고유 식별자. |
| `campaignName` | 문자열 | 캠페인의 이름입니다. |
| `campaignType` | 문자열 | 캠페인 유형 또는 타겟 대상자. |

{style="table-layout:auto"}

이 클래스가 다른 B2B 클래스와 개념적으로 관련되는 방법 및 Adobe Experience Platform UI에서 이러한 관계를 설정하는 방법에 대해 알아보려면 [Real-Time CDP B2B 에디션의 스키마 관계](../../tutorials/relationship-b2b.md)에 대한 안내서를 참조하십시오.

이 클래스와 호환되는 추가 필드의 경우 [[!UICONTROL XDM 비즈니스 캠페인 세부 정보]](../../field-groups/b2b-campaign/details.md)에 대한 필드 그룹 참조를 참조하십시오.
