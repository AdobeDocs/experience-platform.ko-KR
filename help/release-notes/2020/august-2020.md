---
title: Adobe Experience Platform 릴리스 노트 2020년 8월
description: Adobe Experience Platform에 대한 2020년 8월 릴리스 정보입니다.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 23%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2020년 8월 12일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace]은(는) 머신 러닝 및 인공 지능을 사용하여 데이터에서 통찰력을 제공합니다. Adobe Experience Platform에 통합된 [!DNL Data Science Workspace]은(는) Adobe 솔루션 전반에서 사용자의 콘텐츠 및 데이터 자산을 사용하여 예측을 수행하는 데 도움이 됩니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL JupyterLab]의 VM 개선 사항 | 오래 실행되는 [!DNL JupyterLab notebook] 가상 컴퓨터의 안정성을 개선했습니다. |

[!DNL JupyterLab]에 대한 자세한 내용은 [[!DNL JupyterLab] 사용 안내서](../../data-science-workspace/jupyterlab/overview.md)를 참조하세요.

## 대상 {#destinations}

[Real-Time Customer Data Platform](../../rtcdp/overview.md)에서 대상은 해당 파트너에게 데이터를 원활하게 활성화하는 대상 플랫폼과의 사전 빌드된 통합입니다.

**새로운 대상**

Adobe Experience Platform 데이터를 활성화할 수 있는 새 대상을 사용할 수 있습니다. 자세한 내용은 아래를 참조하십시오.

| 대상 | 설명 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 [!DNL Search], [!DNL Shopping], Gmail 및 YouTube과 같은 Google의 소유 및 운영되는 속성에서 고객에게 연락하고 다시 연결할 수 있습니다. <br><br> 대상 카탈로그의 [!DNL Google Customer Match] [페이지](../../destinations/catalog/advertising/google-customer-match.md)를 방문하여 대상 및 Real-Time CDP 설정 방법에 대한 자세한 내용을 확인하십시오. |

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 사용자 정의 파일 이름 편집기 | 내보낸 파일의 이름을 편집할 수 있는 이메일 마케팅 대상 및 클라우드 스토리지 대상의 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 활성화 워크플로에서 [구성 단계](../../destinations/ui/activate-batch-profile-destinations.md)를 참조하세요. |
| 권장 속성 | 내보낸 파일에 추가할 권장 속성을 표시하는 이메일 마케팅 대상 및 클라우드 스토리지 대상의 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 활성화 워크플로에서 [특성 선택 단계](../../destinations/ui/activate-batch-profile-destinations.md)를 참조하세요. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Experience Platform을 기반으로 구축된 Real-Time Customer Data Platform([!DNL Real-Time CDP])으로 기업은 알려진 데이터와 알 수 없는 데이터를 수집하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로필을 활성화할 수 있습니다. [!DNL Real-Time CDP]는 여러 기업의 데이터 소스를 결합하여 실시간으로 고객 프로필을 생성합니다. 이러한 프로필에서 구축된 세그먼트는 다운스트림 대상으로 전송되어 모든 채널과 디바이스에서 일대일로 개인 설정된 고객 경험을 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| IAB TCF 2.0 지원 | [!DNL Real-Time CDP]은(는) IAB([!DNL Interactive Advertising Bureau])에 의해 요약된 대로 TCF([!DNL Transparency & Consent Framework])의 2.0 버전에 대해 등록된 공급업체입니다. CMP에서 생성된 고객 동의 데이터를 수락하도록 데이터 작업 및 프로필 스키마를 구성하고, 세그먼트를 다운스트림 대상으로 활성화할 때 고객의 동의 환경 설정을 적용할 수 있습니다. |

[!DNL Real-Time CDP]에 대한 자세한 내용은 [[!DNL Real-Time CDP] 개요](../../rtcdp/overview.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 [!DNL Experience Platform] 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform]에서는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 흐름 실행 모니터링 | 사용자는 모든 플로우 실행을 모니터링하고 완료 상태, 실행 기간, 처리된 파일 목록, 오류 및 지표를 포함하여 각 실행에 대한 세부 보기를 확인할 수 있습니다. 자세한 내용은 [데이터 흐름 모니터링](../../sources/tutorials/ui/monitor.md) 문서를 참조하십시오. |
| 플로우 실행 알림 | 사용자는 이벤트를 구독하고 웹후크를 등록하여 흐름 실행과 관련된 상태, 지표 및 오류에 대한 실시간 알림을 받을 수 있습니다. |
| UI 카탈로그 개선 사항 | 선택한 객체의 기본 작업에 쉽게 액세스할 수 있도록 소스 카탈로그 화면이 업데이트되었습니다. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.
