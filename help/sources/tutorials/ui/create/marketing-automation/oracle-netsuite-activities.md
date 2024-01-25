---
title: 만들기 [!DNL Oracle NetSuite Activities] UI의 소스 연결
description: Adobe Experience Platform UI를 사용하여 Oracle NetSuite 활동 소스 연결을 만드는 방법을 알아봅니다.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 053cf0af327b39830f025686e0f8f67c27f1c45c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---

# 만들기 [!DNL Oracle NetSuite Activities] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL Oracle NetSuite Activities] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

에서 이벤트 데이터를 가져오는 방법을 알아보려면 다음 튜토리얼을 참조하십시오 [!DNL Oracle NetSuite Activities] UI에서 Adobe Experience Platform에 계정을 추가합니다.

## 시작하기 {#getting-started}

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Oracle NetSuite] 계정, 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/marketing-automation.md).

>[!TIP]
>
>읽기 [[!DNL Oracle NetSuite] 개요](../../../../connectors/marketing-automation/oracle-netsuite.md) 인증 자격 증명을 검색하는 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

## 연결 [!DNL Oracle NetSuite] account {#connect-account}

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 *마케팅 자동화* 범주, 선택 **[!DNL Oracle NetSuite Activities]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![oracle NetSuite 활동 카드가 있는 카탈로그용 플랫폼 UI 스크린샷](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/catalog-card.png)

다음 **[!UICONTROL oracle NetSuite 활동 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

>[!IMPORTANT]
>
>새로 고침 토큰은 7일 후에 만료됩니다. 토큰이 만료되면 업데이트된 토큰으로 Experience Platform 시 계정을 만들어야 합니다. 업데이트된 토큰으로 새 계정을 만들지 않으면 다음 오류 메시지가 표시될 수 있습니다. `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### 기존 계정 {#existing-account}

기존 계정을 사용하려면 [!DNL Oracle NetSuite Activities] 새 데이터 흐름을 만들 계정 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![oracle NetSuite 활동 계정을 기존 계정과 연결하는 플랫폼 UI 스크린샷](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/existing.png)

### 새 계정 {#new-account}

새 계정을 만드는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**&#x200B;을 누르고 이름, 설명(선택 사항) 및 자격 증명을 제공합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![oracle NetSuite 활동 계정을 새 계정과 연결하는 플랫폼 UI 스크린샷](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/new.png)

## 다음 단계 {#next-steps}

이 자습서를 따라 [!DNL Oracle NetSuite Activities] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터를 Platform으로 가져오는 데이터 흐름 구성](../../dataflow/marketing-automation.md).

## 추가 리소스 {#additional-resources}

아래 섹션에서는 사용 시 참조할 수 있는 추가 리소스를 제공합니다. [!DNL Oracle NetSuite Activities] 소스.

### 매핑 {#mapping}

Platform은 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>표시되는 필드는 이 소유한 구독에 따라 다릅니다. [!DNL Oracle NetSuite] 계정에 대한 액세스 권한이 있습니다. 예를 들어 청구에 대한 액세스 권한이 없는 경우 청구 관련 필드가 표시되지 않습니다.

### 예약 {#scheduling}

예약 시 [!DNL Oracle NetSuite Activities] 수집을 위해 다음 빈도 및 간격 구성을 선택해야 합니다.

| 빈도 | 간격 |
| --- | --- |
| `Once` | 1 |

데이터를 검색하는 동안 [!DNL Oracle NetSuite] 는 마지막으로 수정되거나 생성된 날짜와 타임스탬프 대신 날짜 형식으로 응답합니다. 따라서 예약은 하루로 제한됩니다.

예약에 대한 값을 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

![소스 워크플로우의 예약 단계입니다.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/scheduling.png)