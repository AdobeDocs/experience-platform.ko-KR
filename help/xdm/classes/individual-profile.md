---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;ID맵;ID 맵;스키마 디자인;맵;맵;결합 스키마;결합
solution: Experience Platform
title: XDM 개별 프로필 클래스
topic-legacy: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 는 개별 개인의 단일 표현(또는 &quot;프로필&quot;)을 구성하는 표준 XDM(Experience Data Model) 클래스입니다. 특히, 클래스(및 그 호환 필드 그룹)는 브랜드와 상호 작용하는 식별된 개인과 부분적으로 식별된 개인의 속성 및 관심사를 캡처합니다.

프로필은 익명 행동 신호(예: 브라우저 쿠키)부터 이름, 생년월일, 위치 및 이메일 주소와 같은 세부 정보가 포함된 식별이 높은 프로필까지 다양할 수 있습니다. 프로필의 규모가 커지면 개인 정보, ID, 연락처 세부 사항 및 커뮤니케이션 환경 설정이 풍부한 저장소가 되어 개인별로 제공됩니다. 플랫폼 생태계에서 이 클래스를 사용하는 방법에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors).

다음 [!DNL XDM Individual Profile] 클래스 자체는 데이터를 수집할 때 자동으로 채워지는 여러 시스템 생성 값을 제공하는 반면 다른 모든 필드는 다음 사용 시 추가해야 합니다 [호환 가능한 스키마 필드 그룹](#field-groups):

![](../images/classes/individual-profile.png)

| 속성 | 설명 |
| --- | --- |
| `_repo` | 다음을 포함하는 개체 [!UICONTROL DateTime] 필드: <ul><li>`createDate`: 데이터를 처음 처리한 시기 등 데이터 저장소에서 리소스를 만든 날짜 및 시간입니다.</li><li>`modifyDate`: 리소스를 마지막으로 수정한 날짜 및 시간입니다.</li></ul> |
| `_id` | 레코드의 고유 문자열 식별자입니다. 이 필드는 개별 레코드의 고유성을 추적하고 데이터 중복을 방지하며 다운스트림 서비스에서 해당 레코드를 찾는 데 사용됩니다. 어떤 경우에는 `_id` 다음을 수행할 수 있습니다. [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) 또는 [GUID(Globally Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>소스 연결에서 데이터를 스트리밍하거나 Parquet 파일에서 직접 수집하는 경우 기본 ID, 타임스탬프, 레코드 유형 등과 같이 레코드가 고유한 특정 필드 조합을 연결하여 이 값을 생성해야 합니다. 연결된 값은 `uri-reference` 형식이 지정된 문자열. 즉, 콜론 문자를 제거해야 합니다. 그런 다음 연결된 값을 SHA-256 또는 선택한 다른 알고리즘을 사용하여 해시해야 합니다.<br><br>그것을 구분하는 것은 중요하다 **이 필드는 개별 사용자와 관련된 ID를 나타내지 않습니다**&#x200B;하지만, 오히려 데이터 자체의 기록입니다. 한 사람에 대한 신분자료는 다음과 같이 분류되어야 한다 [id 필드](../schema/composition.md#identity) 호환 필드 그룹에서 대신 제공합니다. |
| `createdByBatchID` | 레코드를 만든 수집된 일괄 처리의 ID입니다. |
| `modifiedByBatchID` | 레코드를 업데이트하도록 한 마지막으로 수집된 일괄 처리의 ID입니다. |
| `personID` | 이 레코드와 관련된 개인의 고유 식별자입니다. 이 필드는 또한 로 지정되지 않는 한 반드시 사람과 관련된 ID를 나타내지는 않습니다 [id 필드](../schema/composition.md#identity). |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID입니다. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

## 호환 가능한 필드 그룹 {#field-groups}

>[!NOTE]
>
>여러 필드 그룹의 이름이 변경되었습니다. 다음 문서를 참조하십시오. [필드 그룹 이름 업데이트](../field-groups/name-updates.md) 추가 정보.

Adobe은 와 함께 사용할 여러 표준 필드 그룹을 제공합니다 [!DNL XDM Individual Profile] 클래스 이름을 지정합니다. 다음은 클래스에 일반적으로 사용되는 몇 가지 필드 그룹 목록입니다.

* [[!UICONTROL 동의 및 기본 설정]](../field-groups/profile/consents.md)
* [[!UICONTROL 인구 통계 세부 정보]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 충성도 세부 사항]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 개인 연락처 세부 정보]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 세그먼트 멤버십 세부 정보]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 통신 구독]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 작업 연락처 세부 정보]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM 비즈니스 개인 구성 요소]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM 비즈니스 개인 세부 정보]](../field-groups/profile/business-person-details.md)\*

*\*이 필드 그룹은 Adobe Real-time Customer Data Platform B2B 버전에 액세스할 수 있는 조직에서만 사용할 수 있습니다.*

모든 호환 가능한 필드 그룹의 전체 목록 [!DNL XDM Individual Profile]를 참조하려면 [XDM GitHub 리포지토리](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
