---
keywords: Experience Platform;홈;인기 항목;샌드박스 개발자 안내서
solution: Experience Platform
title: 샌드박스 API 안내서
topic-legacy: developer guide
description: Adobe Experience Platform의 샌드박스는 프로덕션 환경에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 만들 수 있는 분리된 개발 환경을 제공합니다.
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Sandbox] API 안내서

[!DNL Sandbox] API는 IMS 조직 내에서 사용할 수 있는 모든 샌드박스를 프로그래밍 방식으로 관리할 수 있도록 해주는 몇 가지 엔드포인트를 제공합니다. 이러한 엔드포인트는 아래에 요약되어 있습니다. 자세한 내용은 개별 종단점 안내서를 방문하여 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 보려면 [시작 안내서](./getting-started.md)를 참조하십시오.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [[!DNL Sandbox] API 참조](https://www.adobe.io/experience-platform-apis/references/sandbox)를 방문하십시오.

## 사용 가능한 샌드박스

사용 가능한 샌드박스 종단점을 사용하면 각 샌드박스의 이름, 제목, 상태, 유형 및 영역에 대한 정보를 포함하여 현재 사용자가 사용할 수 있는 모든 샌드박스 목록을 볼 수 있습니다. [!DNL Sandbox] API의 사용 가능한 샌드박스 종단점은 샌드박스 관리 액세스 권한이 없는 사용자를 비롯하여 모든 사용자가 액세스할 수 있습니다. API에서 사용 가능한 샌드박스를 보는 방법을 알려면 [사용 가능한 샌드박스 엔드포인트 안내서](./available.md)를 참조하십시오.

## 샌드박스 관리

샌드박스는 Adobe Experience Platform의 단일 인스턴스 내에 있는 가상 파티션으로, 디지털 경험 애플리케이션의 개발 프로세스와의 원활한 통합을 지원합니다. `/sandboxes` 종단점을 사용하여 프로덕션 및 개발 샌드박스를 생성, 보기, 편집, 재설정 및 삭제할 수 있습니다. 이 종단점을 사용하는 방법에 대한 자세한 내용은 [샌드박스 종단점 안내서](./sandboxes.md)를 참조하십시오.

## 샌드박스 유형

현재 Experience Platform에서 지원되는 샌드박스 유형은 프로덕션 및 개발 샌드박스입니다. 기본 플랫폼 라이센스는 총 5개의 샌드박스를 제공하며 이를 프로덕션 또는 개발용으로 분류할 수 있습니다. 샌드박스 10개를 추가로 라이센스를 최대 75개의 샌드박스로 추가 구매할 수 있습니다. API에서 조직에 대해 지원되는 샌드박스 유형을 보는 방법은 [샌드박스 유형 엔드포인트 가이드](./types.md) 를 참조하십시오.

## 다음 단계

[!DNL Sandbox] API를 사용하여 호출을 시작하려면 [시작 안내서](./getting-started.md)를 읽은 다음 엔드포인트 가이드 중 하나를 선택하여 특정 엔드포인트를 사용하는 방법을 알아봅니다.