---
title: Adobe Experience Platform 릴리스 노트 2022년 2월
description: Adobe Experience Platform의 2022년 2월 릴리스 정보.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 16%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2022년 3월 7일 화요일**

>[!NOTE]
>
>이번 릴리스는 원래 날짜인 2월 23일에서 3월 7일로 변경되었습니다.

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform에서는 매일 스냅숏 중에 캡처된 조직 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 [!DNL dashboards]을(를) 제공합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 새로운 표준 대상 위젯 | 다음 표준 위젯을 사용하여 대상과 관련된 다양한 지표를 시각화할 수 있습니다.<ul><li>대상별로 최근에 활성화된 세그먼트입니다. 이 위젯은 선택한 대상에 따라 가장 최근에 활성화된 상위 5개의 세그먼트를 내림차순으로 표시합니다.</li><li>대상자 크기 트렌드입니다. 이 위젯은 해당 대상 계정에 매핑된 세그먼트의 기간 동안의 프로필 수 관계를 보여 줍니다.</li><li>ID별로 매핑되지 않은 세그먼트. 이 위젯은 주어진 대상 및 ID에 대한 ID 수를 내림차순으로 하여 순위가 매겨진 매핑되지 않은 상위 5개의 세그먼트를 나열합니다.</li><li>ID별로 매핑된 세그먼트. 이 위젯은 매핑된 상위 5개의 세그먼트를 나열합니다. 세그먼트는 위젯의 드롭다운 메뉴에서 선택한 대상 ID와 일치하는 소스 ID의 각 수에 따라 높음에서 낮음 순으로 정렬됩니다.</li><li>일반 대상자. 이 위젯은 페이지 상단에서 선택한 대상 계정 전체에 걸쳐 활성화된 상위 5개 세그먼트 목록과 위젯 드롭다운에서 선택한 대상을 제공합니다.</li></ul> 사용 가능한 표준 위젯에 대한 자세한 내용은 [대상 대시보드 설명서](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=ko#standard-widgets)를 참조하십시오. |

[!DNL Dashboards]에 대한 자세한 내용은 [[!DNL Dashboards] 개요](../../dashboards/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network으로 전송할 수 있는 기술 제품군을 제공합니다. 이 경우 데이터를 보강 및 변형하고 Adobe 또는 Adobe이 아닌 대상으로 배포할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 스트림 구성에 대한 UI 워크플로우 개선 | 데이터 수집 UI에서 새 데이터 스트림을 만드는 워크플로우가 업데이트되었습니다. 데이터 스트림에 서비스를 추가할 때 액세스 권한이 있는 서비스만 옵션 목록에 포함됩니다. 자세한 내용은 [데이터 스트림 구성](../../datastreams/overview.md)에 대한 안내서를 참조하십시오. |
| 데이터 수집을 위한 데이터 준비 | Adobe Experience Platform Web SDK을 사용하는 경우, 이제 데이터 준비 기능을 활용하여 데이터를 서버측의 XDM(Experience Data Model)에 매핑할 수 있습니다. 자세한 내용은 데이터스트림 가이드의 [데이터 수집을 위한 데이터 준비](../../datastreams/data-prep.md)에 대한 섹션을 참조하십시오. |
| 자사 디바이스 ID | 이제 Experience Platform Web SDK을 사용하여 고객 데이터를 수집할 때 자신의 장치 ID를 Adobe Experience Platform Edge Network으로 보낼 수 있습니다. 이렇게 하면 서드파티 쿠키 수명 주기에 대한 최근 브라우저 제한 사항에 대한 해결 방법을 제공합니다. 자세한 내용은 [자사 장치 ID](../../web-sdk/identity/first-party-device-ids.md)의 안내서를 참조하십시오. |

Experience Platform의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| (Beta) 파일 기반 대상에 대한 Destination SDK 지원 | [파일 기반 대상에 대한 Destination SDK 지원](../../destinations/destination-sdk/functionality/destination-server/server-specs.md)은(는) 현재 개인 베타 버전으로 일부 파트너와 고객만 사용할 수 있습니다. 기능 및 관련 설명서는 GA 릴리스 전에 변경될 수 있습니다.<br><br>기능에 액세스하는 방법을 알아보려면 Adobe 계정 담당자에게 문의하십시오. Adobe 내부 계정 담당자는 Experience Platform 대상 제품 및 엔지니어링 팀에 연락하여 지원되는 사용 사례를 논의해야 합니다. <br><br> 파일 기반 대상에 대한 Destination SDK 지원의 베타 단계에서 Beta 파트너와 고객은 [Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md)를 사용하여 다음 기능을 활용할 수 있는 개인 대상을 구축할 수 있습니다. <ul><li>Amazon S3, SFTP 서버, Azure Blob, Azure Data Lake 저장소, 데이터 랜딩 영역 저장소를 통해 파일 기반(일괄 처리) 대상을 만듭니다.</li><li>기본 파일 내보내기 예약 및 빈도 옵션을 구성하고 설정합니다.</li><li>내보낸 CSV 파일의 형식을 지정하는 옵션(구분 기호, 이스케이프 문자 및 기타 옵션)을 구성하고 설정합니다.</li><li>사용자 지정 파일 헤더를 설정하고 편집하는 기능.</li><li>파일 및 세그먼트 내보내기에 대한 이벤트 알림을 받는 기능.</li><li>CSV, TSV, JSON, Parquet와 같은 추가 파일 유형을 내보낼 수 있습니다.</li></ul>  <br>새 기능을 시작하려면 [(Beta)을 읽고 Destination SDK을 사용하여 파일 기반 대상을 구성](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)하세요. <br><br> Destination SDK을 사용하여 비공개 또는 제품화된 *스트리밍* 대상을 만드는 기능은 이미 모든 Experience Platform 고객 및 파트너에게 제공됩니다. 자세한 내용은 [Destination SDK을 사용하여 스트리밍 대상을 구성](../../destinations/destination-sdk/guides/configure-destination-instructions.md)하는 방법에 대한 안내서를 참조하십시오. |

## [!DNL Identity Service] {#identity}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 이러한 문제는 고객 데이터가 서로 다른 시스템 간에 분산되어 각 개별 고객이 여러 개의 &quot;ID&quot;를 가지는 것처럼 보이는 경우 더욱 어려워집니다.

Adobe Experience Platform [!DNL Identity Service]을(를) 사용하면 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 더 나은 보기를 얻을 수 있으므로 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| `view-identity-graph`에 대한 새 권한 | 이제 `view-identity-graph` 권한을 사용하여 조직의 사용자가 ID 그래프 데이터를 볼 수 있는지 여부를 제어할 수 있습니다. 이 권한이 없는 사용자는 UI에서 또는 ID를 반환하는 [!DNL Identity Service] API에 액세스할 때 ID 그래프 뷰어에 액세스할 수 없습니다. 사용 권한에 대한 자세한 내용은 [액세스 제어 개요](../../access-control/home.md)를 참조하십시오. |

[!DNL Identity Service]에 대한 일반적인 정보는 [ID 서비스 개요](../../identity-service/home.md)를 참조하세요.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| GA로 이동하는 Beta 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li></ul> |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.