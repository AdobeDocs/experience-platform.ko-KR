---
solution: Experience Platform
title: 세그먼테이션 서비스 UI 안내서
description: Adobe Experience Platform UI에서 대상 및 세그먼트 정의를 만들고 관리하는 방법을 알아봅니다.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 276fd7c532843c9589e1d51b0bc7a76cb5c3eb9f
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 2%

---

# 세그먼테이션 서비스 UI 안내서

[!DNL Adobe Experience Platform Segmentation Service]은(는) 대상 및 세그먼트 정의를 만들고 관리하기 위한 사용자 인터페이스를 제공합니다.

## 시작하기

대상 및 세그먼트 정의를 사용하여 작업하려면 세그먼테이션과 관련된 다양한 [!DNL Experience Platform] 서비스를 이해해야 합니다. 이 사용 안내서를 읽기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service]을(를) 사용하면 개인(예: 고객, 잠재 고객, 사용자 또는 조직)과 관련된 [!DNL Experience Platform]에 저장된 데이터를 더 작은 그룹으로 분할할 수 있습니다.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): [!DNL Platform]&#x200B;(으)로 수집되는 서로 다른 데이터 소스의 ID를 연결하여 고객 프로필을 만들 수 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): [!DNL Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그먼테이션을 최대한 활용하려면 [데이터 모델링 모범 사례](../../xdm/schema/best-practices.md)에 따라 데이터가 프로필 및 이벤트로 수집되는지 확인하십시오.

또한 이 문서에서 사용되는 다음 주요 용어를 이해하고 그 차이점을 이해해야 합니다.

- **대상**: 유사한 비헤이비어 및/또는 특성을 공유하는 사람들의 컬렉션입니다. 이 인물 컬렉션은 세그먼트 정의(플랫폼 생성 대상), 대상자 구성을 사용하여 Adobe Experience Platform에서 생성하거나, 사용자 지정 업로드(외부 생성 대상)와 같은 외부 소스에서 생성할 수 있습니다.
- **세그먼트 정의**: Adobe Experience Platform에서 대상 대상의 주요 특성 또는 동작을 설명하는 데 사용하는 규칙입니다.
- **세그먼트**: 프로필을 대상자로 분리하는 작업입니다.

## 개요

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 대상]**&#x200B;을(를) 선택하여 [!UICONTROL 대상] 대시보드를 표시하는 **[!UICONTROL 개요]** 탭을 엽니다.

>[!NOTE]
>
>Platform을 처음 사용하는 조직에 아직 활성 프로필 데이터 세트 또는 병합 정책을 만들지 않은 경우 [!UICONTROL 대상] 대시보드가 표시되지 않습니다. 대신 [!UICONTROL 개요] 탭에 대상자를 시작하는 데 도움이 되는 링크와 설명서가 표시됩니다.

### [!UICONTROL 대상자] 대시보드 {#segments-dashboard}

**[!UICONTROL 대상]** 대시보드는 조직의 대상 데이터와 관련된 주요 지표를 간략하게 설명합니다.

자세한 내용은 [대상자 대시보드 가이드](../../dashboards/guides/audiences.md)를 참조하세요.

![대상자 대시보드가 표시됩니다. 대상 크기, ID별 프로필, ID 중복 및 대상 크기 변경 트렌드를 포함한 다양한 위젯을 표시합니다.](../../dashboards/images/segments/dashboard-overview.png)

## 찾아보기 {#browse}

대상 포털을 보려면 **[!UICONTROL 찾아보기]** 탭을 선택하십시오. Audience Portal은 조직 및 샌드박스에 속하는 모든 Audiences 목록을 제공하며 프로필 수, 원본, 생성 날짜, 마지막 수정 날짜, 태그 및 분류와 같은 세부 정보를 포함합니다.

또한 대상 포털을 사용하면 세그먼트 빌더 또는 대상 구성을 사용하여 새 대상을 만들 수 있을 뿐만 아니라 외부에서 생성된 대상을 Platform으로 가져올 수 있습니다.

Audience Portal에 대한 자세한 내용은 [Audience Portal 개요](./audience-portal.md)를 참조하십시오.

## 구성 {#compositions}

조직의 대상 구성을 통해 생성된 모든 대상 목록을 보려면 **[!UICONTROL 구성]** 탭을 선택하십시오.

![조직의 대상 구성에서 만든 대상 목록입니다.](../images/ui/overview/compositions.png)

기본적으로 이 보기에는 이름, 상태, 만든 날짜, 만든 사람, 마지막 업데이트 날짜 및 마지막 업데이트 날짜 등 대상에 대한 정보가 나열됩니다.

각 대상 옆에 줄임표 아이콘이 있습니다. 이 옵션을 선택하면 대상자에 대해 사용 가능한 빠른 작업 목록이 표시됩니다.

| 작업 | 설명 |
| ------ | ----------- |
| 복제 | 선택한 대상자를 복사합니다. |
| 액세스 관리 | 대상에 속하는 액세스 레이블을 관리합니다. 액세스 레이블에 대한 자세한 내용은 [레이블 관리](../../access-control/abac/ui/labels.md)에 대한 설명서를 참조하십시오. |
| 삭제 | 선택한 대상자를 삭제합니다. 다운스트림 대상에 사용되거나 다른 대상에 종속된 대상은 **삭제할 수 없습니다**. 대상자 삭제에 대한 자세한 내용은 [세그먼테이션 FAQ](../faq.md#lifecycle-states)를 참조하십시오. |

![표 사용자 지정](/help/images/icons/column-settings.png) 아이콘을 선택하여 표시되는 필드를 변경할 수 있습니다.

![표 사용자 지정 단추가 강조 표시되어 있습니다. 이 단추를 선택하면 대상자 구성 페이지에 표시되는 필드를 사용자 지정할 수 있습니다.](../images/ui/overview/compositions-select-customize-table.png)

표 내에 표시할 수 있는 모든 필드를 나열하는 팝오버가 나타납니다.

![컴포지션 섹션에 표시할 수 있는 특성입니다.](../images/ui/overview/compositions-customize-table.png)

| 필드 | 설명 |
| ----- | ----------- | 
| [!UICONTROL 이름] | 대상자의 이름입니다. |
| [!UICONTROL 상태] | 대상의 상태입니다. 이 필드에 사용할 수 있는 값은 `Draft`, `Inactive` 및 `Published`입니다. |
| [!UICONTROL 생성일] | 대상자가 생성된 시간과 날짜. |
| [!UICONTROL 만든 사람] | 대상을 만든 사람의 이름입니다. |
| [!UICONTROL 업데이트됨] | 대상자가 마지막으로 업데이트된 시간 및 날짜입니다. |
| [!UICONTROL 업데이트한 사람] | 대상자를 마지막으로 업데이트한 사람의 이름입니다. |

대상자가 구성되는 방식을 보려면 [!UICONTROL 대상자] 탭에서 대상자의 이름을 선택하십시오.

대상을 구성하는 빌딩 블록이 포함된 [대상 구성] 페이지가 나타납니다. 대상 구성을 사용하는 방법에 대한 자세한 내용은 [대상 구성 UI 안내서](./audience-composition.md)를 참조하십시오.

## 페더레이션된 대상자 구성 {#fac}

대상 구성 및 세그먼트 정의 외에 Adobe Federated Audience Composition을 사용하여 기본 데이터를 복사하지 않고 Enterprise 데이터 세트에서 새 대상을 작성하고 이러한 대상을 Adobe Experience Platform Audience Portal에 저장할 수 있습니다. Enterprise Data Warehouse에서 페더레이션된 구성된 대상 데이터를 활용하여 Adobe Experience Platform의 기존 대상을 강화할 수도 있습니다. [Federated Audience Composition](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/home)에 대한 안내서를 읽어 보십시오.

![조직의 Federated Audience Composition에서 만든 대상 목록입니다.](../images/ui/overview/federated-audience-composition.png)

## 스트리밍 세분화 {#streaming-segmentation}

스트리밍 세분화는 데이터 풍부성에 중점을 두고 거의 실시간으로 [!DNL Platform]에서 세분화를 수행하는 기능입니다. 스트리밍 세분화를 사용하면 데이터가 [!DNL Platform]&#x200B;(으)로 들어오는 동안 세분화 자격이 적용되므로 세분화 작업을 예약하고 실행할 필요가 줄어듭니다.

스트리밍 세분화에 대한 자세한 내용은 [스트리밍 세분화 사용 안내서](../methods/streaming-segmentation.md)를 참조하세요.

>[!NOTE]
>
>스트리밍 세분화를 사용하려면 조직에 대해 예약된 세분화를 활성화해야 합니다. 예약된 세그먼테이션 활성화에 대한 자세한 내용은 [이 사용 안내서의 스트리밍 세그먼테이션 섹션](#scheduled-segmentation)을 참조하세요.

## 에지 세분화 {#edge-segmentation}

Edge 세그멘테이션은 가장자리에 있는 Platform의 대상자를 즉시 평가하는 기능으로, 동일한 페이지와 다음 페이지 개인화 사용 사례를 활성화합니다.

에지 세분화에 대한 자세한 내용은 [에지 세분화 UI 안내서](../methods/edge-segmentation.md)를 참조하세요.

## 정책 위반

>[!NOTE]
>
>정책 위반은 대상에 할당된 대상을 만드는 경우에만 적용됩니다.

대상자 만들기가 완료되면, 대상자 내에 정책 위반이 없도록 Adobe Experience Platform 데이터 거버넌스에서 대상자를 분석합니다. 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 참조하십시오.

![대상에 대한 정책 위반이 표시됩니다.](../images/ui/overview/audience-dule-policy-violations.png)

## 다음 단계 및 추가 리소스 {#next-steps}

[!DNL Segmentation Service] UI는 [!DNL Real-Time Customer Profile] 데이터에서 마케팅 가능한 대상을 만들 수 있는 풍부한 워크플로를 제공합니다.

[!DNL Segmentation Service]에 대해 자세히 알아보려면 설명서를 계속 읽으십시오. [!DNL Segmentation Service] API를 사용하는 방법을 알아보려면 [[!DNL Segmentation Service] 개발자 안내서](../api/overview.md)를 참조하십시오.
