---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo Engage 커넥터
description: 이 문서에서는 인증, 매핑 및 데이터 지연에 대한 정보를 포함하여 Marketo Engage 소스 커넥터에 대한 개요를 제공합니다.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# [!DNL Marketo Engage] 커넥터

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Marketo Engage]](https://www.marketo.com/software/)은(는) 리드 관리를 위한 완전한 솔루션이며, 복잡한 구매 여정의 모든 단계에서 고객 경험을 전환하여 고객 경험을 혁신하고자 하는 B2B 마케터입니다.

[!DNL Marketo Engage] 소스 커넥터를 사용하면 [!DNL Marketo Engage]의 B2B 데이터를 플랫폼으로 가져와서 플랫폼에 연결된 응용 프로그램을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다.

>[!IMPORTANT]
>
>[실시간 고객 프로필](../../../../profile/home.md)을(를) 사용하여 세분화하기 위해 모든 Marketo 데이터 세트를 사용하려면 [Adobe Real-time Customer Data Platform B2B 에디션](../../../../rtcdp/b2b-overview.md)에 액세스할 수 있어야 합니다. Real-Time CDP B2B 에디션이 없어도 Marketo 소스를 사용하여 세분화를 위해 사람 및 활동 데이터 세트의 데이터를 실시간 고객 프로필로 가져올 수 있습니다.

이 문서에서는 커넥터를 인증하는 방법, [!DNL Marketo Engage] 필드를 XDM(Experience Data Model)에 매핑하는 방법, 커넥터의 데이터 지연 시간 등 [!DNL Marketo Engage] 소스 커넥터에 대한 개요를 제공합니다.

## Adobe 조직 매핑 설정

[!DNL Marketo Engage]에 대한 매핑 집합을 설정하려면 먼저 Adobe 조직 매핑을 설정해야 합니다. 이 작업을 완료하는 방법에 대한 자세한 단계는 [Adobe 조직 매핑 설정 [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html)에 대한 안내서를 참조하십시오.

## [!DNL Marketo Engage] 커넥터 인증

[!DNL Marketo Engage]을(를) 플랫폼에 연결하려면 먼저 `munchkinId`, `clientId` 및 `clientSecret`에 대한 값을 검색해야 합니다.

자격 증명을 검색하려면 [Marketo 소스 커넥터 인증](./marketo-auth.md) 문서에 설명된 단계를 참조하십시오.

## B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설정

그런 다음 B2B 네임스페이스와 스키마 자동 생성 유틸리티를 사용하여 Platform 개발자 콘솔 및 Postman 환경을 설정합니다. 이렇게 하면 B2B 네임스페이스와 스키마를 자동으로 채울 수 있습니다. 자세한 지침은 [B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설정](./marketo-namespaces.md)에 대한 안내서를 참조하십시오.

## 경험 데이터 모델 (XDM)

XDM은 다운스트림 플랫폼 서비스에서 사용하기 위해 서드파티 소스에서 데이터를 수집할 수 있는 일반적인 구조 및 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 플랫폼 생태계에 균일하게 통합할 수 있으므로 데이터를 더 쉽게 전달하고 정보를 수집할 수 있습니다.

Platform에서의 XDM 및 그 역할에 대한 자세한 내용은 [XDM 시스템 개요](../../../../xdm/home.md)를 참조하십시오.

## [!DNL Marketo Engage]에서 XDM으로 필드 매핑

[!DNL Marketo Engage]과(와) 플랫폼 간에 소스 연결을 설정하려면 Platform에 수집되기 전에 Marketo 소스 데이터 필드를 적절한 대상 XDM 필드에 매핑해야 합니다.

[!DNL Marketo Engage] 데이터 세트와 플랫폼 간의 필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하세요.

* [활동](../mapping/marketo.md#activities)
* [프로그램](../mapping/marketo.md#programs)
* [프로그램 멤버십](../mapping/marketo.md#program-memberships)
* [회사](../mapping/marketo.md#companies)
* [정적 목록](../mapping/marketo.md#static-lists)
* [정적 목록 멤버십](../mapping/marketo.md#static-list-memberships)
* [명명된 계정](../mapping/marketo.md#named-accounts)
* [기회](../mapping/marketo.md#opportunities)
* [영업 기회 연락처 역할](../mapping/marketo.md#opportunity-contact-roles)
* [개인](../mapping/marketo.md#persons)

## 플랫폼에서 [!DNL Marketo Engage] 데이터의 예상 대기 시간

다음 표에서는 수집의 특성 및 원하는 대상에 따라 [!DNL Marketo Engage] 데이터를 플랫폼으로 가져오는 데 필요한 예상 대기 시간을 설명합니다.

| 대상 | 예상 대기 시간 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10분 |
| 데이터 레이크 | 60분 미만 |

>[!NOTE]
>
>위의 지연 수치는 95% 신뢰 수준에서 기대치를 나타냅니다. 실제 지연 시간은 다양하며 드문 경우 이러한 수치를 50% 초과할 수 있습니다.

## 다음 단계 및 추가 리소스

다음 설명서는 [!DNL Marketo Engage] 원본 연결을 만드는 방법에 대한 자세한 정보를 제공합니다.

* [!DNL Marketo Engage] 데이터를 플랫폼에 연결하는 방법에 대한 자세한 내용은 [UI에서  [!DNL Marketo Engage] 소스 연결 만들기](../../../tutorials/ui/create/adobe-applications/marketo.md)에 대한 자습서를 참조하십시오.
   * 스키마를 설정하고 사용자 지정 활동 데이터를 수집하는 방법에 대한 자세한 내용은 [사용자 지정 활동 데이터에 대한 소스 연결 및 데이터 흐름 만들기 [!DNL Marketo Engage] 에 대한 자습서를 참조하십시오](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * ECID 매핑을 [!DNL Person] 데이터 집합에서 [!DNL Activity] 데이터 집합으로 마이그레이션하는 방법에 대한 자세한 내용은 [ECID 매핑 마이그레이션 안내서](./migration.md)를 참조하십시오.
* [!DNL Marketo Engage]에서 사용되는 B2B 네임스페이스 및 스키마의 기본 설정에 대한 자세한 내용은 [B2B 네임스페이스 및 스키마](./marketo-namespaces.md)에 대한 설명서를 참조하십시오.
* [!DNL Marketo Engage] munchkin ID를 찾고 자격 증명을 생성하는 방법에 대한 자세한 내용은 [[!DNL Marketo Engage] 인증 안내서](./marketo-auth.md)를 참조하세요.
* [!DNL Marketo Engage] 데이터 세트에 적용되는 특정 매핑 규칙에 대한 자세한 내용은 [[!DNL Marketo Engage] 필드 매핑](../mapping/marketo.md)에 대한 설명서를 참조하십시오.
* [!DNL Real-Time Customer Data Platform B2B Edition] 및 해당 기능에 대한 일반적인 정보는 [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md)의 설명서를 참조하십시오.
