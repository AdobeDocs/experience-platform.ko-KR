---
solution: Experience Platform
title: 세그먼트 정의 클래스
description: 이 문서에서는 XDM(Experience Data Model)의 세그먼트 정의 클래스에 대한 개요를 제공합니다.
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# [!UICONTROL 세그먼트 정의] 클래스

&quot;[!UICONTROL 세그먼트 정의]는 세그먼트 정의의 세부 사항을 캡처하는 표준 XDM(Experience Data Model) 클래스입니다. 이 클래스에는 다른 선택적 특성과 함께 세그먼트의 ID 및 이름과 같은 필수 필드가 포함되어 있습니다. 외부 시스템에서 Adobe Experience Platform으로 세그먼트 정의를 가져오는 경우 이 클래스를 사용해야 합니다.

>[!NOTE]
>
>이 클래스는 세그먼트 정의 자체에 대한 정보를 캡처하는 데만 사용해야 합니다. 프로필 데이터 내에서 세그먼트 멤버십 정보를 캡처하려면 다음을 사용해야 합니다 [세그먼트 멤버십 세부 사항 필드 그룹](../field-groups/profile/segmentation.md) 다음 위치에서 [!UICONTROL XDM 개별 프로필] 스키마.

![](../images/classes/segment-definition.png)

| 속성 | 설명 |
| --- | --- |
| `_repo` | 다음을 포함하는 개체 [!UICONTROL DateTime] 필드: <ul><li>`createDate`: 데이터를 처음 처리한 시기 등 데이터 저장소에서 리소스를 만든 날짜 및 시간입니다.</li><li>`modifyDate`: 리소스를 마지막으로 수정한 날짜 및 시간입니다.</li></ul> |
| `_id` | 레코드에 대한 고유한 시스템 생성 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터의 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템이 생성되므로 데이터를 수집하는 동안 명시적 값을 제공하지 않습니다. 그러나 원할 경우 여전히 고유한 ID 값을 제공하도록 선택할 수 있습니다.<br><br>이 분야를 구분하는 것이 중요합니다 **포함하지 않음** 개별 개인과 관련된 ID를 나타내지만 데이터 자체의 레코드를 나타냅니다. 한 사람에 대한 신분자료는 다음과 같이 분류되어야 한다 [id 필드](../schema/composition.md#identity) 을 가리키도록 업데이트하는 것이 좋습니다. |
| `createdByBatchID` | 레코드를 만든 수집된 일괄 처리의 ID입니다. |
| `description` | 세그먼트 정의에 대한 설명입니다. |
| `identityMap` | 세그먼트가 적용되는 개인의 네임스페이스가 지정된 ID 세트가 포함된 맵 필드입니다. 의 ID 맵에 대한 섹션을 참조하십시오. [스키마 구성 기본 사항](../schema/composition.md#identityMap) 를 참조하십시오. |
| `modifiedByBatchID` | 레코드를 업데이트하도록 한 마지막으로 수집된 일괄 처리의 ID입니다. |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID입니다. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID입니다. |
| `segmentName` | **(필수)** 세그먼트 정의의 이름입니다. |
| `segmentStatus` | 외부 시스템의 세그먼트 상태입니다. 다음 값이 허용됩니다. <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 세그먼트 정의의 최신 버전 번호입니다. |

{style=&quot;table-layout:auto&quot;}
