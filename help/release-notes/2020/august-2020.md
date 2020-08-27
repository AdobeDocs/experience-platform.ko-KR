---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 8월 12일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL 데이터 과학 작업 공간]](#dsw)
- [[!DNL 대상]](#destinations)
- [[!DNL 소스]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 머신 러닝과 인공 지능(AI)을 사용하여 데이터에서 인사이트를 도출합니다. Adobe Experience Platform에 통합되어 Adobe 솔루션에서 콘텐츠와 데이터 자산을 사용하여 예측할 수 [!DNL Data Science Workspace] 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| VM의 [!DNL JupyterLab] | 장기 실행 [!DNL JupyterLab notebook] 가상 시스템의 안정성이 개선되었습니다. |

자세한 내용 [!DNL JupyterLab]은 [[!DNL JupyterLab] 사용 안내서를 참조하십시오](../../data-science-workspace/jupyterlab/overview.md).

## 대상 {#destinations}

Adobe의 실시간 고객 데이터 플랫폼 [](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새 대상**

Adobe Experience Platform 데이터를 활성화할 수 있는 새로운 대상을 사용할 수 있습니다. 자세한 내용은 아래를 참조하십시오.

| 대상 | 설명 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 다음과 같은 Google 소유 및 운영 자산에서 고객에게 도달하고 재참여할 수 있습니다. [!DNL Search], [!DNL Shopping], Gmail 및 YouTube. <br><br> 대상 카탈로그의 [!DNL Google Customer Match] 페이지 [](/help/rtcdp/destinations/google-customer-match-destination.md) 를 방문하여 대상 및 Adobe 실시간 CDP에서 대상을 설정하는 방법에 대한 자세한 내용을 확인하십시오. |

**새로운 기능**

| 기능 | 설명 |
|------- | -----------|
| 사용자 정의 파일 이름 편집기 | 내보낸 파일의 이름을 편집할 수 있는 이메일 마케팅 대상 및 클라우드 스토리지 대상에 대한 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 정품 인증 워크플로우의 [ 구성 단계를](/help/rtcdp/destinations/activate-destinations.md#configure) 참조하십시오. |
| 권장 속성 | 내보낸 파일에 추가할 수 있는 권장 특성을 표시하는 이메일 마케팅 대상 및 클라우드 스토리지 대상에 대한 데이터 활성화 워크플로우로 업데이트합니다. 자세한 내용은 정품 인증 워크플로우의 [속성 선택 단계를](/help/rtcdp/destinations/activate-destinations.md#select-attributes) 참조하십시오. |

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있으며, [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고, 통합 실행에 대한 시간을 설정하고, 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 흐름 실행 모니터링 | 사용자는 모든 흐름 실행을 모니터링하고 완료 상태, 실행 기간, 처리된 파일 목록, 오류 및 지표를 포함하여 각 실행에 대한 세부 보기를 볼 수 있습니다. 자세한 내용은 데이터 흐름 [모니터링](../../sources/tutorials/ui/monitor.md) 문서를 참조하십시오. |
| 흐름 실행 알림 | 사용자는 이벤트에 구독하고 웹 후크를 등록하여 흐름 실행에 대한 상태, 지표 및 오류에 대한 실시간 알림을 받을 수 있습니다. |
| 향상된 UI 카탈로그 | 선택한 개체의 기본 작업에 보다 쉽게 액세스할 수 있도록 소스 카탈로그 화면에 대한 업데이트 |

소스에 대한 자세한 내용은 [소스 개요를 참조하십시오](../../sources/home.md).
