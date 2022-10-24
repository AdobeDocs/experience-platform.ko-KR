---
title: Adobe Experience Platform 릴리스 노트 - 2020년 8월
description: Adobe Experience Platform에 대한 2020년 8월 릴리스 노트입니다.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 8월 12일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 에서는 기계 학습 및 인공 지능을 사용하여 데이터로부터 통찰력을 제공합니다. Adobe Experience Platform에 통합, [!DNL Data Science Workspace] 은 Adobe 솔루션에서 콘텐츠 및 데이터 자산을 사용하여 예측을 하는 데 도움이 됩니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 향상된 VM [!DNL JupyterLab] | 장기 실행 안정성을 개선했습니다. [!DNL JupyterLab notebook] 가상 시스템. |

자세한 내용은 [!DNL JupyterLab]를 보려면 [[!DNL JupyterLab] 사용 안내서](../../data-science-workspace/jupyterlab/overview.md).

## 대상 {#destinations}

in [Real-time Customer Data Platform](../../rtcdp/overview.md), 대상은 대상 플랫폼과의 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새 대상**

새 대상은 Adobe Experience Platform 데이터를 활성화할 수 있는 곳입니다. 자세한 내용은 아래를 참조하십시오.

| 대상 | 설명 |
|--- | ---|
| [!DNL Google Customer Match] | Google 고객 일치 기능을 사용하면 온라인 및 오프라인 데이터를 사용하여 다음과 같이 Google이 소유하거나 운영하는 속성에서 고객에게 도달하고 다시 참여하도록 할 수 있습니다. [!DNL Search], [!DNL Shopping], Gmail 및 YouTube. <br><br> 다음 방문 [!DNL Google Customer Match] [페이지](../../destinations/catalog/advertising/google-customer-match.md) 대상 카탈로그에서 대상 및 Real-Time CDP에서 설정하는 방법에 대한 자세한 내용을 참조하십시오. |

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 사용자 지정 파일 이름 편집기 | 내보낸 파일의 이름을 편집할 수 있는 이메일 마케팅 대상 및 클라우드 스토리지 대상에 대한 데이터 활성화 워크플로우를 업데이트합니다. 자세한 내용은 [ 단계 구성](../../destinations/ui/activate-batch-profile-destinations.md) 활성화 워크플로우에서 생성합니다. |
| 권장 속성 | 내보낸 파일에 추가할 권장 속성을 표시하는 이메일 마케팅 대상 및 클라우드 스토리지 대상에 대한 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 [속성 선택 단계](../../destinations/ui/activate-batch-profile-destinations.md) 활성화 워크플로우에서 생성합니다. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Experience Platform, Real-time Customer Data Platform(영어) 기본 제공[!DNL Real-Time CDP])은 회사에서 알려진 데이터와 알 수 없는 데이터를 함께 가져와서 고객 여정 전체에서 지능형 의사 결정을 사용하여 고객 프로필을 활성화하는 데 도움이 됩니다. [!DNL Real-Time CDP] 여러 엔터프라이즈 데이터 소스를 결합하여 고객 프로필을 실시간으로 만듭니다. 그런 다음 이러한 프로필에서 작성한 세그먼트를 다운스트림 대상으로 전송하여 모든 채널 및 장치에서 개인화된 고객 경험을 일대일로 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| IAB TCF 2.0 지원 | [!DNL Real-Time CDP] 는 이제 2.0 버전의 [!DNL Transparency & Consent Framework] (TCF), [!DNL Interactive Advertising Bureau] (IAB). CMP에서 생성한 고객 동의 데이터를 수락하도록 데이터 작업 및 프로필 스키마를 구성하고, 세그먼트를 다운스트림 대상으로 활성화할 때 고객의 동의 환경 설정을 적용할 수 있습니다. |

자세한 내용은 [!DNL Real-Time CDP]를 참조하고 [[!DNL Real-Time CDP] 개요](../../rtcdp/overview.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 흐름 실행 모니터링 | 사용자는 모든 플로우 실행을 모니터링하고 완료 상태, 실행 기간, 처리된 파일 목록, 오류 및 지표를 포함하여 각 실행에 대한 세부 보기를 볼 수 있습니다. 자세한 내용은 [데이터 흐름 모니터링](../../sources/tutorials/ui/monitor.md) 문서 를 참조하십시오. |
| 흐름 실행 알림 | 사용자는 이벤트에 가입하고 웹 후크를 등록하여 흐름 실행과 관련된 상태, 지표 및 오류에 대한 실시간 알림을 받을 수 있습니다. |
| UI 카탈로그 개선 사항 | 선택한 객체의 기본 작업에 쉽게 액세스할 수 있도록 소스 카탈로그 화면에 대한 업데이트. |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
