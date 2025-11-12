---
title: PathFactory Source 개요
description: API 또는 사용자 인터페이스를 사용하여 PathFactory를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 3%

---

# [!DNL PathFactory]

[[!DNL PathFactory]](https://www.pathfactory.com/)은(는) 비즈니스가 지능형 콘텐츠 인사이트를 통해 콘텐츠 여정을 관리하고 참여를 유도하는 데 도움이 되는 클라우드 기반 플랫폼을 제공합니다. 이 안내서에서는 최적의 데이터 수집을 위해 PathFactory의 커넥터를 활용하여 PathFactory의 데이터를 Experience Platform에 통합하는 방법에 대해 자세히 설명합니다.

다음 세 가지 기본 소스를 사용하여 [[!DNL PathFactory]](https://www.pathfactory.com/)에서 데이터를 수집할 수 있습니다.

* **[!DNL Visitors]**: 고객 및 연락처 데이터를 레코드로 수집하여 대상자를 더 잘 이해할 수 있습니다.
* **[!DNL Sessions]**: 플랫폼에서 개별 사용자 세션 활동을 추적하는 시계열 이벤트입니다.
* **[!DNL Page Views]**: 보고 있는 페이지에 대한 통찰력을 제공하여 콘텐츠 성능을 분석하는 데 도움이 되는 시계열 이벤트입니다.

[!DNL PathFactory] 소스 계정을 설정하는 방법에 대한 자세한 내용은 아래 문서를 참조하십시오.

## 허용 목록에 추가하다 IP 주소 {#ip-allow-list}

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

## 전제 조건 {#prerequisites}

[[!DNL PathFactory]](https://www.pathfactory.com/) 커넥터를 Experience Platform과 통합하기 전에 다음 전제 조건을 충족하는지 확인하십시오.

* **[PathFactory 계정]**&#x200B;입니다.
   * 올바른 계정이 아직 없는 경우 [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml)에 문의하세요.
* **제품에 대한**&#x200B;활성 구독[!DNL PathFactory].
* **사용자 이름, 암호 및 도메인**.
   * [!DNL PathFactory] 계정 및 해당 데이터에 액세스하려면 이러한 자격 증명이 필요합니다.
* **액세스 토큰** 및 **API 끝점**.
   * [!DNL PathFactory] API에 연결하는 데 필요합니다.

### 자격 증명을 획득하고 토큰에 액세스하는 방법 {#gather-credentials}

[!DNL PathFactory]을(를) Experience Platform에 연결하려면 다음 자격 증명을 제공해야 합니다.

| 자격 증명 | 설명 | 엔드포인트 |
| --- | --- | --- |
| 사용자 이름 | [!DNL PathFactory] 계정 사용자 이름입니다. | 적용할 수 없음 |
| 암호 | [!DNL PathFactory] 계정 암호입니다. | 적용할 수 없음 |
| 도메인 | [!DNL PathFactory] 계정과 연결된 도메인입니다. | 적용할 수 없음 |
| 액세스 토큰 | API 인증에 사용되는 고유한 토큰입니다. | 적용할 수 없음 |
| 방문자 엔드포인트 | 방문자 데이터에 대한 API 엔드포인트. | `/api/public/v3/data_lake_apis/visitors.json` |
| 세션 끝점 | 세션 데이터에 대한 API 엔드포인트. | `/api/public/v3/data_lake_apis/sessions.json` |
| 페이지 조회수 엔드포인트 | 페이지 보기 데이터에 대한 API 엔드포인트. | `/api/public/v3/data_lake_apis/page_views.json` |

사용자 이름, 암호, 도메인 및 액세스 토큰을 얻는 방법에 대한 자세한 지침은 [[!DNL PathFactory] 지원 센터](https://support.pathfactory.com/categories/adobe/)를 참조하십시오. 이 리소스는 자격 증명 검색 및 관리에 대한 포괄적인 안내서를 제공합니다.

### Experience Platform에 대한 권한 구성

**[!UICONTROL View Sources]** 계정을 Experience Platform에 연결하려면 계정에 대해 **[!UICONTROL Manage Sources]** 및 [!DNL PathFactory] 권한이 모두 활성화되어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

## Experience Platform에 [!DNL PathFactory] 연결 {#pathfactory-connect}

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL PathFactory]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [API를 사용하여  [!DNL PathFactory] 데이터를 Experience Platform으로 가져오기](../../tutorials/api/create/marketing-automation/pathfactory.md)할 원본 연결 및 데이터 흐름을 만듭니다.
* [UI를 사용하여  [!DNL PathFactory] 계정을 Experience Platform에 연결](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [UI를 사용하여 원본 연결에 대한 데이터 흐름을 만듭니다](../../tutorials/ui/dataflow/marketing-automation.md).
