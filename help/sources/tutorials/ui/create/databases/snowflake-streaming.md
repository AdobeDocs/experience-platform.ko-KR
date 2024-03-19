---
title: UI를 사용하여 Snowflake 데이터베이스에서 Experience Platform으로 데이터 스트리밍
type: Tutorial
description: Snwoflake 데이터베이스에서 Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아봅니다
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 3%

---

# 에서 데이터 스트리밍 [!DNL Snowflake] UI를 사용하여 Experience Platform 할 데이터베이스

사용자 인터페이스를 사용하여 의 데이터를 스트리밍하는 방법 알아보기 [!DNL Snowflake] 이 안내서를 따라 Adobe Experience Platform에 데이터베이스를 추가합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

### 인증

의 안내서 읽기 [다음에 대한 필수 구성 요소 설정 [!DNL Snowflake] 스트리밍 데이터](../../../../connectors/databases/snowflake-streaming.md) 에서 스트리밍 데이터를 수집하기 전에 완료해야 하는 단계에 대한 자세한 내용 [!DNL Snowflake] Experience Platform.

## 사용 [!DNL Snowflake Streaming] 소스-스트림 [!DNL Snowflake] Experience Platform 데이터

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 *데이터베이스* 범주, 선택 **[!DNL Snowflake Streaming]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

>[!TIP]
>
>소스 카탈로그에 인증된 계정이 없는 소스는 **[!UICONTROL 설정]** 옵션을 선택합니다. 인증된 계정이 존재하면 이 옵션은 다음으로 변경됩니다. **[!UICONTROL 데이터 추가]**.

![Experience Platform UI의 소스 카탈로그로서 Snowflake 스트리밍 소스 카드가 선택된 경우](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

다음 **[!UICONTROL Snowflake 스트리밍 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

>[!BEGINTABS]

>[!TAB 새 계정 만들기]

새 계정을 만들려면 다음을 선택합니다. **[!UICONTROL 새 계정]** 이름, 설명(선택 사항) 및 자격 증명을 제공합니다.

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![소스 워크플로우의 새로운 계정 생성 인터페이스입니다.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| 자격 증명 | 설명 |
| --- | --- |
| 계정 | 의 이름 [!DNL Snowflake] 계정입니다. |
| 웨어하우스 | 의 이름 [!DNL Snowflake] 웨어하우스 웨어하우스에서 쿼리 실행을 관리합니다. [!DNL Snowflake]. 각 [!DNL Snowflake] warehouse는 서로 독립적이므로 데이터를 Experience Platform 상태로 가져오기 위해 개별적으로 액세스해야 합니다. |
| 데이터베이스 | 의 이름 [!DNL Snowflake] 데이터베이스. 데이터베이스에는 Experience Platform 대상으로 가져올 데이터가 포함되어 있습니다. |
| 스키마 | (선택 사항) 와 연관된 데이터베이스 스키마 [!DNL Snowflake] 계정입니다. |
| 사용자 이름 | 의 사용자 이름 [!DNL Snowflake] 계정입니다. |
| 암호 | 에 대한 암호 [!DNL Snowflake] 계정입니다. |
| 역할 | (선택 사항) 지정된 연결에 대해 사용자에게 제공할 수 있는 사용자 정의 역할입니다. 제공되지 않은 경우 이 값의 기본값은 입니다. `public`. |

계정 만들기에 대한 자세한 내용은 [역할 설정 구성](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) 다음에서 [!DNL Snowflake Streaming] 개요.

>[!TAB 기존 계정 사용]

기존 계정을 사용하려면 **[!UICONTROL 기존 계정]** 그런 다음 기존 계정 카탈로그에서 원하는 계정을 선택합니다.

**[!UICONTROL 다음]**&#x200B;을 선택하여 계속하십시오.

![소스 카탈로그의 기존 계정 선택 페이지입니다.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## 데이터 선택 {#select-data}

>[!IMPORTANT]
>
>스트리밍 데이터 흐름을 만들려면 소스 테이블에 타임스탬프 열이 있어야 합니다. 타임스탬프는 Experience Platform이 데이터가 수집되는 시기와 증분 데이터가 스트리밍되는 시기를 아는 데 필요합니다. 기존 연결에 대한 타임스탬프 열을 소급하여 추가하고 새 데이터 흐름을 만들 수 있습니다.

다음 [!UICONTROL 데이터 선택] 단계가 나타납니다. 이 단계에서는 Experience Platform으로 가져올 데이터를 선택하고, 타임스탬프와 시간대를 구성하고, 원시 데이터 수집을 위한 샘플 소스 데이터 파일을 제공해야 합니다.

화면 왼쪽에 있는 데이터베이스 디렉터리를 사용하고 Experience Platform으로 가져올 테이블을 선택합니다.

![데이터베이스 테이블이 선택된 선택 데이터 인터페이스입니다.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

그런 다음 테이블의 타임스탬프 열 유형을 선택합니다. 다음 두 가지 유형의 타임스탬프 열 중에서 선택할 수 있습니다. `TIMESTAMP_NTZ` 또는  `TIMESTAMP_LTZ`. 열 유형을 선택한 경우 `TIMESTAMP_NTZ`을 클릭한 다음 시간대도 제공해야 합니다. 열에는 null 아님 제약 조건이 있어야 합니다. 자세한 내용은 의 섹션을 참조하십시오. [제한 사항 및 자주 묻는 질문]

이 단계에서 채우기 설정을 구성할 수도 있습니다. 채우기 는 처음 수집되는 데이터를 결정합니다. 다시 채우기를 활성화하면 처음 예약된 수집 중에 지정된 경로의 모든 현재 파일이 수집됩니다. 그렇지 않으면 첫 번째 수집 실행과 시작 시간 사이에 로드된 파일만 수집됩니다. 시작 시간 이전에 로드된 파일은 수집되지 않습니다.

다음 항목 선택 **[!UICONTROL 채우기]** 채우기를 활성화하려면 전환합니다.

![타임스탬프, 시간대 및 채우기 구성 단계입니다.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

마지막으로 다음을 선택합니다. **[!UICONTROL 파일 선택]** 샘플 소스 데이터를 업로드하여 매핑 세트를 만드는 데 도움이 되도록 합니다. 매핑 세트는 이후 단계에서 원래 데이터를 XDM(Experience Data Model)에 매핑하는 데 사용됩니다.

완료되면 다음을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![소스 샘플 데이터의 미리보기.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## 데이터 세트 및 데이터 흐름 세부 정보 제공 {#provide-dataset-and-dataflow-details}

그런 다음 데이터 세트 및 데이터 흐름에 대한 정보를 제공해야 합니다.

### 데이터 세트 세부 정보 {#dataset-details}

데이터 세트는 스키마(열) 및 필드(행)를 포함하는 데이터 수집을 위한 저장소 및 관리 구조입니다. Experience Platform에 성공적으로 수집된 데이터는 데이터 세트로 데이터 레이크 내에 유지됩니다. 이 단계에서는 새 데이터 세트를 만들거나 기존 데이터 세트를 사용할 수 있습니다.

>[!BEGINTABS]

>[!TAB 새 데이터 세트 사용]

새 데이터 세트를 사용하려면 다음을 선택합니다. **[!UICONTROL 새 데이터 세트]**&#x200B;그런 다음 데이터 세트에 대한 이름과 설명(선택 사항)을 입력합니다. 데이터 세트에서 준수하는 XDM(경험 데이터 모델) 스키마도 선택해야 합니다.

![새 데이터 세트 선택 인터페이스입니다.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| 새 데이터 세트 세부 정보 | 설명 |
| --- | --- |
| 출력 데이터 세트 이름 | 새 데이터 세트의 이름입니다. |
| 설명 | (선택 사항) 새 데이터 세트에 대한 간략한 개요. |
| 스키마 | 조직에 있는 스키마의 드롭다운 목록입니다. 소스 구성 프로세스 전에 고유한 스키마를 생성할 수도 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [ui에서 XDM 스키마 만들기](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB 기존 데이터 세트 사용]

기존 데이터 세트가 있는 경우 **[!UICONTROL 기존 데이터 세트]** 그런 다음 **[!UICONTROL 고급 검색]** 실시간 고객 프로필로 수집하도록 활성화되었는지 여부 등 해당 세부 정보를 포함하여 조직의 모든 데이터 세트 창을 보는 옵션.

![기존 데이터 세트 선택 인터페이스입니다.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++프로필 수집, 오류 진단 및 부분 수집을 활성화하는 단계를 선택합니다.

데이터 세트가 실시간 고객 프로필에 대해 활성화된 경우 이 단계에서 전환할 수 있습니다 **[!UICONTROL 프로필 데이터 세트]** 프로필 수집을 위해 데이터를 활성화하려면 이 단계를 사용하여 을 활성화할 수도 있습니다 **[!UICONTROL 오류 진단]** 및 **[!UICONTROL 부분 수집]**.

* **[!UICONTROL 오류 진단]**: 선택 **[!UICONTROL 오류 진단]** 데이터 세트 활동 및 데이터 흐름 상태를 모니터링할 때 나중에 참조할 수 있는 오류 진단을 소스에 지시할 수 있습니다.
* **[!UICONTROL 부분 수집]**: 부분 일괄 처리 수집은 구성 가능한 특정 임계값까지 오류가 포함된 데이터를 수집하는 기능입니다. 이 기능을 사용하면 모든 정확한 데이터를 Experience Platform으로 성공적으로 수집할 수 있으며 잘못된 데이터는 모두 잘못된 이유에 대한 정보로 별도로 배치됩니다.

+++

### 데이터 흐름 세부 정보 {#dataflow-details}

데이터 세트가 구성되면 이름, 선택적 설명 및 경고 구성을 포함하여 데이터 흐름에 대한 세부 정보를 제공해야 합니다.

![데이터 흐름은 구성 단계를 자세히 설명합니다.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| 데이터 흐름 구성 | 설명 |
| --- | --- |
| 데이터 흐름 이름 | 데이터 흐름의 이름입니다.  기본적으로 가져올 파일의 이름이 사용됩니다. |
| 설명 | (선택 사항) 데이터 흐름에 대한 간략한 설명입니다. |
| 경고 | Experience Platform은 사용자가 구독할 수 있는 이벤트 기반 경고를 생성할 수 있습니다. 이러한 옵션을 트리거하려면 실행 중인 데이터 흐름이 필요합니다. 자세한 내용은 [경고 개요](../../alerts.md) <ul><li>**소스 데이터 흐름 실행 시작**: 데이터 흐름 실행이 시작될 때 알림을 받으려면 이 경고를 선택합니다.</li><li>**소스 데이터 흐름 실행 성공**: 데이터 흐름이 오류 없이 종료될 경우 알림을 받으려면 이 경고를 선택합니다.</li><li>**소스 데이터 흐름 실행 실패**: 데이터 흐름 실행이 오류로 인해 종료되는 경우 알림을 받으려면 이 경고를 선택합니다.</li></ul> |

완료되면 다음을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

## 필드를 XDM 스키마에 매핑 {#mapping}

다음 [!UICONTROL 매핑] 단계가 나타납니다. 매핑 인터페이스를 사용하여 소스 데이터를 적절한 스키마 필드에 매핑한 다음 해당 데이터를 Experience Platform으로 수집한 다음 을 선택합니다 **[!UICONTROL 다음]**. 매핑 인터페이스를 사용하는 방법에 대한 자세한 내용은 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md) 추가 정보.

![소스 워크플로우의 매핑 인터페이스입니다.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## 데이터 흐름 검토 {#review}

데이터 흐름 생성 프로세스의 마지막 단계는 데이터 흐름을 실행하기 전에 검토하는 것입니다. 사용 **[!UICONTROL 리뷰]** 단계에서 새 데이터 흐름이 실행되기 전에 세부 사항을 검토합니다. 세부 정보는 다음 카테고리로 그룹화됩니다.

* **연결**: 소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 수를 표시합니다.
* **데이터 세트 할당 및 필드 매핑**: 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 세트를 표시합니다.

데이터 흐름을 검토한 후 다음을 선택합니다 **[!UICONTROL 완료]** 데이터 흐름이 만들어지는 데 시간이 걸릴 수 있습니다.

![소스 워크플로우의 검토 단계입니다.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## 다음 단계

이 자습서에 따라 의 스트리밍 데이터 흐름을 만들었습니다. [!DNL Snowflake] 데이터. 추가 리소스는 아래 설명서를 참조하십시오.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 수집 비율, 성공 및 오류에 대한 정보를 볼 수 있습니다. 스트리밍 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [ui에서 스트리밍 데이터 흐름 모니터링](../../monitor-streaming.md).

### 데이터 흐름 업데이트

데이터 흐름 예약, 매핑 및 일반 정보에 대한 구성을 업데이트하려면 다음 자습서를 참조하십시오. [ui에서 소스 데이터 흐름 업데이트](../../update-dataflows.md).

### 데이터 흐름 삭제

를 사용하여 더 이상 필요하지 않거나 잘못 생성된 데이터 흐름을 삭제할 수 있습니다. **[!UICONTROL 삭제]** 다음에서 사용할 수 있는 함수 **[!UICONTROL 데이터 흐름]** 작업 영역. 데이터 흐름을 삭제하는 방법에 대한 자세한 내용은 [UI에서 데이터 흐름 삭제](../../delete.md).