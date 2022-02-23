---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 3ae4d0f0a92c96b15c605c6654693fd6d7e94ba8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 2월 23일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 스트림 구성을 위한 UI 워크플로우가 개선되었습니다 | 데이터 수집 UI에서 새 데이터 스트림을 만드는 워크플로우가 업데이트되었습니다. 데이터 스트림에 서비스를 추가할 때 액세스 권한이 있는 서비스만 옵션 목록에 포함됩니다. 다음 안내서를 참조하십시오. [데이터 스트림 구성](../../edge/fundamentals/datastreams.md) 추가 정보. |
| 데이터 수집을 위한 데이터 준비 | 이제 Adobe Experience Platform Web SDK를 사용하는 경우 데이터 준비 기능을 활용하여 데이터를 서버 쪽의 XDM(Experience Data Model)에 매핑할 수 있습니다. 의 섹션을 참조하십시오. [데이터 수집을 위한 데이터 준비](../../edge/fundamentals/datastreams.md#data-prep) 자세한 내용은 데이터 스트림 안내서를 참조하십시오. |
| 자사 장치 ID | 이제 Platform Web SDK를 사용하여 고객 데이터를 수집할 때 자체 장치 ID를 Adobe Experience Platform Edge 네트워크로 전송하여 타사 쿠키 수명 주기에 대한 최근 브라우저 제한 사항에 대한 해결 방법을 제공할 수 있습니다. 다음 안내서를 참조하십시오. [자사 장치 ID](../../edge/identity/first-party-device-ids.md) 추가 정보. |

Platform의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Data Prep] Adobe Analytics 소스 커넥터 지원 | 이제 Adobe Analytics 소스 커넥터에서 데이터 준비 기능을 지원하므로 데이터 스트림을 만들 때 Analytics 보고서 세트 데이터를 대상 XDM 스키마에 매핑할 수 있습니다. 다음에서 자습서를 참조하십시오. [analytics 소스 커넥터 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 추가 정보. |

자세한 내용은 [!DNL Data Prep]를 보려면 [[!DNL Data Prep] 개요](../../data-prep/home.md).

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
