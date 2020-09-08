---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;data flows
description: Adobe Experience Platform의 소스 커넥터는 예약된 기준으로 외부 소스 데이터를 인제스트하는 기능을 제공합니다. 이 자습서에서는 소스 작업 영역에서 기존 계정 및 데이터 흐름을 보는 단계를 제공합니다.
solution: Experience Platform
title: 계정 및 데이터 흐름 모니터링
topic: overview
translation-type: tm+mt
source-git-commit: e5898da7d25a708f3431b251f1cfa620b943e9a5
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

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

![계정 선택](../../images/tutorials/monitor/accounts-sort.png)

계정 **[!UICONTROL 페이지에서]** 액세스한 계정과 연결된 기존 데이터 흐름 또는 대상 데이터 집합 목록을 볼 수 있습니다.

![데이터 흐름](../../images/tutorials/monitor/dataflows.png)

## 데이터 흐름 모니터링

데이터 파일은 계정을 보지 않고도 **[!UICONTROL 카탈로그]** 페이지에서 직접 액세스할 수 **[!UICONTROL 있습니다]**. 상단 헤더에서 **[!UICONTROL 데이터 흐름]** 을 선택하여 기존 데이터 흐름 목록을 봅니다.

![카탈로그 데이터 흐름](../../images/tutorials/monitor/catalog-dataflows.png)

기존 데이터 흐름 목록이 나타납니다. 이 페이지에서는 소스, 사용자 이름, 데이터 흐름 수 및 상태에 대한 정보를 비롯하여 볼 수 있는 데이터 흐름 목록이 있습니다. 왼쪽 상단의 단계 아이콘을 선택하여 정렬합니다.

![데이터 흐름 목록](../../images/tutorials/monitor/dataflows-list.png)

정렬 패널이 나타납니다. 스크롤 메뉴에서 액세스할 소스를 선택하고 오른쪽의 목록에서 데이터 흐름을 선택합니다.

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

오류 요약에서 볼 수 있는 오류 코드는 다음 표를 **[!UICONTROL 참조하십시오]**.

| 오류 코드 | 오류 메시지 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | &quot;복사 활동에 문제가 발생했습니다.&quot; |
| `CONNECTOR-2001-500` | &quot;Experience Platform 소스에서 데이터 세트로 복사하는 동안 문제가 발생했습니다.&quot; |
| `CONNECTOR-3001-500` | &quot;벌크 인제스트 API를 사용하여 일괄 처리를 만드는 동안 흐름 공급자에 문제가 발생했습니다.&quot; |

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
