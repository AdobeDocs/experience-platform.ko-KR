---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Microsoft Dynamics을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# Microsoft Dynamics 커넥터

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform]은(는) 타사 CRM 시스템에서 데이터 수집을 지원합니다. CRM 공급자에 대한 지원에는 [!DNL Microsoft Dynamics]이(가) 포함됩니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## [!DNL Microsoft Dynamics]에서 XDM으로 필드 매핑

[!DNL Microsoft Dynamics]과(와) Experience Platform 간에 소스 연결을 설정하려면 Experience Platform에 수집되기 전에 [!DNL Microsoft Dynamics] 소스 데이터 필드를 해당 대상 XDM 필드에 매핑해야 합니다.

[!DNL Microsoft Dynamics] 데이터 세트와 Experience Platform 간의 필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하세요.

- [연락처](../adobe-applications/mapping/dynamics.md#contacts)
- [잠재 고객](../adobe-applications/mapping/dynamics.md#leads)
- [계정](../adobe-applications/mapping/dynamics.md#accounts)
- [기회](../adobe-applications/mapping/dynamics.md#opportunities)
- [영업 기회 연락처 역할](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [캠페인](../adobe-applications/mapping/dynamics.md#campaigns)
- [마케팅 목록](../adobe-applications/mapping/dynamics.md#marketing-list)
- [마케팅 목록 멤버](../adobe-applications/mapping/dynamics.md#marketing-list-members)

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Microsoft Dynamics]을(를) [!DNL Experience Platform]에 연결하는 방법에 대한 정보를 제공합니다.

## API를 사용하여 [!DNL Microsoft Dynamics]을(를) [!DNL Experience Platform]에 연결

- [흐름 서비스 API를 사용하여 Microsoft Dynamics 기본 연결 만들기](../../tutorials/api/create/crm/ms-dynamics.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 CRM 소스의 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## UI를 사용하여 [!DNL Microsoft Dynamics]을(를) [!DNL Experience Platform]에 연결

- [UI에서 Microsoft Dynamics 소스 연결 만들기](../../tutorials/ui/create/crm/dynamics.md)
- [UI에서 CRM 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
