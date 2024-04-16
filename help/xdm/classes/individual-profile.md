---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;identityMap;ID 맵;ID 맵;스키마 디자인;맵;맵;유니온 스키마;유니온
solution: Experience Platform
title: XDM 개별 프로필 클래스
description: XDM 개별 프로필 클래스에 대해 알아봅니다.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: ce937f1335283382189fa40f65aa268735c02715
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] 클래스

[!DNL XDM Individual Profile] 는 개별 사용자의 단일 표시(또는 &quot;프로필&quot;)를 형성하는 표준 경험 데이터 모델(XDM) 클래스입니다. 특히 클래스(및 호환 가능한 필드 그룹)는 브랜드와 상호 작용하는 식별된 개인과 부분적으로 식별된 개인 모두의 속성과 관심을 캡처합니다.

프로필의 범위는 익명 행동 신호(예: 브라우저 쿠키)부터 이름, 생년월일, 위치 및 이메일 주소와 같은 세부 정보가 포함된 고도로 식별된 프로필까지 다양합니다. 프로필이 성장하면 개인의 개인 정보, ID, 연락처 세부 정보 및 커뮤니케이션 환경 설정을 저장하는 강력한 저장소가 됩니다. 플랫폼 생태계에서 이 클래스의 사용에 대한 자세한 내용은 [XDM 개요](../home.md#data-behaviors).

![XDM 개별 프로필 클래스의 스키마 다이어그램입니다.](../images/classes/individual-profile.png)

| 속성 | 설명 |
| --- | --- |
| `_repo` | 다음을 포함하는 개체 [!UICONTROL DateTime] 필드: <ul><li>`createDate`: 데이터 저장소에서 리소스를 만든 날짜 및 시간입니다(예: 데이터가 처음 수집된 시간).</li><li>`modifyDate`: 리소스를 마지막으로 수정한 날짜 및 시간입니다.</li></ul> |
| `_id` | 레코드에 대한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다. 경우에 따라, `_id` 다음이 될 수 있음: [UUID(범용 고유 식별자)](https://tools.ietf.org/html/rfc4122) 또는 [GUID(Globally Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>소스 연결에서 데이터를 스트리밍하거나 Parquet 파일에서 직접 수집하는 경우, 기본 ID, 타임스탬프, 레코드 유형 등과 같이 레코드를 고유하게 만드는 특정 필드 조합을 연결하여 이 값을 생성해야 합니다. 연결된 값은 이어야 합니다. `uri-reference` 형식이 지정된 문자열입니다. 즉, 콜론 문자는 제거해야 합니다. 그런 다음 연결된 값을 SHA-256 또는 선택한 다른 알고리즘을 사용하여 해시해야 합니다.<br><br>이를 구별하는 것이 중요합니다 **이 필드는 개별 사용자와 관련된 id를 나타내지 않습니다.**&#x200B;를 검색하는 것이 더 효율적입니다. 개인과 관련된 ID 데이터는 다음으로 내보냅니다. [id 필드](../schema/composition.md#identity) 호환 가능한 필드 그룹에서 대신 제공합니다. |
| `createdByBatchID` | 레코드가 생성된 수집된 일괄 처리의 ID입니다. |
| `modifiedByBatchID` | 마지막으로 수집된 일괄 처리의 ID로 인해 레코드가 업데이트되었습니다. |
| `personID` | 해당 레코드와 관련된 개별 사용자에 대한 고유 식별자. 이 필드는 또한 로 지정되지 않는 한 해당 사용자와 관련된 ID를 반드시 나타내지는 않습니다. [id 필드](../schema/composition.md#identity). |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID입니다. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID입니다. |

{style="table-layout:auto"}

## 호환 가능한 필드 그룹 {#field-groups}

>[!NOTE]
>
>여러 필드 그룹의 이름이 변경되었습니다. 다음에 대한 문서 보기: [필드 그룹 이름 업데이트](../field-groups/name-updates.md) 추가 정보.

Adobe은 와 함께 사용할 수 있도록 여러 표준 필드 그룹을 제공합니다. [!DNL XDM Individual Profile] 클래스. 다음은 클래스에서 일반적으로 사용되는 몇 가지 필드 그룹 목록입니다.

* [[!UICONTROL 동의 및 환경 설정]](../field-groups/profile/consents.md)
* [[!UICONTROL 인구 통계 세부 정보]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 고객 충성도 세부 정보]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 개인 연락처 세부 정보]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 세그먼트 멤버십 세부 정보]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 통신 구독]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 회사 연락처 세부 정보]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM 비즈니스 사용자 구성 요소]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM 비즈니스 사용자 세부 정보]](../field-groups/profile/business-person-details.md)\*

*\*이 필드 그룹은 Adobe Real-time Customer Data Platform의 B2B 에디션에 액세스할 수 있는 조직만 사용할 수 있습니다.*

호환되는 모든 필드 그룹의 전체 목록을 보려면 [!DNL XDM Individual Profile]을(를) 참조하십시오. [XDM GitHub 저장소](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
