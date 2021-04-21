---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;마케팅 참여;마케팅;home;popular topics;marketing to engage;marketing
solution: Experience Platform
title: Marketo Engage 커넥터
topic-legacy: overview
description: 이 문서에서는 Marketo Engage 소스 커넥터의 인증, 매핑 및 데이터 지연에 대한 정보를 비롯하여 개요 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# (베타) [!DNL Marketo Engage] 커넥터

>[!IMPORTANT]
>
>[!DNL Marketo Engage] 소스는 현재 베타 상태입니다. 기능 및 설명서는 변경될 수 있습니다.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (이하 &quot;[!DNL Marketo]&quot;이라 한다)는 리드 관리를 위한 완벽한 솔루션이며 복잡한 구매 여정의 모든 단계에서 참여를 유도하여 고객 경험을 혁신하고자 하는 B2B 마케터에게 적합합니다.

[!DNL Marketo] 소스 커넥터를 사용하면 [!DNL Marketo]의 B2B 데이터를 Platform으로 가져오고 플랫폼에 연결된 애플리케이션을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다.

이 문서에서는 커넥터 인증 방법, [!DNL Marketo] 필드를 XDM(경험 데이터 모델)에 매핑하는 방법 및 커넥터의 데이터 지연에 대한 정보를 포함하여 [!DNL Marketo] 소스 커넥터에 대한 개요를 제공합니다.

## [!DNL Marketo] 커넥터 인증

[!DNL Marketo]을(를) 플랫폼에 연결하려면 먼저 `munchkinId`, `clientId` 및 `clientSecret`에 대한 값을 검색해야 합니다.

자격 증명을 검색하려면 [Marketo 소스 커넥터 인증](./marketo-auth.md) 문서에 설명된 단계를 참조하십시오.

## 경험 데이터 모델(XDM)

XDM은 다운스트림 플랫폼 서비스에서 사용할 수 있도록 제3자 소스의 데이터를 인제스트할 수 있도록 공통 구조와 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 플랫폼 에코시스템에 일관되게 통합할 수 있으므로 데이터를 보다 손쉽게 전달하고 정보를 수집할 수 있습니다.

XDM 및 플랫폼 역할에 대한 자세한 내용은 [XDM 시스템 개요](../../../../xdm/home.md)를 참조하십시오.

## [!DNL Marketo]에서 XDM으로 필드 매핑

[!DNL Marketo] 및 플랫폼 간의 소스 연결을 설정하려면 플랫폼에 인제스트되기 전에 Marketo 소스 데이터 필드를 해당 대상 XDM 필드에 매핑해야 합니다.

[!DNL Marketo] 데이터 세트와 플랫폼 사이의 필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하십시오.

* [활동](../mapping/marketo.md#activities)
* [프로그램](../mapping/marketo.md#programs)
* [프로그램 멤버십](../mapping/marketo.md#program-memberships)
* [회사](../mapping/marketo.md#companies)
* [정적 목록](../mapping/marketo.md#static-lists)
* [정적 목록 구성원 자격](../mapping/marketo.md#static-list-memberships)
* [지정된 계정](../mapping/marketo.md#named-accounts)
* [기회](../mapping/marketo.md#opportunities)
* [기회 연락처 역할](../mapping/marketo.md#opportunity-contact-roles)
* [인물](../mapping/marketo.md#persons)

## 플랫폼의 [!DNL Marketo] 데이터의 예상 대기 시간

다음 표는 데이터 수집의 특성 및 원하는 대상을 기반으로, 플랫폼에 [!DNL Marketo] 데이터를 가져오기 위한 예상 지연에 대해 간략하게 설명합니다.

| 대상 | 예상 지연 |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60분 |

## 다음 단계 및 추가 리소스

다음 설명서는 [!DNL Marketo] 소스 연결을 만드는 방법에 대한 자세한 정보를 제공합니다.

* [!DNL Marketo] 데이터를 플랫폼에 연결하는 방법에 대한 자세한 내용은 UI](../../../tutorials/ui/create/adobe-applications/marketo.md)에서 Marketo 소스 커넥터 만들기에서 자습서를 참조하십시오.[
* [!DNL Marketo]에 사용된 B2B 네임스페이스 및 스키마에 대한 기본 설정에 대한 자세한 내용은 [B2B 네임스페이스 및 스키마](./marketo-namespaces.md)에 대한 설명서를 참조하십시오.
* [!DNL Marketo] 혼합 ID를 찾고 자격 증명을 생성하는 방법에 대한 자세한 내용은 [[!DNL Marketo] 인증 안내서](./marketo-auth.md)를 참조하십시오.
* [!DNL Marketo] 데이터 집합에 적용되는 특정 매핑 규칙에 대한 자세한 내용은 [[!DNL Marketo] 필드 매핑](../mapping/marketo.md)에 대한 설명서를 참조하십시오.