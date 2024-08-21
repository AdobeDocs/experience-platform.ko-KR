---
title: Adobe Experience Platform 릴리스 노트 2024년 8월
description: Adobe Experience Platform에 대한 2024년 8월 릴리스 정보입니다.
source-git-commit: d01e16938485f6648cc02ce1674e0e9e84d78147
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 21%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2024년 8월 20일**

>[!TIP]
>
>[샘플 사용 사례 개요 설명서](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview)를 보고 조직이 Real-Time CDP을 통해 달성할 수 있는 전망, 획득 등과 같은 다양한 사용 사례에 대해 알아보십시오.

Experience Platform의 기존 기능 및 설명서에 대한 업데이트:

- [속성 기반 액세스 제어](#abac)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [ID 서비스](#identity-service)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 속성 기반 액세스 제어 {#abac}

속성 기반 액세스 제어는 Adobe Experience Platform의 기능으로, 개인 정보를 중요하게 생각하는 브랜드에게 사용자 액세스를 더 유연하게 관리할 수 있습니다. 스키마 필드 및 세그먼트와 같은 개별 객체를 사용자 역할에 할당할 수 있습니다. 이 기능을 사용하면 조직의 특정 Platform 사용자에 대해 개별 객체에 대한 액세스 권한을 부여하거나 취소할 수 있습니다.

속성 기반 액세스 제어를 통해 조직 관리자는 모든 플랫폼 워크플로 및 리소스에서 중요한 개인 데이터(SPD), 개인 식별 정보(PII) 및 기타 사용자 지정된 유형의 데이터에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

**새로운 기능**

| 기능 업데이트 | 설명 |
| --- | --- |
| 새 권한 관리자 기능 | 이제 [권한 관리자](../../access-control/abac/permission-manager/overview.md)를 사용하여 간단한 쿼리를 사용하여 보고서를 생성할 수 있습니다. 이렇게 하면 액세스 관리를 이해하고 여러 워크플로우 및 세부 기간 수준에서 액세스 권한을 확인하는 데 걸리는 시간을 절약할 수 있습니다. 사용자 및 역할에 대한 보고서를 만드는 방법에 대한 자세한 내용은 [권한 관리자 사용 안내서](../../access-control/abac/permission-manager/permissions.md)를 참조하세요. ![왼쪽 탐색 메뉴에서 사용 권한 관리자를 강조 표시하는 이미지 Experience Platform 사용자 인터페이스입니다.사용자 인터페이스의 ](assets/august/permission-manager-rn.png "권한 관리자"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

특성 기반 액세스 제어에 대한 자세한 내용은 [특성 기반 액세스 제어 개요](../../access-control/abac/overview.md)를 참조하십시오. 특성 기반 액세스 제어 워크플로에 대한 포괄적인 지침을 보려면 [특성 기반 액세스 제어 전체 안내서](../../access-control/abac/end-to-end-guide.md)를 읽어 보십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 이제 필요 시 파일을 일괄 처리 대상으로 내보낼 수 있습니다. | 이제 모든 고객이 주문형 파일을 일괄 처리 대상으로 내보낼 수 있습니다. 자세한 내용은 [전용 설명서](../../destinations/ui/export-file-now.md)를 참조하세요. |
| [예약 단계](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)에서 내보낸 여러 대상에 대한 내보내기 일정을 편집합니다. | 이제 모든 고객이 대상 활성화 워크플로의 예약 단계에서 내보낸 여러 대상에 대한 내보내기 일정을 직접 편집할 수 있는 옵션을 사용할 수 있습니다. ![예약 단계에서 일정 편집 옵션을 강조 표시하는 Experience Platform 사용자 인터페이스의 이미지입니다.](assets/august/edit-schedule.png "예약 단계에서 일정 옵션을 편집합니다."){width="250" align="center" zoomable="yes"} |
| [예약 단계](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)에서 내보낸 여러 대상에 대한 파일 이름을 편집합니다. | 이제 모든 고객이 대상 활성화 워크플로의 예약 단계에서 내보낸 여러 파일의 이름을 직접 편집할 수 있는 옵션을 사용할 수 있습니다. ![예약 단계에서 파일 이름 편집 옵션을 강조 표시하는 Experience Platform 사용자 인터페이스의 이미지입니다.](assets/august/edit-file-name.png "예약 단계에서 파일 이름 옵션을 편집합니다."){width="250" align="center" zoomable="yes"} |
| [대상 세부 정보](../../destinations/ui/destination-details-page.md#bulk-remove) 페이지의 데이터 흐름에서 여러 대상을 제거하십시오. | 이제 모든 고객이 **[!UICONTROL 대상 세부 정보]** 페이지의 기존 데이터 흐름에서 여러 대상을 제거하는 옵션을 사용할 수 있습니다. ![대상 세부 정보 페이지에서 대상 제거 옵션을 강조 표시하는 Experience Platform 사용자 인터페이스 이미지.](assets/august/bulk-remove-audiences.png "대상 세부 정보 페이지에서 대상 제거 옵션을 선택하십시오."){width="250" align="center" zoomable="yes"} |
| [대상 세부 정보](../../destinations/ui/destination-details-page.md#bulk-export) 페이지에서 요청 시 여러 파일을 일괄 처리 대상으로 내보냅니다. | 이제 모든 고객이 **[!UICONTROL 대상 세부 정보]** 페이지에서 여러 파일을 요청 시 배치 대상으로 내보내는 옵션을 사용할 수 있습니다. ![대상 세부 정보 페이지에서 지금 파일 내보내기 옵션을 강조 표시하는 Experience Platform 사용자 인터페이스 이미지입니다.](assets/august/bulk-export-file-now.png "대상 세부 정보 페이지의 지금 파일 내보내기 옵션."){width="250" align="center" zoomable="yes"} |
| [대상 세부 정보](../../destinations/ui/destination-details-page.md#bulk-edit-file-names) 페이지에서 내보낸 여러 대상에 대한 파일 이름을 편집합니다. | 이제 **[!UICONTROL 대상 세부 정보]** 페이지에서 내보낸 여러 파일의 이름을 직접 편집할 수 있습니다. ![대상 세부 정보 페이지에서 파일 이름 편집 옵션을 강조 표시하는 Experience Platform 사용자 인터페이스 이미지.](assets/august/edit-file-name-destination-details.png "대상 세부 정보 페이지의 파일 이름 편집 옵션입니다."){width="250" align="center" zoomable="yes"} |
| [대상 세부 정보](../../destinations/ui/export-datasets.md#remove-dataset) 페이지의 데이터 흐름에서 여러 데이터 세트를 제거하십시오. | 이제 모든 고객이 데이터 흐름에서 여러 데이터 세트를 제거하는 옵션을 사용할 수 있습니다. ![대상 세부 정보 페이지에서 데이터 세트 제거 옵션을 강조 표시하는 Experience Platform 사용자 인터페이스 이미지입니다.](assets/august/bulk-remove-datasets.png "대상 세부 정보 페이지에서 데이터 세트 제거 옵션을 선택하십시오."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하세요.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| ML 지원 스키마 생성 흐름 | 고급 머신 러닝 알고리즘을 사용하여 샘플 데이터 파일을 분석하고 표준 및 사용자 지정 필드를 사용하여 최적화된 스키마를 자동으로 생성합니다.<br>주요 기능:<br><ul><li>더 빠른 스키마 생성: ML이 권장하고 생성한 XDM 필드를 사용하여 샘플 데이터 파일에서 직접 스키마를 생성합니다.</li><li>유연한 스키마 발전: 생성된 스키마에서 필드를 쉽게 추가하거나 업데이트할 수 있습니다.</li><li>매끄러운 통합: 스키마 Ul의 핵심 스키마 생성 흐름과 완전히 통합되어 유연하고 일관된 사용자 경험을 보장합니다.</li><li>효율적인 검토 및 편집: 플랫 뷰 편집기를 사용하여 스키마를 빠르게 보고 업데이트하므로 작성 프로세스가 보다 효율적이고 사용자 친화적입니다.</li></ul><br>자세한 내용은 [ML 지원 스키마 만들기 워크플로우 가이드](../../xdm/ui/ml-assisted-schema-creation.md)를 참조하세요. |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## ID 서비스 {#identity-service}

Adobe Experience Platform Identity Service를 사용하여 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 포괄적인 보기를 만들고, 이를 통해 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**업데이트된 설명서**

| 기능 | 설명 |
| --- | --- |
| 그래프 구성 안내서 | ID 그래프 연결 규칙 및 ID 데이터를 사용하는 동안 발생할 수 있는 일반적인 그래프 시나리오에 대한 자세한 내용은 [그래프 구성 안내서](../../identity-service/identity-graph-linking-rules/example-configurations.md)를 참조하십시오. 그래프 구성 안내서는 간단한 1인 그래프 시나리오에서 복잡하고 계층적인 다인 그래프 시나리오에 이르기까지 다양한 예를 제공합니다. 또한 [그래프 시뮬레이션 UI](../../identity-service/identity-graph-linking-rules/graph-simulation.md)에서 입력할 수 있는 이벤트 및 알고리즘 구성의 예제와 특정 그래프 시나리오가 주어지면 기본 ID를 선택하는 방법에 대한 분류에 대해 안내서를 사용할 수 있습니다. |

{style="table-layout:auto"}

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 수집 세부 정보 | 사용자 지정 업로드 원본을 사용하는 대상의 경우 대상 세부 정보 페이지에서 대상의 수집에 대한 세부 정보를 보다 포괄적으로 볼 수 있습니다. 또한 스키마를 선택하고 레이블 지정에 대해 원하는 속성을 선택하여 페이로드 속성에 레이블을 적용할 수 있습니다. 수집 세부 정보 섹션에 대한 자세한 내용은 [Audience Portal 안내서](../../segmentation/ui/audience-portal.md#ingestion-details)를 참조하십시오. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션이나 타사 데이터 소스에서 데이터를 수집합니다.

**업데이트된 설명서**

| 업데이트된 설명서 | 설명 |
| --- | --- |
| 데이터 흐름 업데이트에 대한 확장된 설명서 | 기존 데이터 흐름에서 수행할 수 있는 다양한 구성에 대한 자세한 정보를 제공하기 위해 [UI에서 기존 원본 데이터 흐름을 업데이트하는 중](../../sources/tutorials/ui/update-dataflows.md)에 대한 안내서를 업데이트했습니다. 비활성화된 데이터 흐름이 다시 활성화될 때 예상되는 동작을 명확하게 하도록 안내서도 업데이트되었습니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
