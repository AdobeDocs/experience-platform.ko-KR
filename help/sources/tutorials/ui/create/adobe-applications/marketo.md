---
keywords: Experience Platform;홈;인기 항목;Marketo 소스 커넥터;Marketo 커넥터;Marketo 소스;Marketo
solution: Experience Platform
title: UI에서 Marketo Engage 소스 커넥터 만들기
topic-legacy: overview
type: Tutorial
description: 이 자습서에서는 UI에서 B2B 데이터를 Adobe Experience Platform으로 가져오기 위해 Marketo Engage 소스 커넥터를 만드는 단계를 제공합니다.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 0%

---

# 만들기 [!DNL Marketo Engage] UI의 소스 커넥터

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Marketo Engage] (이하 &quot;라 한다)[!DNL Marketo]&quot;) B2B 데이터를 Adobe Experience Platform으로 가져오기 위한 UI의 소스 커넥터입니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [XDM(경험 데이터 모델)](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [UI에서 스키마 만들기 및 편집](../../../../../xdm/ui/resources/schemas.md): UI에서 스키마를 만들고 편집하는 방법을 알아봅니다.
* [ID 네임스페이스](../../../../../identity-service/namespaces.md): ID 네임스페이스는 [!DNL Identity Service] ID가 연관되는 컨텍스트의 지표 역할을 합니다. 정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Marketo] 플랫폼의 계정은 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID는 특정 항목에 대한 고유 식별자입니다 [!DNL Marketo] 인스턴스. |
| `clientId` | 사용자의 고유한 클라이언트 ID [!DNL Marketo] 인스턴스. |
| `clientSecret` | 사용자의 고유한 클라이언트 암호 [!DNL Marketo] 인스턴스. |

이러한 값 가져오기에 대한 자세한 내용은 [[!DNL Marketo] 인증 안내서](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

필요한 자격 증명을 수집하면 다음 섹션의 단계를 따를 수 있습니다.

## 연결 [!DNL Marketo] account

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL Adobe 애플리케이션] 카테고리, 선택 **[!UICONTROL Marketo Engage]**. 그런 다음 **[!UICONTROL 데이터 추가]** 새 [!DNL Marketo] 데이터 흐름.

![카탈로그](../../../../images/tutorials/create/marketo/catalog.png)

다음 **[!UICONTROL Marketo Engage에 연결]** 페이지가 나타납니다. 이 페이지에서 새 계정을 사용하거나 기존 계정에 액세스할 수 있습니다.

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 계정 이름, 선택적 설명 및 [!DNL Marketo] 인증 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![신규 계정](../../../../images/tutorials/create/marketo/new.png)

### 기존 계정

기존 계정으로 데이터 흐름을 만들려면 **[!UICONTROL 기존 계정]** 그런 다음 [!DNL Marketo] 사용할 계정입니다. 선택 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/marketo/existing.png)

## 데이터 세트 선택

작성 후 [!DNL Marketo] 계정에서는 다음 단계에서 탐색할 수 있는 인터페이스를 제공합니다 [!DNL Marketo] 데이터 세트.

인터페이스 왼쪽 절반은 디렉토리 브라우저로 10개를 표시합니다 [!DNL Marketo] 데이터 세트. 완벽하게 작동하는 [!DNL Marketo] 소스 연결을 사용하려면 9개의 서로 다른 데이터 세트를 수집해야 합니다. 또한 [!DNL Marketo] 계정 기반 마케팅(ABM) 기능을 사용하는 경우 10번째 데이터 흐름을 만들어 데이터를 수집해야 합니다 [!UICONTROL 명명된 계정] 데이터 세트.

>[!NOTE]
>
>간결성을 위해 다음 자습서에서는 을 사용합니다 [!UICONTROL 명명된 계정] 예를 들어, 아래에 설명된 단계는 10개 중 하나에 적용됩니다 [!DNL Marketo] 데이터 세트.

먼저 수집할 데이터 세트를 선택한 다음 을 선택합니다 **[!UICONTROL 다음]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## 맵 [!DNL Marketo] 플랫폼으로 스키마

다음 [!UICONTROL 매핑] 단계가 나타나고 매핑할 인터페이스를 제공합니다. [!DNL Marketo] Platform으로 스키마를 전송할 수 있습니다.

수집할 인바운드 데이터에 대한 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

### 기존 데이터 세트 사용

기존 데이터 세트에 데이터를 수집하려면 을 선택합니다 **[!UICONTROL 기존 데이터 세트]**&#x200B;그런 다음 데이터 세트 아이콘을 선택합니다.

![기존 데이터 세트](../../../../images/tutorials/create/marketo/existing-dataset.png)

다음 **[!UICONTROL 데이터 세트 선택]** 대화 상자가 나타납니다. 사용할 적절한 스키마가 있는 데이터 세트를 찾고 선택한 다음 선택합니다 **[!UICONTROL 확인]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### 새 데이터 세트 사용

데이터를 새 데이터 세트에 수집하려면 을 선택합니다 **[!UICONTROL 새 데이터 세트]** 제공된 필드에 데이터 집합의 이름과 설명을 입력합니다.

에 스키마 이름을 입력하여 스키마를 검색할 수 있습니다 **[!UICONTROL 스키마 선택]** 검색 창. 드롭다운 아이콘을 선택하여 기존 스키마 목록을 볼 수도 있습니다. 또는 다음을 선택할 수 있습니다 **[!UICONTROL 고급 검색]** 각 세부 정보를 포함하여 기존 스키마의 페이지에 액세스합니다.

전환 **[!UICONTROL 프로필 데이터 세트]** target 데이터 세트에 대한 활성화 단추 [!DNL Profile]를 사용하면 엔티티의 속성 및 동작을 전체적으로 볼 수 있습니다. 모든 항목의 데이터 [!DNL Profile]-활성화된 데이터 세트가 [!DNL Profile] 및 변경 사항은 데이터 흐름을 저장할 때 적용됩니다.

![새로운 데이터 세트 만들기](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

스키마를 선택하면 아래로 스크롤하여 매핑 대화 상자를 보고 매핑을 시작합니다 [!DNL Marketo] 데이터 집합 필드를 적절한 대상 XDM 필드에 추가합니다.

### 맵 [!DNL Marketo] XDM 필드를 대상으로 하는 데이터 세트 소스 필드

각 [!DNL Marketo] 데이터 세트에는 따라야 할 고유한 매핑 규칙이 있습니다. 매핑 방법에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Marketo] XDM에 데이터 세트:

* [활동](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [프로그램](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [프로그램 멤버십](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [회사](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [정적 목록](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [정적 목록 구성원](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [명명된 계정](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [기회](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [기회 연락처 역할](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [사람](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

선택 **[!UICONTROL 데이터 미리 보기]** 선택한 데이터 세트를 기반으로 매핑 결과를 확인하십시오.

![매핑](../../../../images/tutorials/create/marketo/mapping.png)

다음 [!UICONTROL 미리 보기] popover는 선택한 데이터 세트에서 최대 100개의 샘플 데이터 행의 매핑 결과를 탐색할 수 있는 인터페이스를 제공합니다.

![미리 보기](../../../../images/tutorials/create/marketo/mapping-preview.png)

소스 필드가 적절한 대상 필드에 매핑되면 을 선택합니다 **[!UICONTROL 닫기]**.

## 데이터 흐름 세부 정보 제공

다음 [!UICONTROL 데이터 흐름 세부 정보] 새 데이터 로드에 대한 이름 및 간단한 설명을 제공할 수 있는 단계가 나타납니다.

![데이터 흐름 세부 정보](../../../../images/tutorials/create/marketo/dataflow-detail.png)

를 활성화합니다 **[!UICONTROL 오류 진단]** API를 사용하여 다운로드할 수 있는 새로 수집된 일괄 처리에 대한 자세한 오류 메시지 생성을 허용하려면 토글을 전환합니다. 자세한 내용은 [데이터 수집 오류 진단 검색](../../../../../ingestion/quality/error-diagnostics.md).

![오류](../../../../images/tutorials/create/marketo/errors.png)

다음 [!DNL Marketo] 커넥터는 일괄 처리를 사용하여 모든 기록 레코드를 수집하고 실시간 업데이트를 위해 스트리밍 수집 기능을 사용합니다. 이렇게 하면 커넥터가 잘못된 레코드를 수집하는 동안 스트리밍을 계속할 수 있습니다. 를 활성화합니다 **[!UICONTROL 부분 수집]** 전환 후 설정 [!UICONTROL 오류 임계값 %] 데이터 흐름이 실패하지 않도록 최대화하려면 다음을 수행하십시오.

**[!UICONTROL 부분 수집]** 은 특정 임계값까지 오류가 포함된 데이터를 수집할 수 있는 기능을 제공합니다. 자세한 내용은 [부분 배치 수집 개요](../../../../../ingestion/batch-ingestion/partial.md).

데이터 흐름 세부 정보를 제공하고 오류 임계값을 최대로 설정하면 **[!UICONTROL 다음]**.

![부분 수집](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## 데이터 흐름 검토

다음 **[!UICONTROL 검토]** 새 데이터 흐름을 만들기 전에 검토할 수 있는 단계가 나타납니다. 세부 사항은 다음 범주 내에 그룹화됩니다.

* **[!UICONTROL 연결]**: 소스 유형, 선택한 소스 엔티티의 관련 경로 및 해당 소스 엔티티 내의 열 양을 표시합니다.
* **[!UICONTROL 데이터 세트 및 맵 필드 할당]**: 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 세트를 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]** 데이터 흐름을 만들 시간을 허용합니다.

![검토](../../../../images/tutorials/create/marketo/review.png)

## 데이터 흐름 모니터링

데이터 흐름이 만들어지면 이를 통해 수집되는 데이터를 모니터링하여 수집률, 성공 및 오류에 대한 정보를 볼 수 있습니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 다음 내용을 참조하십시오 [UI에서 데이터 흐름 모니터링](../../../../../dataflows/ui/monitor-sources.md).

## 속성 삭제

데이터 세트의 사용자 지정 속성은 소급하여 숨기거나 제거할 수 없습니다. 기존 데이터 세트에서 사용자 지정 속성을 숨기거나 제거하려면 이 사용자 지정 속성, 새 XDM 스키마 없이 새 데이터 세트를 만들고 새로 만드는 데이터 세트에 대해 새 데이터 세트를 구성해야 합니다. 숨기거나 제거할 사용자 지정 특성이 있는 데이터 세트로 구성된 원본 데이터 흐름을 비활성화하거나 삭제해야 합니다.

## 데이터 흐름 삭제

더 이상 필요하지 않거나 잘못된 데이터 흐름을 **[!UICONTROL 삭제]** 함수에서 사용 가능한 함수 [!UICONTROL 데이터 흐름] 작업 공간. 데이터 흐름을 삭제하는 방법에 대한 자세한 내용은 [UI에서 데이터 흐름 삭제](../../delete.md).

## 다음 단계

이 자습서를 따라 가져올 데이터 흐름을 만들었습니다 [!DNL Marketo] 데이터. 이제 와 같은 다운스트림 Platform 서비스에서 들어오는 데이터를 사용할 수 있습니다. [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](/help/profile/home.md)
* [[!DNL Data Science Workspace] 개요](/help/data-science-workspace/home.md)
