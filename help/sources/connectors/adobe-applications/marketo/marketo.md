---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo Engage 커넥터
topic-legacy: overview
description: 이 문서에서는 인증, 매핑 및 데이터 지연에 대한 정보를 포함하여 Marketo Engage 소스 커넥터에 대한 개요를 제공합니다.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 2844ffd7270ffcc2fba4da08dda1aea238cf6c9f
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# [!DNL Marketo Engage] 커넥터

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (이하 &quot;[!DNL Marketo]&quot;라 한다)는 리드 관리를 위한 완전한 솔루션이며, 복잡한 구매 여정의 모든 단계에서 고객 경험을 전환하여 고객 경험을 혁신하고자 하는 B2B 마케터입니다.

[!DNL Marketo] 소스 커넥터를 사용하면 [!DNL Marketo]에서 Platform으로 B2B 데이터를 가져와 플랫폼에 연결된 응용 프로그램을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다.

이 문서에서는 커넥터 인증 방법, [!DNL Marketo] 필드를 XDM(Experience Data Model)에 매핑하는 방법, 커넥터의 데이터 지연에 대한 정보를 포함하는 [!DNL Marketo] 소스 커넥터에 대한 개요를 제공합니다.

## [!DNL Marketo] 커넥터 인증

[!DNL Marketo] 을 Platform에 연결하려면 먼저 `munchkinId`, `clientId` 및 `clientSecret`에 대한 값을 검색해야 합니다.

자격 증명을 검색하려면 [Marketo 소스 커넥터 인증](./marketo-auth.md) 문서에 설명된 단계를 참조하십시오.

## XDM(경험 데이터 모델)

XDM은 다운스트림 플랫폼 서비스에서 사용할 타사 소스의 데이터를 수집할 수 있도록 하는 일반적인 구조 및 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 플랫폼 에코시스템에 균일하게 통합할 수 있으므로 데이터를 쉽게 전달하고 정보를 수집할 수 있습니다.

Platform의 XDM 및 역할에 대한 자세한 내용은 [XDM 시스템 개요](../../../../xdm/home.md)를 참조하십시오.

## [!DNL Marketo]에서 XDM으로 필드 매핑

[!DNL Marketo] 과(와) 플랫폼 간에 소스 연결을 설정하려면 Platform으로 수집하기 전에 Marketo 소스 데이터 필드를 적절한 대상 XDM 필드에 매핑해야 합니다.

[!DNL Marketo] 데이터 세트와 플랫폼 간의 필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하십시오.

* [활동](../mapping/marketo.md#activities)
* [프로그램](../mapping/marketo.md#programs)
* [프로그램 멤버십](../mapping/marketo.md#program-memberships)
* [회사](../mapping/marketo.md#companies)
* [정적 목록](../mapping/marketo.md#static-lists)
* [정적 목록 구성원](../mapping/marketo.md#static-list-memberships)
* [명명된 계정](../mapping/marketo.md#named-accounts)
* [기회](../mapping/marketo.md#opportunities)
* [기회 연락처 역할](../mapping/marketo.md#opportunity-contact-roles)
* [사람](../mapping/marketo.md#persons)

## 플랫폼에서 [!DNL Marketo] 데이터의 예상 지연

다음 표에서는 수집 특성 및 원하는 대상에 따라 [!DNL Marketo] 데이터를 플랫폼으로 가져오는 데 걸리는 예상 지연을 간략하게 설명합니다.

| 대상 | 예상 지연 |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60분 |

## 다음 단계 및 추가 리소스

다음 설명서는 [!DNL Marketo] 소스 연결 만들기에 대한 자세한 정보를 제공합니다.

* [!DNL Marketo] 데이터를 Platform에 연결하는 방법에 대한 자세한 내용은 [UI](../../../tutorials/ui/create/adobe-applications/marketo.md)에서 Marketo 소스 커넥터 만들기에서 자습서를 참조하십시오.
* [!DNL Marketo]과 함께 사용되는 B2B 네임스페이스 및 스키마에 대한 기본 설정에 대한 자세한 내용은 [B2B 네임스페이스 및 스키마](./marketo-namespaces.md)에 대한 설명서를 참조하십시오.
* [!DNL Marketo] Munchkin ID를 찾고 자격 증명을 생성하는 방법에 대한 자세한 내용은 [[!DNL Marketo] 인증 안내서](./marketo-auth.md)를 참조하십시오.
* [!DNL Marketo] 데이터 세트에 적용되는 특정 매핑 규칙에 대한 자세한 내용은 [[!DNL Marketo] 필드 매핑](../mapping/marketo.md)에 있는 설명서를 참조하십시오.
* [!DNL Real-time Customer Data Platform B2B Edition] 및 해당 기능에 대한 일반적인 정보는 [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md)의 설명서를 참조하십시오.
