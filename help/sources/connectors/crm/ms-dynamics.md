---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Microsoft Dynamics를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics 커넥터

Adobe Experience Platform을 사용하면 를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 에서는 타사 CRM 시스템에서 데이터 섭취를 지원합니다. CRM 공급자를 지원하는 기능은 다음과 같습니다 [!DNL Microsoft Dynamics].

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 필드 매핑 위치 [!DNL Microsoft Dynamics] XDM으로

소스 연결을 설정하려면 [!DNL Microsoft Dynamics] 및 플랫폼, [!DNL Microsoft Dynamics] 소스 데이터 필드를 Platform으로 수집하기 전에 적절한 대상 XDM 필드에 매핑해야 합니다.

필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Microsoft Dynamics] 데이터 세트 및 플랫폼:

- [연락처](../adobe-applications/mapping/dynamics.md#contacts)
- [리드](../adobe-applications/mapping/dynamics.md#leads)
- [계정](../adobe-applications/mapping/dynamics.md#accounts)
- [기회](../adobe-applications/mapping/dynamics.md#opportunities)
- [기회 연락처 역할](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [캠페인](../adobe-applications/mapping/dynamics.md#campaigns)
- [마케팅 목록](../adobe-applications/mapping/dynamics.md#marketing-list)
- [마케팅 목록 구성원](../adobe-applications/mapping/dynamics.md#marketing-list-members)

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Microsoft Dynamics] to [!DNL Platform] api 또는 사용자 인터페이스 사용:

## Connect [!DNL Microsoft Dynamics] to [!DNL Platform] api 사용

- [Flow Service API를 사용하여 Microsoft Dynamics 기본 연결 만들기](../../tutorials/api/create/crm/ms-dynamics.md)
- [Flow Service API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [Flow Service API를 사용하여 CRM 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## Connect [!DNL Microsoft Dynamics] to [!DNL Platform] ui 사용

- [UI에서 Microsoft Dynamics 소스 연결 만들기](../../tutorials/ui/create/crm/dynamics.md)
- [UI에서 CRM 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
