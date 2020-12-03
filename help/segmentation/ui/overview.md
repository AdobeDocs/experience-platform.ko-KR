---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;realized;existing;exiting;
solution: Experience Platform
title: 세그멘테이션 서비스 사용 안내서
topic: ui guide
description: Adobe Experience Platform 세그멘테이션 서비스는 세그먼트 정의를 만들고 관리하기 위한 사용자 인터페이스를 제공합니다.
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---


# 세그멘테이션 서비스 사용 안내서

[!DNL Adobe Experience Platform Segmentation Service] 세그먼트 정의를 만들고 관리하기 위한 사용자 인터페이스를 제공합니다.

## 시작하기

세그먼트 정의를 사용하려면 세그먼테이션과 관련된 다양한 [!DNL Experience Platform] 서비스를 이해해야 합니다. 이 사용자 안내서를 읽기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 고객, 잠재 고객, 사용자 또는 조직과 같은 개인 [!DNL Experience Platform] 과 관련된 데이터를 작은 그룹으로 나눌 수 있습니다.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):수집되는 다양한 데이터 소스에서 ID를 연결하여 고객 프로파일을 만들 수 [!DNL Platform]있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

또한 이 문서를 통해 사용되는 두 개의 주요 용어를 알고 이 용어 간의 차이점을 이해하는 것이 중요합니다.
- **세그먼트 정의**:대상 대상의 주요 특성 또는 행동을 설명하는 데 사용되는 규칙 세트입니다.
- **대상**:세그먼트 정의 기준을 충족하는 결과 프로필 집합입니다.

## 개요

UI [[!DNL Experience Platform] 에서](http://platform.adobe.com/)왼쪽 탐색 **[!UICONTROL 에서]** 세그먼트를 선택하여 **[!UICONTROL 개요]** 탭을엽니다. 이 탭에서는 세그먼트를 이해하고 작업을 시작하는 데 도움이 되는 설명서 및 비디오에 대한 링크를 제공합니다.

![](../images/ui/overview/segment-overview.png)

## 찾아보기

IMS **[!UICONTROL 조직의]** 모든 세그먼트 정의 목록을 보려면 찾아보기 탭을 선택합니다.

![](../images/ui/overview/segment-browse-all.png)

이 보기에는 분류, 가입 해지, 프로필 수, 평가 방법, 만든 날짜, 마지막으로 수정한 날짜 등 세그먼트 정의에 대한 정보가 표시됩니다.

분류에는 다음 각 상태에 속한 프로필의 백분율을 나타내는 막대 그래프가 표시됩니다. [!UICONTROL 입장], [!UICONTROL 실현됨]및 [!UICONTROL 종료됨].

![](../images/ui/overview/segment-browse-breakdown.png)

| 상태 | 설명 |
| ------ | ----------- |
| 입력됨 | 세그먼트 내의 새 프로필. |
| 실현 | 세그먼트 내에 남아 있는 기존 프로필. |
| 종료 중 | 세그먼트를 떠나는 기존 프로필. |

이탈은 세그먼트 작업이 마지막으로 실행된 시간과 비교하여 세그먼트 정의 내에서 변경되는 프로필의 백분율을 나타내며 프로필 수는 세그먼트에 자격을 갖춘 총 프로필 수를 나타냅니다.

평가 방법은 스트리밍 또는 일괄 처리일 수 있습니다. 데이터가 시스템에 입력되면 스트리밍 세그먼트는 지속적으로 평가됩니다. 배치 세그먼트는 설정된 일정에 따라 평가됩니다.

![](../images/ui/overview/segment-browse-segments.png)

페이지 상단에는 모든 세그먼트를 일정에 추가하고 새 세그먼트를 만드는 옵션이 있습니다.

예약을 **[!UICONTROL 위해 모든 세그먼트 추가를 전환하면]** 예약된 세그먼테이션이 활성화됩니다. 예약된 세그멘테이션에 대한 자세한 내용은 이 사용 안내서의 [예약된 세그멘테이션 섹션에서 확인할 수 있습니다](#scheduled-segmentation).

세그먼트 **[!UICONTROL 만들기를]** 선택하면 세그먼트 빌더로 이동합니다. 세그먼트 만들기에 대한 자세한 내용은 사용자 안내서에서 세그먼트 [만들기에 대한 섹션을 참조하십시오](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

오른쪽 사이드바는 총 세그먼트 수, 마지막 평가 날짜, 다음 평가 날짜 및 평가 방법별 세그먼트 분류를 나열하는 IMS 조직 내의 모든 세그먼트에 대한 정보를 포함합니다.

![](../images/ui/overview/segment-browse-segment-info.png)

세그먼트 정의의 행을 선택하면 세그먼트 정의 요약을 제공합니다. 세그먼트 편집 또는 삭제 옵션, 세그먼트에 적합한 대상, 총 대상자 크기, 세그먼트의 이름, 설명, 평가 방법, 만든 날짜 및 마지막으로 수정한 날짜 외에 세그먼트 정의에 대한 요약을 제공합니다.

![](../images/ui/overview/segment-browse-details.png)

## 세그먼트 정의 세부 사항 {#segment-details}

특정 세그먼트 정의에 대한 자세한 내용을 보려면 **[!UICONTROL 찾아보기]** 탭 내에서 세그먼트 이름을 선택합니다.

세그먼트 세부 사항 페이지가 나타납니다. 맨 위에는 세그먼트 정의, 자격이 있는 대상 크기에 대한 정보 및 세그먼트가 활성화된 대상에 대한 요약이 있습니다.

![](../images/ui/overview/segment-details-summary.png)

### 세그먼트 요약

세그먼트 **[!UICONTROL 요약]** 섹션에서는 ID, 이름, 설명 및 속성의 세부 사항과 같은 정보를 제공합니다.

또한 세그먼트를 편집할 수 있는 옵션이 제공됩니다. 세그먼트 **[!UICONTROL 편집을]** 선택하면 해당 페이지로 이동합니다 [!DNL Segment Builder]. 작업 공간 사용에 대한 자세한 내용은 [!DNL Segment Builder] 사용 [[!DNL Segment Builder] 안내서를 참조하십시오](./segment-builder.md).

### 세그먼트의 총 고객 수

세그먼트 **[!UICONTROL 의 총 대상]** 섹션에는 세그먼트에 자격을 갖춘 총 프로필 수가 표시됩니다.

추정은 해당 일의 샘플 데이터의 샘플 크기를 사용하여 생성됩니다. 프로필 스토어에 1백만 개 미만의 개체가 있는 경우 전체 데이터 세트가 사용됩니다.100만개에서 2000만개가 사용됩니다.2천만 개 이상의 개체에 대해 전체 개체의 5%가 사용됩니다. 세그먼트 예측 생성에 대한 자세한 내용은 세그먼트 작성 자습서의 [예측 생성 섹션](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 에서 확인할 수 있습니다.

### 활성화된 대상

활성화된 **[!UICONTROL 대상]** 섹션에는 이 세그먼트가 활성화된 대상이 표시됩니다.

>[!NOTE]
>
> 대상은 에서 사용할 수 [!DNL Real-time Customer Data Platform]있는 기능으로, 외부 플랫폼으로 데이터를 내보낼 수 있습니다. 대상에 대한 자세한 내용은 [대상 개요를 참조하십시오](../../destinations/home.md). 대상에 세그먼트를 활성화하는 방법을 알려면 세그먼트에 대한 활성화 [가이드를 참조하십시오](../../destinations/ui/activate-destinations.md).

### 프로필 샘플

그 아래에는 ID, 이름, 성 및 개인 이메일 등 정보를 자세히 설명하는 세그먼트 자격을 규정하는 프로필 샘플이 있습니다. [!DNL Profile]

데이터 샘플링이 트리거되는 방법은 섭취 방법에 따라 다릅니다.

일괄 처리를 위해 프로필 스토어는 마지막 샘플링 작업이 실행된 이후 새 일괄 처리가 성공적으로 수집되었는지 확인하기 위해 15분마다 자동으로 스캔됩니다. 그런 경우 프로필 스토어는 이후 스캔되어 레코드 수가 5% 이상 변경되었는지 확인합니다. 이러한 조건이 충족되면 새 샘플링 작업이 트리거됩니다.

스트리밍 통합 시, 프로필 스토어는 매시간마다 자동으로 스캔되어 레코드 수가 최소 5% 이상 변경되었는지 확인합니다. 이 조건이 충족되면 새 샘플링 작업이 트리거됩니다.

스캔 샘플 크기는 프로필 스토어의 전체 개체 수에 따라 달라집니다. 이러한 샘플 크기는 다음 표에 나와 있습니다.

| 프로필 스토어의 엔티티 | 샘플 크기 |
| ------------------------- | ----------- |
| 100만 미만 | 전체 데이터 세트 |
| 1~2000만 | 100만 |
| 2,000만 이상 | 합계의 5% |

각 ID에 대한 자세한 내용은 ID를 선택하여 확인할 [!DNL Profile] 수 [!DNL Profile] 있습니다. 프로필의 세부 사항에 대한 자세한 내용은 [[!DNL Real-time Customer Profile] 사용 안내서를 참조하십시오](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## 세그먼트 만들기 {#create-segment}

오른쪽 **[!UICONTROL 상단 모서리에서 세그먼트]** 만들기를 선택하면 [!DNL Segment Builder] 작업 공간이 열리고 세그먼트 정의를 만들 수 있습니다.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 작업 공간

[!DNL Segment Builder] 은 데이터 요소와 상호 작용할 수 있는 풍부한 작업 공간을 [!DNL Profile] 제공합니다. 작업 영역에서는 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다.

작업 공간 사용에 대한 자세한 내용은 [!DNL Segment Builder] 사용 [[!DNL Segment Builder] 안내서를 참조하십시오](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## 예약된 세그먼테이션 {#scheduled-segmentation}

세그먼트 정의가 만들어지면 주문형 또는 예약된(연속) 평가를 통해 평가할 수 있습니다. 평가는 해당 대상을 만들기 위해 세그먼트 정의를 통해 [!DNL Real-time Customer Profile] 데이터를 이동하는 것을 의미합니다. 만들어진 대상은 저장 및 저장되므로 [!DNL Experience Platform] API를 사용하여 내보낼 수 있습니다.

on-demand 평가에는 API를 사용하여 평가를 수행하고 필요에 따라 대상을 빌드하는 작업이 포함되지만, 예약된 평가(&#39;예약된 세그먼트&#39;라고도 함)를 사용하면 특정 시간(하루 최대 1회)에 세그먼트 정의를 평가하는 반복 일정을 만들 수 있습니다.

### 예약된 세그먼테이션 사용 {#enable-scheduled-segmentation}

예약된 평가에 대한 세그먼트 정의 활성화는 UI 또는 API를 사용하여 수행할 수 있습니다. UI에서 세그먼트 내 **[!UICONTROL 의]** **[!UICONTROL 찾아보기]** 탭으로 ****&#x200B;돌아가서예약할 모든 세그먼트추가를전환합니다. 이렇게 하면 조직에서 설정한 일정에 따라 모든 세그먼트가 평가됩니다.

>[!NOTE]
>
>최대 5개의 병합 정책을 포함하는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다 [!DNL XDM Individual Profile]. 조직에서 단일 샌드박스 환경 [!DNL XDM Individual Profile] 에 대해 5개 이상의 병합 정책을 보유하고 있는 경우 예약된 평가를 사용할 수 없습니다.

일정은 현재 API를 사용해서만 만들 수 있습니다. API를 사용하여 예약을 생성, 편집 및 작업하는 방법에 대한 자세한 내용은 튜토리얼을 따라 세그먼트 결과를 평가하고 액세스할 수 있으며, 특히 API를 사용한 [예약된 평가에 대한 섹션을 참조하십시오](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## 스트리밍 세분화 {#streaming-segmentation}

스트리밍 세그먼테이션은 데이터 풍부함에 주력하면서 거의 실시간으로 세분화를 수행하는 [!DNL Platform] 기능입니다. 이제 스트리밍 세분화를 통해 데이터가 유입되면 세그먼트 자격 조건 [!DNL Platform]이 높아져 세분화 작업을 예약하고 실행할 필요가 없습니다.

스트리밍 세그멘테이션에 대한 자세한 내용은 [스트리밍 세그멘테이션 사용자 안내서를 참조하십시오](./streaming-segmentation.md).

>[!NOTE]
>
>스트리밍 세그멘테이션이 작동하려면 조직의 예약된 세그멘테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 자세한 내용은 이 사용자 안내서 [의 스트리밍 세그멘테이션 섹션을 참조하십시오](#scheduled-segmentation).

## 정책 위반

>[!NOTE]
>
>대상에 지정된 세그먼트를 만드는 경우에만 정책 위반이 적용됩니다.

세그먼트 작성을 완료하면 세그먼트 내에 정책 위반이 없도록 Adobe Experience Platform 데이터 거버넌스에 의해 세그먼트가 분석됩니다. See the [[!DNL Data Governance] overview](../../data-governance/home.md) for more information.

![](../images/ui/overview/segment-dule-policy-violations.png)

## 다음 단계 및 추가 리소스 {#next-steps}

이 [!DNL Segmentation Service] UI는 마케팅 가능한 대상을 데이터에서 분리할 수 있는 풍부한 워크플로우를 제공합니다 [!DNL Real-time Customer Profile] .

자세한 내용 [!DNL Segmentation Service]은 설명서를 계속 읽어 보십시오. API를 사용하는 방법에 대한 자세한 내용은 [!DNL Segmentation Service] 개발자 안내서를 참조하십시오 [[!DNL Segmentation Service] ](../api/overview.md).
