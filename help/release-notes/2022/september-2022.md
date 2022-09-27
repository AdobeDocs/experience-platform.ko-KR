---
title: Adobe Experience Platform 릴리스 노트 - 2022년 9월
description: Adobe Experience Platform에 대한 2022년 9월 릴리스 노트입니다.
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 7%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 9월 28일**

Adobe Experience Platform의 기존 기능 업데이트:

- [ID 서비스](#identity-service)
- [소스](#sources)

## ID 서비스 {#identity-service}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 서로 다른 시스템에서 고객 데이터가 단편화된 경우 각 고객이 여러 &quot;ID&quot;를 보유한 것처럼 보일 때 더욱 어렵습니다.

Adobe Experience Platform Identity 서비스를 사용하면 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 해당 행동을 더 잘 볼 수 있으므로 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 집합 삭제 지원 | 이제 ID 서비스는 를 통해 요청할 때 데이터 세트 삭제를 지원합니다 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI 또는 데이터 위생입니다. 안내서 읽기 [UI에서 데이터 세트 삭제](../../catalog/datasets/user-guide.md#delete-a-dataset) 추가 정보. |

ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Audience Manager 세그먼트 모집단이 실시간 고객 프로필에 미치는 영향 | 크기 조정 가능한 Audience Manager 세그먼트 모집단을 수집하면 Audience Manager 소스를 사용하여 처음 Audience Manager 세그먼트를 Platform으로 보낼 때 총 프로필 수에 직접적인 영향을 줍니다. 즉, 모든 세그먼트를 선택하면 라이센스 사용 권한을 초과하는 프로필 수가 발생할 수 있습니다. 자세한 내용은 [Audience Manager 소스 개요](../../sources/connectors/adobe-applications/audience-manager.md). 라이센스 사용에 대한 자세한 내용은 [라이선스 사용 대시보드 사용](../../dashboards/guides/license-usage.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).