---
solution: Experience Platform
title: 세그먼트 정의 클래스
topic: overview
description: 이 문서에서는 XDM(경험 데이터 모델)의 세그먼트 정의 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f4e80cc6a5e5e135bedb77b2d56ae5cb2c8d8c53
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot;은 세그먼트 정의의 세부 사항을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다. 이 클래스에는 다른 선택적 속성과 함께 세그먼트의 ID 및 이름과 같은 필수 필드가 포함됩니다. 외부 시스템에서 Adobe Experience Platform으로 세그먼트 정의를 가져오는 경우 이 클래스를 사용해야 합니다.

>[!NOTE]
>
>이 클래스는 세그먼트 정의 자체에 대한 정보를 캡처하는 데에만 사용해야 합니다. 프로필 데이터 내에서 세그먼트 멤버십 정보를 캡처하려면 [!UICONTROL XDM Individual Profile] 스키마에 [세그먼트 멤버십 세부 정보 혼합을 사용해야 합니다.](../mixins/profile/segmentation.md)

![](../images/classes/segment-definition.png)

| 속성 | 설명 |
| --- | --- |
| `_repo` | 다음 [!UICONTROL DateTime] 필드를 포함하는 개체: <ul><li>`createDate`:데이터를 처음 인제스트한 시기 등 데이터 저장소에서 리소스가 만들어진 날짜 및 시간입니다.</li><li>`modifyDate`:리소스를 마지막으로 수정한 날짜 및 시간입니다.</li></ul> |
| `_id` | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고 데이터 중복을 방지하고 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 하지만 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다.<br><br>이 필드는 개별 개인 **과 관련된 ID를** 제공하지 않고 데이터 자체의 레코드를 구별하는 것이 중요합니다. 사람과 관련된 ID 데이터는 대신 [ID 필드](../schema/composition.md#identity)로 분류해야 합니다. |
| `createdByBatchID` | 레코드를 만든 인제스트된 일괄 처리의 ID. |
| `description` | 세그먼트 정의에 대한 설명입니다. |
| `identityMap` | 세그먼트가 적용되는 개인에 대한 이름 지정 ID 세트가 포함된 지도 필드입니다. 이 필드는 ID 데이터를 수집할 때 시스템에 의해 자동으로 업데이트됩니다.<br /><br />사용 사례에 대한 자세한 내용은 스키마 구성 [의 기본 사항](../schema/composition.md#identityMap) 에서 ID 맵에 대한 섹션을 참조하십시오. |
| `modifiedByBatchID` | 레코드를 업데이트하는 마지막 인제스트된 일괄 처리의 ID. |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID. |
| `segmentName` | **(필수)** 세그먼트 정의 이름입니다. |
| `segmentStatus` | 외부 시스템의 세그먼트 상태입니다. 다음 값이 허용됩니다. <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 세그먼트 정의의 최신 버전 번호입니다. |
