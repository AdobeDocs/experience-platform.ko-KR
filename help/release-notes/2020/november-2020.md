---
title: Adobe Experience Platform 릴리스 정보
description: Experience Platform 릴리스 노트
doc-type: release notes
last-update: November, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 39668013723dcda332558b74cf72b5f93db04461
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 6%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜:2020년 11월**

Adobe Experience Platform의 새로운 기능:

- [[!DNL 액세스 제어]](#access-control)
- [[!DNL 샌드박스]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 는 [Adobe Admin Console](https://adminconsole.adobe.com) 제품 프로필을 활용하여 사용자와 사용 권한 및 샌드박스를 연결합니다. 권한은 데이터 모델링, 프로필 관리, 샌드박스 관리 등 다양한 플랫폼 기능에 대한 액세스를 제어합니다.

**주요 기능**

| 기능 | 설명 |
|--- | ---|
| 권한 | 제품 프로필 내 탭 [!DNL Admin Console]에서 해당 프로필에 연결된 사용자가 사용할 수 있는 [!DNL Platform] [!DNL Platform] 기능을 사용자 지정할 수 있습니다. 사용 가능한 권한 카테고리는 다음과 같습니다. [!UICONTROL 데이터 모델링], [!UICONTROL 데이터 관리], [!UICONTROL 프로필 관리], [!UICONTROL 데이터 모니터링], 데이터 모니터링, Sandbox 관리, Identity Administration,Sandbox Administration 대상,Safety, Saffrs입니다. |
| 샌드박스 액세스 | 제품 프로필 내 **[!UICONTROL 권한]** [!DNL Platform] 탭에서 특정 샌드박스에 대한 액세스 권한을 부여할 수 있습니다. 자세한 내용은 [아래의 샌드박스](#sandboxes) 섹션을 참조하십시오. |

자세한 내용은 [액세스 제어 개요를 참조하십시오](../../access-control/home.md).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 디지털 경험 애플리케이션을 전 세계적으로 강화하도록 설계되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하면서 이러한 애플리케이션의 개발, 테스트 및 배포 요구 사항을 충족하고 운영 규정을 준수해야 합니다. 이러한 요구 사항을 해결하기 위해 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Experience Platform] [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**주요 기능**

| 기능 | 설명 |
|--- | ---|
| 프로덕션 샌드박스 | [!DNL Experience Platform] 은 삭제 또는 재설정할 수 없는 단일 프로덕션 샌드박스를 제공합니다. |
| 비프로덕션 샌드박스 | 한 인스턴스에 여러 비프로덕션 샌드박스를 만들 수 있으므로 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고 실험을 실행하고 사용자 정의 구성을 만들 수 있습니다. [!DNL Platform] |
| 샌드박스 전환기 | 사용자 [!DNL Experience Platform] 인터페이스에서 화면의 왼쪽 위 모서리에 있는 샌드박스 전환기를 사용하면 드롭다운 메뉴를 통해 사용 가능한 샌드박스 간을 전환할 수 있습니다. |
| `x-sandbox-name` header | 이제 API에 대한 모든 [!DNL Experience Platform] 호출에는 새 `x-sandbox-name` 헤더가 포함되어야 하며, 이 값은 작업이 수행될 샌드박스의 `name` 속성을 참조합니다. |

자세한 내용은 [샌드박스 개요를 참조하십시오](../../sandboxes/home.md).