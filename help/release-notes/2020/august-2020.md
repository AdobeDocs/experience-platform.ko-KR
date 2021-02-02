---
title: Adobe Experience Platform 릴리스 노트
description: 2020년 8월 10일 Experience Platform 릴리스 노트
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 7%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 12월 8일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 머신 러닝과 인공 지능을 사용하여 데이터에서 인사이트를 도출합니다. Adobe Experience Platform에 통합된 [!DNL Data Science Workspace]은(는) Adobe 솔루션에서 컨텐츠와 데이터 자산을 사용하여 예측하는 데 도움이 됩니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL JupyterLab]의 VM 개선 사항 | 장시간 실행되는 [!DNL JupyterLab notebook] 가상 컴퓨터의 안정성이 개선되었습니다. |

[!DNL JupyterLab]에 대한 자세한 내용은 [[!DNL JupyterLab] 사용자 안내서](../../data-science-workspace/jupyterlab/overview.md)를 참조하십시오.

## 대상 {#destinations}

[실시간 고객 데이터 플랫폼](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로, 데이터를 해당 파트너에게 원활하게 활성화할 수 있습니다.

**새 대상**

Adobe Experience Platform 데이터를 활성화할 수 있는 새 대상을 사용할 수 있습니다. 자세한 내용은 아래를 참조하십시오.

| 대상 | 설명 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 다음과 같이 Google의 소유물 및 운영 자산에서 고객에게 도달하고 다시 참여할 수 있습니다.[!DNL Search], [!DNL Shopping], Gmail 및 YouTube. <br><br> 대상  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) 및 실시간 CDP에서 대상을 설정하는 방법에 대한 자세한 내용은 대상 카탈로그의 페이지를 참조하십시오. |

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 사용자 정의 파일 이름 편집기 | 내보낸 파일의 이름을 편집할 수 있는 이메일 마케팅 대상 및 클라우드 스토리지 대상에 대한 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 정품 인증 워크플로우에서 [ 단계 구성](../../destinations/ui/activate-destinations.md#configure)을 참조하십시오. |
| 권장 특성 | 내보낸 파일에 추가할 수 있는 권장 특성을 표시하는 이메일 마케팅 대상 및 클라우드 스토리지 대상에 대한 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 정품 인증 워크플로우에서 [특성 선택 단계](../../destinations/ui/activate-destinations.md#select-attributes)을 참조하십시오. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

실시간 고객 데이터 플랫폼([!DNL Real-time CDP])은 Experience Platform을 기반으로 구축된 실시간 고객 데이터 플랫폼(MVT)을 기반으로 기업이 알려진 데이터와 알 수 없는 데이터를 통합하여 고객 여정 전반에 걸쳐 지능적인 의사 결정이 있는 고객 프로파일을 활성화할 수 있도록 도와줍니다. [!DNL Real-time CDP] 여러 엔터프라이즈 데이터 소스를 통합하여 고객 프로파일을 실시간으로 생성 그런 다음 이러한 프로필에서 작성한 세그먼트를 다운스트림 대상으로 전송하여 모든 채널 및 디바이스에서 일대일 개인화된 고객 경험을 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| IAB TCF 2.0 지원 | [!DNL Real-time CDP] 는 이제  [!DNL Transparency & Consent Framework] (IAB)에서 설명한 바와 같이 2.0 버전의  [!DNL Interactive Advertising Bureau] (TCF)에 대해 등록된 공급자입니다. 다운스트림 대상으로 세그먼트를 활성화할 때 데이터 작업 및 프로필 스키마를 구성하여 CMP에서 생성된 고객 동의 데이터를 수용하고 고객의 동의 기본 설정을 적용할 수 있습니다. |

[!DNL Real-time CDP]에 대한 자세한 내용은 [[!DNL Real-time CDP] 개요](../../rtcdp/overview.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 동시에 [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 흐름 실행 모니터링 | 사용자는 모든 흐름 실행을 모니터링하고 완료 상태, 실행 기간, 처리된 파일 목록, 오류 및 지표를 포함하여 각 실행에 대한 세부 보기를 볼 수 있습니다. 자세한 내용은 [데이터 흐름 모니터링](../../sources/tutorials/ui/monitor.md) 문서를 참조하십시오. |
| 흐름 실행 알림 | 사용자는 이벤트에 구독하고 웹 후크를 등록하여 흐름 실행에 대한 상태, 지표 및 오류에 대한 실시간 알림을 받을 수 있습니다. |
| 향상된 UI 카탈로그 | 선택한 객체의 기본 작업에 보다 쉽게 액세스할 수 있도록 소스 카탈로그 화면에 대한 업데이트를 제공합니다. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.