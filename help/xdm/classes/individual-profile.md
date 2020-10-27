---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM 개별 프로필 클래스
topic: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 은 식별된 개인 및 부분적으로 식별된 개인의 특성과 이해에 대한 단일 표현(또는 &quot;프로필&quot;)을 구성하는 표준 XDM 클래스입니다.

프로필은 익명의 행동 신호(예: 브라우저 쿠키)부터 이름, 생년월일, 위치 및 이메일 주소와 같은 세부 정보가 포함된 식별된 프로필에 이르기까지 다양합니다. 프로파일의 규모가 커지면 개인 정보, ID, 연락처 세부 정보 및 개인 사용자를 위한 커뮤니케이션 환경 설정이 풍부한 강력한 저장소가 됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요를 참조하십시오](../home.md#data-behaviors).

클래스 자체에서는 데이터를 인제스트할 때 자동으로 채워지는 여러 개의 시스템 생성 값을 제공하는 반면, 다른 모든 필드는 [!DNL XDM Individual Profile] 호환 믹스인을 사용하여 추가해야 합니다 [](#mixins).

![](../images/classes/individual-profile.png)

| 속성 | 설명 |
| --- | --- |
| `_repo` | 다음 DateTime 필드를 [!UICONTROL 포함하는] 개체: <ul><li>`createDate`:데이터를 처음 인제스트한 시기 등 데이터 저장소에서 리소스를 만든 날짜 및 시간입니다.</li><li>`modifyDate`:리소스를 마지막으로 수정한 날짜 및 시간입니다.</li></ul> |
| `_id` | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고 데이터 중복을 방지하고 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다. 이 필드는 시스템에서 생성되므로 데이터 수집 중에 명시적 값을 제공해서는 안 됩니다.<br><br>이 필드는 개인 사용자와 관련된 ID가 **아니라** 데이터 자체의 기록을 나타낸다는 것을 구분하는 것이 중요합니다. 신분자료는 신분관계를 조건으로 해서 [신분관계로](../schema/composition.md#identity) 분류한다. |
| `createdByBatchID` | 레코드를 만든 인제스트된 일괄 처리 ID입니다. |
| `modifiedByBatchID` | 레코드가 업데이트되도록 한 마지막 인제스트된 일괄 처리 ID입니다. |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID. |

## 호환 가능한 믹싱 {#mixins}

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트에](../mixins/name-updates.md) 대한 문서를 참조하십시오.

Adobe은 [!DNL XDM Individual Profile] 클래스에 사용할 수 있는 여러 가지 표준 믹스를 제공합니다. 다음은 가장 일반적으로 클래스에 사용되는 혼합물 목록입니다.

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL 인구 통계 세부 사항]](../mixins/profile/person-details.md)
* [[!UICONTROL 개인 연락처 세부 정보]](../mixins/profile/personal-details.md)
* [[!UICONTROL 작업 연락처 세부 정보]](../mixins/profile/work-details.md)
* [[!UICONTROL 세그먼트 멤버십 세부 정보]](../mixins/profile/segmentation.md)