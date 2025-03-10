---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;캠페인;캠페인 관리 서비스
title: Platform UI를 사용하여 Adobe Campaign Managed Cloud Services 소스 연결 만들기
description: Platform UI를 사용하여 Adobe Experience Platform을 Adobe Campaign Managed Cloud Services에 연결하는 방법을 알아봅니다.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: 67f42c155bf34f2b8adc3b08536bb3310bb77390
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 6%

---

# Platform UI를 사용하여 Adobe Campaign Managed Cloud Services 소스 연결 만들기

이 자습서에서는 Adobe Campaign Managed Cloud Services 데이터를 Adobe Experience Platform으로 가져오기 위해 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [샌드박스](../../../../../sandboxes/home.md): 플랫폼은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## Adobe Campaign Managed Cloud Services을 플랫폼에 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 검색 창을 사용하여 표시되는 소스의 범위를 좁힐 수도 있습니다.

**[!UICONTROL Adobe 응용 프로그램]** 범주에서 **[!UICONTROL Adobe Campaign Managed Cloud Services]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![Adobe Campaign Managed Cloud Services 카드를 표시하는 소스 카탈로그입니다.](../../../../images/tutorials/create/campaign/catalog.png)

### 데이터 선택 {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Adobe Campaign 환경 인스턴스"
>abstract="사용할 Adobe Campaign 환경의 이름입니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="대상 매핑"
>abstract="대상 매핑은 메시지를 게재할 목적으로 Campaign에서 사용하는 기술 오브젝트이고, 게재 목록(주소, 전화번호, 옵트인 표시기, 추가 식별자 등)을 전송하는 데 필요한 모든 기술 설정을 포함합니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="스키마 이름"
>abstract="Adobe Campaign 데이터베이스에 정의된 엔티티 이름입니다."
>text="Learn more in documentation"

[!UICONTROL 데이터 선택] 단계가 나타나고 [!UICONTROL Adobe Campaign 인스턴스], [!UICONTROL 대상 매핑] 및 [!UICONTROL 스키마 이름]을 구성하는 인터페이스를 제공합니다.

| 속성 | 설명 |
| --- | --- |
| Adobe Campaign 인스턴스 | 사용 중인 Adobe Campaign 환경 인스턴스의 이름입니다. |
| 대상 매핑 | 메시지를 전달하기 위해 Campaign에서 사용하는 기술 개체이며, 게재를 보내는 데 필요한 모든 기술 설정을 포함합니다. |
| 스키마 이름 | Platform으로 가져오는 스키마 엔티티의 이름입니다. 옵션에는 게재 로그 및 추적 로그가 포함됩니다. |

![Adobe Campaign 인스턴스, 대상 매핑 및 스키마 이름을 구성할 수 있는 인터페이스입니다.](../../../../images/tutorials/create/campaign/select-data.png)

Campaign 인스턴스, 대상 매핑 및 스키마 이름에 대한 값을 제공하면 화면이 업데이트되어 스키마 미리보기와 샘플 데이터 세트가 표시됩니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![스키마 계층 구조 및 데이터 집합 샘플을 미리 봅니다](../../../../images/tutorials/create/campaign/preview.png)

### 기존 데이터 세트 사용

[!UICONTROL 데이터 흐름 세부 정보] 페이지에서 기존 데이터 집합을 사용할지 또는 데이터 흐름에 대한 새 데이터 집합을 구성할지 여부를 선택할 수 있습니다.

기존 데이터 집합을 사용하려면 **[!UICONTROL 기존 데이터 집합]**&#x200B;을(를) 선택하십시오. [!UICONTROL 고급 검색] 옵션을 사용하거나 드롭다운 메뉴에서 기존 데이터 세트 목록을 스크롤하여 기존 데이터 세트를 검색할 수 있습니다.

데이터 세트를 선택한 상태에서 데이터 흐름의 이름과 설명(선택 사항)을 입력합니다.

![기존 데이터 집합 옵션을 표시하는 인터페이스입니다.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### 새 데이터 세트 사용

새 데이터 집합을 사용하려면 **[!UICONTROL 새 데이터 집합]**&#x200B;을(를) 선택한 다음 출력 데이터 집합 이름과 선택적 설명을 입력하십시오. 그런 다음 [!UICONTROL 고급 검색] 옵션을 사용하거나 드롭다운 메뉴에서 기존 스키마 목록을 스크롤하여 매핑할 스키마를 선택합니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![새 데이터 집합 옵션을 표시하는 인터페이스입니다.](../../../../images/tutorials/create/campaign/new-dataset.png)

### 경고 활성화

경고를 활성화하여 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 구독하고 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 소스 경고 구독](../../alerts.md)에 대한 안내서를 참조하십시오.

데이터 흐름에 세부 정보를 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![데이터 흐름에 사용할 수 있는 다양한 경고 유형 선택](../../../../images/tutorials/create/campaign/alerts.png)

### 데이터 필드를 XDM 스키마에 매핑

소스 스키마의 소스 필드를 대상 스키마의 해당 대상 XDM 필드에 매핑할 수 있는 인터페이스를 제공하는 [!UICONTROL 매핑] 단계가 나타납니다.

Platform은 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md)를 참조하십시오.

>[!IMPORTANT]
>
>소스 필드를 대상 XDM 필드에 매핑할 때 지정된 기본 ID 필드를 해당 대상 XDM 필드에 매핑해야 합니다.
>
>각 대상자에 대해 Adobe Campaign에 매핑할 필드를 최대 20개까지 추가할 수 있습니다. Campaign 탐색기의 관리 > 플랫폼 > 옵션 폴더에서 `NmsCdp_Aep_Sources_Max_Columns` 옵션의 값을 업데이트하여 이 제한을 변경할 수 있습니다.

원본 데이터가 성공적으로 매핑되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![4개의 원본 데이터 필드가 해당 XDM 스키마 필드에 매핑된 매핑 트리입니다.](../../../../images/tutorials/create/campaign/mapping.png)

### 데이터 흐름 검토

새 데이터 흐름을 만들기 전에 검토할 수 있는 **[!UICONTROL 검토]** 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 원본 형식, 선택한 원본 파일의 관련 경로 및 해당 원본 파일에 있는 열의 양을 표시합니다.
* **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 데이터 집합이 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 집합을 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 선택하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![연결 및 데이터 집합 정보를 표시하는 검토 페이지입니다.](../../../../images/tutorials/create/campaign/review.png)

### 데이터 세트 활동 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집 중인 데이터를 모니터링하여 수집 비율 및 성공한 일괄 처리와 실패한 일괄 처리에 대한 정보를 볼 수 있습니다.

데이터 집합 활동을 보려면 소스 카탈로그에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하세요.

![데이터 흐름 헤더 탭이 선택된 소스 카탈로그 페이지입니다.](../../../../images/tutorials/create/campaign/dataflows.png)

그런 다음 나타나는 데이터 흐름 목록에서 대상 데이터 세트를 선택합니다.

![Adobe Campaign 게재 로그 대상 데이터 집합이 선택된 기존 데이터 흐름 목록입니다.](../../../../images/tutorials/create/campaign/target-dataset.png)

데이터 세트 활동 페이지가 나타납니다. 여기에서 수집 비율, 성공한 배치 및 실패한 배치를 포함하여 데이터 흐름의 성능에 대한 정보를 확인할 수 있습니다.

이 페이지에서는 데이터 흐름의 메타데이터 설명을 업데이트하고, 부분 수집 및 오류 진단을 활성화하고, 새 데이터를 데이터 집합에 추가할 수 있는 인터페이스도 제공합니다.

![선택한 데이터 집합의 수집 속도를 나타내는 그래프가 있는 인터페이스입니다.](../../../../images/tutorials/create/campaign/dataset-activity.png)


>[!IMPORTANT]
>
>이전 이벤트 로그를 Adobe Campaign Managed Cloud Services 소스로 채울 수 없습니다. 다시 채우기가 필요한 경우 사용자 지정 워크플로 또는 사용자 지정 구현을 사용하여 데이터를 Amazon S3 또는 Azure Blob으로 내보내거나 Amazon S3 또는 Azure Blob에서 Adobe Experience Platform 데이터 세트로 데이터를 내보냅니다.


## 다음 단계

이 자습서에 따라 Campaign v8 게재 로그 및 추적 로그 데이터를 플랫폼으로 가져오는 데이터 흐름을 만들었습니다. 이제 [!DNL Real-Time Customer Profile] 및 [!DNL Data Science Workspace]과(와) 같은 다운스트림 플랫폼 서비스에서 수신 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-Time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)
