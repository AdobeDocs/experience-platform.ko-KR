---
keywords: Experience Platform;홈;인기 항목;샌드박스 개발자 안내서
solution: Experience Platform
title: 샌드박스 API 안내서
description: Adobe Experience Platform의 샌드박스는 프로덕션 환경에 영향을 주지 않고 기능을 테스트하고 실험을 실행하며 사용자 지정 구성을 만들 수 있는 격리된 개발 환경을 제공합니다.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# [!DNL Sandbox] API 안내서

[!DNL Sandbox] API는 조직 내에서 사용할 수 있는 모든 샌드박스를 프로그래밍 방식으로 관리할 수 있는 여러 끝점을 제공합니다. 이러한 엔드포인트는 아래에 요약되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 참조하고 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보는 [시작 안내서](./getting-started.md)를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [[!DNL Sandbox] API 참조](https://www.adobe.io/experience-platform-apis/references/sandbox)를 방문하세요.

## 사용 가능한 샌드박스

사용 가능한 샌드박스 엔드포인트를 사용하면 각 샌드박스의 이름, 제목, 상태, 유형 및 지역에 대한 정보를 포함하여 현재 사용자가 사용할 수 있는 모든 사용 가능한 샌드박스 목록을 볼 수 있습니다. [!DNL Sandbox] API의 사용 가능한 샌드박스 끝점은 샌드박스 관리 액세스 권한이 없는 사용자를 포함하여 모든 사용자가 액세스할 수 있습니다. API에서 사용 가능한 샌드박스를 보는 방법은 [사용 가능한 샌드박스 끝점 안내서](./available.md)를 참조하세요.

## 샌드박스 관리

샌드박스는 Adobe Experience Platform의 단일 인스턴스 내에 있는 가상 파티션으로, 디지털 경험 애플리케이션의 개발 프로세스와 매끄럽게 통합할 수 있습니다. `/sandboxes` 끝점을 사용하여 프로덕션 및 개발 샌드박스를 만들고, 보고, 편집하고, 재설정하고, 삭제할 수 있습니다. 이 끝점을 사용하는 방법을 알아보려면 [샌드박스 끝점 안내서](./sandboxes.md)를 참조하세요.

## 샌드박스 유형

현재 Experience Platform에서 지원되는 샌드박스 유형은 프로덕션 및 개발 샌드박스입니다. 기본 Experience Platform 라이선스는 프로덕션 또는 개발로 분류할 수 있는 총 5개의 샌드박스를 부여합니다. 추가 팩 10개, 최대 총 75개의 샌드박스에 대해 라이센스를 부여할 수 있습니다. API에서 조직에 대해 지원되는 샌드박스 유형을 보는 방법은 [샌드박스 유형 끝점 안내서](./types.md)를 참조하십시오.

## 다음 단계

[!DNL Sandbox] API를 사용하여 호출을 시작하려면 [시작 안내서](./getting-started.md)를 읽은 다음 끝점 안내서 중 하나를 선택하여 특정 끝점을 사용하는 방법을 알아보세요.
