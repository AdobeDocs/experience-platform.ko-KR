---
keywords: Experience Platform;홈;인기 항목;세그멘테이션 서비스;세그멘테이션 서비스;사용자 안내서;사용자 안내서;세그멘테이션 ui 안내서;세그먼트 빌더;실현됨;기존;종료
solution: Experience Platform
title: 세그멘테이션 서비스 UI 안내서
topic-legacy: ui guide
description: Adobe Experience Platform 세그멘테이션 서비스는 세그먼트 정의를 만들고 관리하기 위한 사용자 인터페이스를 제공합니다.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
translation-type: tm+mt
source-git-commit: fa2f4e046c6210137aa3e98d9f18010c1058275a
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---

# 세그멘테이션 서비스 UI 안내서

[!DNL Adobe Experience Platform Segmentation Service] 세그먼트 정의를 만들고 관리하기 위한 사용자 인터페이스를 제공합니다.

## 시작하기

세그먼트 정의를 사용하려면 세그멘테이션과 관련된 다양한 [!DNL Experience Platform] 서비스를 이해해야 합니다. 이 사용 안내서를 읽기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 고객, 잠재 고객, 사용자 또는 조직과 같은 개인 [!DNL Experience Platform] 과 관련된 저장된 데이터를 작은 그룹으로 나눌 수 있습니다.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):인제스트되는 다양한 데이터 소스의 ID를 통합하여 고객 프로파일을 생성할 수  [!DNL Platform]있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크

또한 이 문서를 통해 사용되는 두 개의 주요 용어를 알고 이 용어 간의 차이점을 이해하는 것이 중요합니다.
- **세그먼트 정의**:대상 대상의 주요 특성 또는 행동을 설명하는 데 사용되는 규칙 세트입니다.
- **대상**:세그먼트 정의 기준을 충족하는 결과 프로필 집합.

## 개요

[[!DNL Experience Platform] UI](https://platform.adobe.com/)에서 왼쪽 탐색 영역에서 **[!UICONTROL Segments]**&#x200B;을 선택하여 **[!UICONTROL Overview]** 탭을 엽니다. 이 탭에서는 세그먼트를 이해하고 작업을 시작하는 데 도움이 되는 설명서 및 비디오에 대한 링크를 제공합니다.

![](../images/ui/overview/segment-overview.png)

## 찾아보기

IMS 조직에 대한 모든 세그먼트 정의 목록을 보려면 **[!UICONTROL Browse]** 탭을 선택합니다.

![](../images/ui/overview/segment-browse-all.png)

이 보기는 분류, 이탈, 프로필 수, 평가 방법, 만든 날짜 및 마지막으로 수정한 날짜를 포함한 세그먼트 정의에 대한 정보를 나열합니다.

분류에는 다음 각 상태에 속하는 프로파일의 백분율을 나타내는 막대 그래프가 표시됩니다.[!UICONTROL Realized], [!UICONTROL Existing] 및 [!UICONTROL Exiting].

![](../images/ui/overview/segment-browse-breakdown.png)

| 상태 | 설명 |
| ------ | ----------- |
| 실현 | 세그먼트 내의 새 프로필. |
| 기존 | 세그먼트 내에 남아 있는 기존 프로필. |
| 종료 중 | 세그먼트를 떠나는 기존 프로필. |

이탈(churn)은 세그먼트 작업이 마지막으로 실행된 시간에 비해 세그먼트 정의 내에서 변경되는 프로필의 백분율을 나타내며 프로필 수는 세그먼트에 자격을 갖춘 총 프로필 수를 나타냅니다.

평가 방법은 스트리밍 또는 일괄 처리일 수 있습니다. 스트리밍 세그먼트는 데이터가 시스템에 입력될 때 지속적으로 평가됩니다. 배치 세그먼트는 설정된 일정에 따라 평가됩니다.

![](../images/ui/overview/segment-browse-segments.png)

페이지 상단에는 모든 세그먼트를 일정에 추가하고 새 세그먼트를 만드는 옵션이 있습니다.

**[!UICONTROL Add all segments to schedule]**&#x200B;을(를) 전환하면 예약된 세그먼테이션이 활성화됩니다. 예약된 세그멘테이션에 대한 자세한 내용은 이 사용 안내서](#scheduled-segmentation)의 [예약된 세그멘테이션 섹션에서 확인할 수 있습니다.

**[!UICONTROL Create segment]**&#x200B;을 선택하면 세그먼트 빌더로 이동합니다. 세그먼트 만들기에 대한 자세한 내용은 사용자 안내서](#create-segment)에서 세그먼트 만들기에 대한 섹션을 참조하십시오.[

![](../images/ui/overview/segment-browse-top.png)

오른쪽 사이드바는 총 세그먼트 수, 마지막 평가 날짜, 다음 평가 날짜 및 평가 방법별 세그먼트 분류를 나열하는 IMS 조직 내의 모든 세그먼트에 대한 정보를 포함합니다.

![](../images/ui/overview/segment-browse-segment-info.png)

세그먼트 정의의 행을 선택하면 세그먼트 정의 요약을 제공합니다. 세그먼트 이름, 설명, 평가 방법, 만든 날짜 및 마지막으로 수정한 날짜 외에 세그먼트를 편집 또는 삭제할 수 있는 옵션, 세그먼트에 대한 자격이 있는 대상, 총 대상자 크기 등이 포함됩니다.

![](../images/ui/overview/segment-browse-details.png)

## 세그먼트 정의 세부 정보 {#segment-details}

특정 세그먼트 정의에 대한 자세한 내용을 보려면 **[!UICONTROL Browse]** 탭 내에서 세그먼트 이름을 선택합니다.

세그먼트 세부 사항 페이지가 나타납니다. 맨 위에는 세그먼트 정의 요약, 자격이 있는 대상 크기에 대한 정보 및 세그먼트가 활성화된 대상이 있습니다.

![](../images/ui/overview/segment-details-summary.png)

### 세그먼트 요약

**[!UICONTROL Segment summary]** 섹션에서는 ID, 이름, 설명 및 속성의 세부 사항과 같은 정보를 제공합니다.

또한 세그먼트를 편집할 수 있는 옵션이 제공됩니다. **[!UICONTROL Edit segment]**&#x200B;을 선택하면 [!DNL Segment Builder]로 이동합니다. [!DNL Segment Builder] 작업 영역 사용에 대한 자세한 내용은 [[!DNL Segment Builder] 사용자 안내서](./segment-builder.md)를 참조하십시오.

### 세그먼트의 총 고객 수

**[!UICONTROL Total audience in segment]** 섹션에는 세그먼트에 적합한 총 프로필 수가 표시됩니다.

추정은 해당 일의 샘플 데이터의 샘플 크기를 사용하여 생성됩니다. 프로필 스토어에 1백만 개 미만의 엔티티가 있는 경우 전체 데이터 세트가 사용됩니다.1백만~2천만 개의 개체 중 100만 개의 개체가 사용됩니다.2천만 개 이상의 개체에 대해 전체 엔티티의 5%가 사용됩니다. 세그먼트 예상 생성에 대한 자세한 내용은 세그먼트 작성 자습서의 [예측 생성 섹션](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)에서 확인할 수 있습니다.

### 활성화된 대상

**[!UICONTROL Activated destinations]** 섹션에는 이 세그먼트가 활성화된 대상이 표시됩니다.

>[!NOTE]
>
> 대상은 [!DNL Real-time Customer Data Platform]에서 사용할 수 있는 기능으로, 외부 플랫폼으로 데이터를 내보낼 수 있습니다. 대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오. 세그먼트를 대상에 활성화하는 방법에 대해 알아보려면 세그먼트를 대상](../../destinations/ui/activate-destinations.md)으로 활성화하는 방법에 대한 [안내서를 읽어 보십시오.

### 프로필 샘플

그 아래에 [!DNL Profile] ID, 이름, 성 및 개인 이메일 등 정보를 자세히 설명하는 프로필 샘플이 있습니다.

데이터 샘플링을 트리거하는 방법은 수집 방법에 따라 다릅니다.

일괄 처리를 위해 프로필 스토어는 마지막 샘플링 작업이 실행된 이후 새 일괄 처리가 성공적으로 인제스트되었는지 확인하기 위해 15분마다 자동으로 스캔됩니다. 그런 경우 나중에 프로필 스토어를 스캔하여 레코드 수가 5% 이상 변경되었는지 확인합니다. 이러한 조건이 충족되면 새 샘플링 작업이 트리거됩니다.

스트리밍 수집에 대해 프로필 스토어는 매시간 자동으로 스캔되어 기록 수가 최소 5% 변경되었는지 확인합니다. 이 조건이 충족되면 새 샘플링 작업이 트리거됩니다.

스캔의 샘플 크기는 프로필 저장소의 전체 개체 수에 따라 달라집니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 스토어의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2,000만 | 100만 |
| 2천만 명 이상 | 합계의 5% |

각 [!DNL Profile]에 대한 자세한 내용은 [!DNL Profile] ID를 선택하여 확인할 수 있습니다. 프로필의 세부 사항에 대한 자세한 내용은 [[!DNL Real-time Customer Profile] 사용자 안내서](../../profile/ui/user-guide.md#profile-detail)를 참조하십시오.

![](../images/ui/overview/segment-details-profiles.png)

## 세그먼트 만들기 {#create-segment}

오른쪽 위 모서리에서 **[!UICONTROL Create segment]**&#x200B;을 선택하면 세그먼트 정의 만들기를 시작할 수 있는 [!DNL Segment Builder] 작업 영역이 열립니다.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 작업 공간

[!DNL Segment Builder] 는  [!DNL Profile] 데이터 요소와 상호 작용할 수 있는 풍부한 작업 영역을 제공합니다. 작업 영역은 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다.

[!DNL Segment Builder] 작업 영역 사용에 대한 자세한 내용은 [[!DNL Segment Builder] 사용자 안내서](./segment-builder.md)를 참조하십시오.

![](../images/ui/overview/segment-builder.png)

## 예약된 세그먼테이션 {#scheduled-segmentation}

세그먼트 정의가 생성되면 주문형 또는 예약된(연속) 평가를 통해 평가할 수 있습니다. 평가는 해당 대상을 만들기 위해 세그먼트 정의를 통해 [!DNL Real-time Customer Profile] 데이터를 이동하는 것을 의미합니다. 만들어진 대상은 [!DNL Experience Platform] API를 사용하여 내보낼 수 있도록 저장되고 저장됩니다.

주문형 평가에는 API를 사용하여 평가를 수행하고 필요에 따라 대상을 빌드하는 작업이 포함되지만, 예약된 평가(&#39;예약된 세그멘테이션&#39;이라고도 함)를 사용하면 일정 시간(최대 일일 1회)에 세그먼트 정의를 평가하는 반복 일정을 만들 수 있습니다.

### 예약된 세그먼테이션 사용 {#enable-scheduled-segmentation}

예약된 평가에 대한 세그먼트 정의 활성화는 UI 또는 API를 사용하여 수행할 수 있습니다. UI에서 **[!UICONTROL Segments]** 내의 **[!UICONTROL Browse]** 탭으로 돌아가 **[!UICONTROL Add all segments to schedule]**&#x200B;를 전환합니다. 이렇게 하면 조직에서 설정한 일정에 따라 모든 세그먼트가 평가됩니다.

>[!NOTE]
>
>[!DNL XDM Individual Profile]에 대해 최대 5개의 병합 정책이 있는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다. 조직에서 단일 샌드박스 환경 내에서 [!DNL XDM Individual Profile]에 대한 병합 정책이 5개 이상 있는 경우 예약된 평가를 사용할 수 없습니다.

예약은 현재 API를 사용해서만 만들 수 있습니다. API를 사용하여 예약을 생성, 편집 및 작업하는 방법에 대한 자세한 내용은 튜토리얼을 따라 세그먼트 결과를 평가하고 액세스할 수 있습니다. 특히 API](../tutorials/evaluate-a-segment.md#scheduled-evaluation)를 사용하여 [예약된 평가에 대한 섹션을 참조하십시오.

![](../images/ui/overview/segment-browse-scheduled.png)

## 스트리밍 세그먼테이션 {#streaming-segmentation}

스트리밍 세그먼테이션은 데이터 풍부함에 주력하면서 거의 실시간으로 [!DNL Platform]에 세분화를 수행하는 기능입니다. 스트리밍 세그먼테이션을 통해 이제 데이터가 [!DNL Platform]에 도달하면 세그먼트 자격이 부여되므로 세그먼테이션 작업을 예약하고 실행할 필요가 없습니다.

스트리밍 세그멘테이션에 대한 자세한 내용은 [스트리밍 세그멘테이션 사용자 안내서](./streaming-segmentation.md)에서 확인할 수 있습니다.

>[!NOTE]
>
>스트리밍 세그먼테이션이 작동하려면 조직에 대해 예약된 세그먼테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 자세한 내용은 이 사용 안내서](#scheduled-segmentation)의 스트리밍 세그멘테이션 섹션을 참조하십시오.[

## 가장자리 세그멘테이션 {#edge-segmentation}

Edge Segmentation은 Platform에서 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지 개인화 사용 사례를 활성화하는 기능입니다.

가장자리 세그멘테이션에 대한 자세한 내용은 [가장자리 세그멘테이션 UI 안내서](./edge-segmentation.md)에서 확인할 수 있습니다.

## 정책 위반

>[!NOTE]
>
>정책 위반은 대상에 지정된 세그먼트를 만드는 경우에만 적용됩니다.

세그먼트 작성을 완료하면 세그먼트 내에 정책 위반이 없도록 Adobe Experience Platform 데이터 거버넌스에 의해 세그먼트가 분석됩니다. 자세한 내용은 [[!DNL Data Governance] 개요](../../data-governance/home.md)를 참조하십시오.

![](../images/ui/overview/segment-dule-policy-violations.png)

## 다음 단계 및 추가 리소스 {#next-steps}

[!DNL Segmentation Service] UI는 [!DNL Real-time Customer Profile] 데이터에서 마케팅 가능한 대상을 격리할 수 있는 풍부한 워크플로를 제공합니다.

[!DNL Segmentation Service]에 대한 자세한 내용을 보려면 설명서를 계속 읽으십시오. [!DNL Segmentation Service] API를 사용하는 방법에 대한 자세한 내용은 [[!DNL Segmentation Service] 개발자 안내서](../api/overview.md)를 참조하십시오.
