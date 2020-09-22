---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;data flows
description: Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 기존 계정 및 데이터 흐름을 보는 단계를 제공합니다.
solution: Experience Platform
title: 계정 및 데이터 흐름 모니터링
topic: overview
translation-type: tm+mt
source-git-commit: 8f752d6a08496f9583627781d9143ee7f9159bf0
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---


# UI에서 계정 및 데이터 흐름 모니터링

Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 기존 계정 및 데이터 흐름을 보는 단계를 [!UICONTROL 제공합니다] .

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model] (XDM) 시스템](../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL 실시간 고객 프로필]](../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 계정 모니터링

[Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택하여 **[!UICONTROL 소스 작업 영역에]** 액세스합니다. [ **[!UICONTROL 카탈로그]** ] 화면에는 계정 및 데이터 흐름을 만들 수 있는 다양한 소스가 표시됩니다. 각 소스에는 연결된 기존 계정 및 데이터 흐름 수가 표시됩니다.

상단 헤더에서 **[!UICONTROL 계정을]** 선택하여 기존 계정을 봅니다.

![카탈로그](../../images/tutorials/monitor/catalog-accounts.png)

계정 **[!UICONTROL 페이지가]** 나타납니다. 이 페이지에는 소스, 사용자 이름, 데이터 흐름 수 및 작성 날짜에 대한 정보를 비롯하여 볼 수 있는 계정 목록이 있습니다.

왼쪽 상단에 있는 단계 아이콘을 선택하여 정렬 창을 실행합니다.

![계정](../../images/tutorials/monitor/accounts-list.png)

정렬 패널을 사용하면 특정 소스의 계정에 액세스할 수 있습니다. 작업할 소스를 선택하고 오른쪽 목록에서 계정을 선택합니다.

>[!TIP]
>
> [ ![이름](../../images/tutorials/monitor/spectrum-control.png) ] 열의 **[!UICONTROL 스펙트럼 제어]** 단추를 사용하여 선택한 계정에 대한 새 소스 데이터 흐름을 만듭니다.

![계정 선택](../../images/tutorials/monitor/accounts-sort.png)

또한 기존 계정 정보를 편집하고 계정 자격 증명을 업데이트할 수 있습니다. 편집할 계정 정보의 연필 아이콘을 선택합니다.

![](../../images/tutorials/monitor/click-edit.png)

계정 **[!UICONTROL 세부 사항]** 모달이 나타납니다. 이 페이지에서 기존 계정 세부 사항 및 인증 자격 증명을 업데이트할 수 있습니다.

![](../../images/tutorials/monitor/edit-account.png)

계정 **[!UICONTROL 페이지에서]** 액세스한 계정과 연결된 기존 데이터 흐름 또는 대상 데이터 집합 목록을 볼 수 있습니다. 선택한 데이터 흐름`...`에 사용할 수 있는 추가 옵션을 표시하려면 줄임표(줄임표) 단추를 선택합니다. 이러한 옵션은 아래에 자세히 설명되어 있습니다.

| 컨트롤 | 설명 |
| ------- | ----------- |
| [!UICONTROL 일정 편집] | 데이터 흐름 통합 일정을 편집할 수 있습니다. |
| [!UICONTROL 데이터 흐름 비활성화] | 선택한 데이터 흐름 동안 데이터 수집을 비활성화할 수 있습니다. |
| [!UICONTROL 삭제] | 선택한 데이터 흐름을 삭제할 수 있습니다. |

![데이터 흐름](../../images/tutorials/monitor/dataflows.png)

## 데이터 흐름 모니터링

데이터 파일은 계정을 보지 않고도 **[!UICONTROL 카탈로그]** 페이지에서 직접 액세스할 수 **[!UICONTROL 있습니다]**. 데이터 **[!UICONTROL 흐름]** 목록을 보려면 상단 헤더에서 데이터 흐름을 선택합니다.

![카탈로그 데이터 흐름](../../images/tutorials/monitor/catalog-dataflows.png)

기존 데이터 흐름 목록이 나타납니다. 이 페이지에서는 소스, 사용자 이름, 데이터 흐름 수 및 상태에 대한 정보를 비롯하여 볼 수 있는 데이터 흐름 목록이 있습니다.

상태에 대한 자세한 내용은 다음 표를 참조하십시오.

| 상태 | 설명 |
| ------ | ----------- |
| 활성화됨 | 상태는 데이터 흐름 `Enabled` 이 활성화되어 있고 제공된 일정에 따라 데이터를 인제스트하고 있음을 나타냅니다. |
| 비활성화됨 | 상태는 데이터 흐름 `Disabled` 이 비활성 상태이며 데이터를 인제스트하고 있지 않음을 나타냅니다. |
| 처리 중 | 상태는 데이터 흐름 `Processing` 이 아직 활성화되지 않았음을 나타냅니다. 이 상태는 종종 새 데이터 흐름 만들기 직후 발생합니다. |
| 오류 | 데이터 흐름 활성화 프로세스가 중단되었음을 `Error` 나타냅니다. |

왼쪽 상단의 단계 아이콘을 선택하여 정렬합니다.

![데이터 흐름 목록](../../images/tutorials/monitor/dataflows-list.png)

정렬 패널이 나타납니다. 스크롤 메뉴에서 액세스할 소스를 선택하고 오른쪽의 목록에서 데이터 흐름을 선택합니다. 또한 줄임표(`...`) 단추를 선택하여 선택한 데이터 흐름을 위한 사용 가능한 추가 옵션을 표시할 수도 있습니다.

![데이터 흐름 정렬](../../images/tutorials/monitor/dataflows-sort.png)

데이터 **[!UICONTROL 흐름 활동]** 페이지에는 데이터 흐름 상태 및 처리 시간에 대한 정보는 물론, 수집된 레코드 및 실패한 레코드 수에 대한 자세한 정보가 포함되어 있습니다. 데이터 흐름 위의 달력 아이콘을 선택하여 통합 레코드 기간을 조정합니다.

![datflow-activity](../../images/tutorials/monitor/dataflow-activity.png)

달력에서 인제스트된 레코드의 다른 기간을 볼 수 있습니다. 지난 7일 **[!UICONTROL 또는]** 지난 30일 ****&#x200B;동안 두 개의 사전 설정 옵션 중 하나를 선택할 수 있습니다. 또는 달력을 사용하여 사용자 지정 기간을 설정할 수 있습니다. 원하는 시간대를 선택하고 적용을 **[!UICONTROL 선택하여]** 계속합니다.

![흐름 달력](../../images/tutorials/monitor/flow-calendar.png)

기본적으로 **[!UICONTROL 데이터 흐름 활동에는]** 데이터 흐름 **[!UICONTROL 과 연결된 속성]** 패널이표시됩니다. 목록에서 흐름을 선택하여 고유한 실행 ID에 대한 정보를 포함하여 관련 메타 데이터를 확인합니다.

데이터 흐름 **[!UICONTROL 실행 시작]** 을 선택하여 **[!UICONTROL 데이터 흐름 실행 개요에 액세스합니다]**.

![runs](../../images/tutorials/monitor/run-metadata.png)

데이터 흐름 **[!UICONTROL 실행 개요에는]** 데이터 흐름 **[!UICONTROL 의 메타데이터, 부분 통합]** 상태, 할당된 **[!UICONTROL 오류 임계값]**&#x200B;등 데이터 수에 대한 정보가표시됩니다. 상단 헤더에는 **[!UICONTROL 오류 요약이 포함되어 있습니다]**. 오류 **[!UICONTROL 요약에는]** 처리 과정에서 오류가 발생한 단계를 보여주는 특정 최상위 오류가 포함되어 있습니다.

![dataflow-run-overview](../../images/tutorials/monitor/dataflow-run-overview.png)

오류 요약에서 볼 수 있는 오류는 다음 표를 **[!UICONTROL 참조하십시오]**.

| 오류 | 설명 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 소스에서 데이터를 복사하는 동안 오류가 발생했습니다. |
| `CONNECTOR-2001-500` | 복사한 데이터를 처리하는 동안 오류가 발생했습니다 [!DNL Platform]. 구문 분석, 유효성 검사 또는 변환과 관련하여 이 오류가 발생할 수 있습니다. |

화면 하단에는 데이터 흐름 실행 오류에 대한 **[!UICONTROL 정보가 포함되어 있습니다]**. 여기에서 인제스트된 파일을 보거나 오류 진단을 미리 보고 다운로드하거나 파일 매니페스트를 다운로드할 수도 있습니다.

데이터 흐름 **[!UICONTROL 실행 오류]** 섹션에는 **[!UICONTROL 오류 코드]**, 실패한 레코드 수 및 오류를 설명하는 정보가 표시됩니다.

문제 **[!UICONTROL 발생]** 오류에 대한 자세한 내용을 보려면 [오류 진단 미리 보기]를 선택합니다.

![데이터 흐름 실행 오류](../../images/tutorials/monitor/dataflow-run-errors.png)

오류 **[!UICONTROL 진단 미리 보기]** 패널이 나타납니다. 이 화면에는 **[!UICONTROL 파일 이름]**, **[!UICONTROL 오류 코드]**, 오류가 발생한 열의 이름, 오류 설명 등 통합 실패와 관련된 특정 정보가 표시됩니다.

이 섹션에는 오류가 포함된 열의 미리 보기도 포함됩니다.

>[!IMPORTANT]
>
>오류 진단 미리 보기 **[!UICONTROL 를]** 활성화하려면 데이터 흐름 **[!UICONTROL 을 구성할]** 때 **[!UICONTROL 부분 섭취]** 및오류 진단을활성화해야합니다. 이렇게 하면 시스템이 흐름 실행 중에 수집되는 모든 레코드를 검색할 수 있습니다.

![미리 보기 오류 진단](../../images/tutorials/monitor/preview-error-diagnostics.png)

오류를 미리 본 후 **[!UICONTROL 데이터 흐름 실행 개요]** 패널 내에서 [다운로드 **** ]를 선택하여 전체 오류 진단에 액세스하고 파일 매니페스트를 다운로드할 수 있습니다. 자세한 내용은 [오류 진단](../../../ingestion/batch-ingestion/partial.md#retrieve-errors) 및 메타데이터 [다운로드에 대한](../../../ingestion/batch-ingestion/partial.md#download-metadata) 문서를 참조하십시오.

![미리 보기 오류 진단](../../images/tutorials/monitor/download.png)

데이터 흐름 및 섭취 모니터링에 대한 자세한 내용은 스트리밍 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오](../../../ingestion/quality/monitor-data-flows.md).

## 다음 단계

이 튜토리얼을 따라 소스 작업 영역에서 기존 계정 및 데이터 흐름 **[!UICONTROL 에]** 성공적으로 액세스했습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../profile/home.md)
- [데이터 과학 작업 공간 개요](../../../data-science-workspace/home.md)
