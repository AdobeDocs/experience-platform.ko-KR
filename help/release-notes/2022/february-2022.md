---
title: Adobe Experience Platform 릴리스 노트 - 2022년 2월
description: Adobe Experience Platform에 대한 2022년 2월 릴리스 노트입니다.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 3%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2022년 3월 7일**

>[!NOTE]
>
>이 릴리스는 2월 23일의 원래 날짜에서 3월 7일로 변경되었습니다.

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform은 여러 기능을 제공합니다 [!DNL dashboards] 을 통해 일일 스냅샷 동안 캡처된 조직 데이터에 대한 중요한 통찰력을 볼 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 표준 대상 위젯 | 다음 표준 위젯을 사용하면 대상과 관련된 다양한 지표를 시각화할 수 있습니다.<ul><li>대상별로 최근에 활성화된 세그먼트입니다. 이 위젯은 선택한 대상에 따라 가장 최근에 활성화된 상위 5개의 세그먼트를 내림차순으로 표시합니다.</li><li>대상 크기 트렌드입니다. 이 위젯은 해당 대상 계정에 매핑된 세그먼트의 일정 기간 동안 프로필 수 관계를 나타냅니다.</li><li>ID로 매핑되지 않은 세그먼트입니다. 이 위젯은 지정된 대상 및 ID에 대한 내림차순 ID 카운트로 순위가 지정된 상위 5개의 매핑되지 않은 세그먼트를 나열합니다.</li><li>ID별로 매핑된 세그먼트. 이 위젯은 상위 5개의 매핑된 세그먼트를 나열합니다. 세그먼트는 위젯의 드롭다운 메뉴에서 선택한 대상 ID와 일치하는 소스 ID의 각 수에 따라 높은 값에서 낮은 순서로 정렬됩니다.</li><li>일반적인 대상. 이 위젯은 페이지 맨 위에서 선택한 대상 계정에서 활성화된 상위 5개 세그먼트 목록과 위젯 드롭다운에서 선택한 대상을 제공합니다.</li></ul> 사용 가능한 표준 위젯에 대한 자세한 내용은 [대상 대시보드 설명서.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

자세한 내용은 [!DNL Dashboards]를 보려면 [[!DNL Dashboards] 개요](../../dashboards/home.md).

## 데이터 수집 {#data-collection}

Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 스트림 구성을 위한 UI 워크플로우가 개선되었습니다 | 데이터 수집 UI에서 새 데이터 스트림을 만드는 워크플로우가 업데이트되었습니다. 데이터 스트림에 서비스를 추가할 때 액세스 권한이 있는 서비스만 옵션 목록에 포함됩니다. 다음 안내서를 참조하십시오. [데이터 스트림 구성](../../edge/datastreams/overview.md) 추가 정보. |
| 데이터 수집을 위한 데이터 준비 | 이제 Adobe Experience Platform Web SDK를 사용하는 경우 데이터 준비 기능을 활용하여 데이터를 서버 쪽의 XDM(Experience Data Model)에 매핑할 수 있습니다. 의 섹션을 참조하십시오. [데이터 수집을 위한 데이터 준비](../../edge/datastreams/data-prep.md) 자세한 내용은 데이터 스트림 안내서를 참조하십시오. |
| 자사 장치 ID | 이제 Platform Web SDK를 사용하여 고객 데이터를 수집할 때 자체 장치 ID를 Adobe Experience Platform Edge 네트워크로 전송하여 타사 쿠키 수명 주기에 대한 최근 브라우저 제한 사항에 대한 해결 방법을 제공할 수 있습니다. 다음 안내서를 참조하십시오. [자사 장치 ID](../../edge/identity/first-party-device-ids.md) 추가 정보. |

Platform의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| (베타) 파일 기반 대상에 대한 Destination SDK 지원 | [파일 기반 대상에 대한 Destination SDK 지원](../../destinations/destination-sdk/file-based-destination-configuration.md) 는 현재 비공개 베타에 있으며 일부 파트너 및 고객만 사용할 수 있습니다. GA 릴리스 전에 기능 및 관련 설명서가 변경될 수 있습니다.<br><br>기능에 액세스하는 방법에 대해 알려면 Adobe 계정 담당자에게 문의하십시오. Adobe 내부 계정 담당자는 Experience Platform 대상 제품 및 엔지니어링 팀에 연락하여 지원되는 사용 사례에 대해 논의해야 합니다. <br><br> 파일 기반 대상에 대한 Destination SDK 지원 베타 단계에서 베타 파트너 및 고객은 [Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) 다음 기능을 통해 혜택을 받을 비공개 대상을 빌드하려면 다음을 수행하십시오. <ul><li>Amazon S3, SFTP 서버, Azure Blob, Azure Data Lake 저장소, 데이터 랜딩 영역 저장소를 통해 파일 기반(일괄 처리) 대상을 만듭니다.</li><li>기본 파일 내보내기 예약 및 빈도 옵션을 구성하고 설정합니다.</li><li>내보낸 CSV 파일(구분 기호, 이스케이프 문자 및 기타 옵션)의 형식을 지정하는 옵션을 구성하고 설정합니다.</li><li>사용자 지정 파일 헤더를 설정하고 편집하는 기능.</li><li>파일 및 세그먼트 내보내기에 대한 이벤트 알림을 받는 기능.</li><li>CSV, TSV, JSON, Parquet과 같은 추가 파일 유형을 내보내는 기능.</li></ul>  <br>새 기능을 시작하려면 다음을 참조하십시오. [(베타) Destination SDK을 사용하여 파일 기반 대상 구성](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> 비공개 또는 제품을 만드는 기능 *스트리밍* 모든 Experience Platform 고객 및 파트너는 Destination SDK을 사용한 대상을 이미 사용할 수 있습니다. 방법에 대한 안내서를 참조하십시오. [Destination SDK을 사용하여 스트리밍 대상 구성](/help/destinations/destination-sdk/configure-destination-instructions.md) 자세한 내용 |

## [!DNL Identity Service] {#identity}

적절한 디지털 경험을 제공하려면 고객을 완전히 이해해야 합니다. 서로 다른 시스템에서 고객 데이터가 단편화된 경우 각 개별 고객이 여러 &quot;ID&quot;를 보유한 것처럼 보일 때 더욱 어렵습니다.

Adobe Experience Platform [!DNL Identity Service] 은 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 고객의 행동을 더 잘 파악할 수 있도록 지원하고 효과적이고 개인화된 디지털 경험을 실시간으로 제공할 수 있도록 합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 권한 `view-identity-graph` | 이제 를 사용할 수 있습니다 `view-identity-graph` 조직의 사용자가 id 그래프 데이터를 볼 수 있는지 여부를 제어할 수 있는 권한입니다. 이 권한이 없는 사용자는 UI에서 ID 그래프 뷰어에 액세스할 수 없거나 액세스할 때 허용되지 않습니다 [!DNL Identity Service] ID를 반환하는 API입니다. 자세한 내용은 [액세스 제어 개요](../../access-control/home.md) 사용 권한에 대한 자세한 내용을 참조하십시오. |

자세한 내용은 [!DNL Identity Service]를 참조하려면 [ID 서비스 개요](../../identity-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| GA로 이동하는 베타 소스 | 다음 소스가 Beta에서 GA로 승격되었습니다. <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).