---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;스키마;XDM;개별 프로필;필드;스키마;ID맵;ID 맵;스키마 디자인;맵;결합 스키마;공용 스키마
solution: Experience Platform
title: XDM 개별 프로필 클래스
topic-legacy: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 81d96b629ce628f663a86701d8f076eb771fdf77
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 식별된 개인과 부분적으로 식별된 각 개인의 특성 및 이해에 대한 단일 표현(또는 &quot;프로필&quot;)을 구성하는 표준 XDM 클래스입니다.

프로필은 익명의 행동 신호(예: 브라우저 쿠키)부터 이름, 생년월일, 위치 및 이메일 주소와 같은 세부 정보가 포함된 식별된 프로필까지 다양합니다. 프로파일이 성장함에 따라 개인 정보, ID, 연락처 정보 및 커뮤니케이션 환경 설정이 포함된 강력한 저장소가 됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors)를 참조하십시오.

[!DNL XDM Individual Profile] 클래스 자체에서는 데이터를 인제스트할 때 자동으로 채워지는 여러 개의 시스템 생성 값을 제공하는 반면, 다른 모든 필드는 [호환 믹싱](#mixins)의 사용을 통해 추가해야 합니다.

![](../images/classes/individual-profile.png)

| 속성 | 설명 |
| --- | --- |
| `_repo` | 다음 [!UICONTROL DateTime] 필드를 포함하는 개체: <ul><li>`createDate`:데이터를 처음 인제스트한 시기 등 데이터 저장소에서 리소스가 만들어진 날짜 및 시간입니다.</li><li>`modifyDate`:리소스를 마지막으로 수정한 날짜 및 시간입니다.</li></ul> |
| `_id` | 레코드에 대한 고유 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고 데이터 중복을 방지하고 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 개별 개인 **과 관련된 ID를** 제공하지 않고 데이터 자체의 레코드를 구별하는 것이 중요합니다. 사람과 관련된 ID 데이터는 대신 [ID 필드](../schema/composition.md#identity)로 분류해야 합니다. |
| `createdByBatchID` | 레코드를 만든 인제스트된 일괄 처리의 ID. |
| `modifiedByBatchID` | 레코드를 업데이트하는 마지막 인제스트된 일괄 처리의 ID. |
| `personID` | 이 레코드가 관련된 개별 사람에 대한 고유 식별자입니다. 이 필드는 [ID 필드](../schema/composition.md#identity)로 지정되지 않는 한 사람과 관련된 ID를 나타낼 필요가 없습니다. |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID. |

## 호환 가능한 믹싱 {#mixins}

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트](../mixins/name-updates.md)에 있는 문서를 참조하십시오.

Adobe은 [!DNL XDM Individual Profile] 클래스에 사용할 수 있도록 여러 가지 표준 믹스를 제공합니다. 다음은 클래스에 일반적으로 사용되는 일부 믹싱 목록입니다.

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)

[!DNL XDM Individual Profile]에 대한 모든 호환 믹싱의 전체 목록은 [XDM GitHub 보고서](https://github.com/adobe/xdm/tree/master/components/mixins/profile)를 참조하십시오.