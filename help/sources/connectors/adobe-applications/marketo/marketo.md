---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo Engage 커넥터
description: 이 문서에서는 인증, 매핑 및 데이터 지연에 대한 정보를 포함하여 Marketo Engage 소스 커넥터에 대한 개요를 제공합니다.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: d8cd69524d984fdb828447287f3f4a4fe5913d61
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# [!DNL Marketo Engage] 커넥터

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (이하 &quot;라고 한다)[!DNL Marketo]&quot;)는 리드 관리를 위한 완전한 솔루션이며, 복잡한 구매 여정의 모든 단계에서 고객 경험을 전환하여 고객 경험을 혁신하고자 하는 B2B 마케터입니다.

포함 [!DNL Marketo] 소스 커넥터에서는 B2B 데이터를 가져올 수 있습니다. [!DNL Marketo] 플랫폼에 연결하고 플랫폼에 연결된 애플리케이션을 사용하여 이 데이터를 최신 상태로 유지하십시오.

>[!IMPORTANT]
>
>다음에 대한 액세스 권한이 있어야 합니다. [Adobe Real-time Customer Data Platform 에디션](../../../../rtcdp/b2b-overview.md) 을 사용하여 세분화에 모든 Marketo 데이터 세트를 사용하려면 [실시간 고객 프로필](../../../../profile/home.md). Real-Time CDP B2B 에디션이 없어도 Marketo 소스를 사용하여 세분화를 위해 사람 및 활동 데이터 세트의 데이터를 실시간 고객 프로필로 가져올 수 있습니다.

이 문서에서는 [!DNL Marketo] 소스 커넥터(커넥터 인증 방법, 매핑 방법 정보 포함) [!DNL Marketo] experience Data Model(XDM)에 대한 필드 및 커넥터의 데이터 지연.

## 인증 [!DNL Marketo] 커넥터

연결하려면 [!DNL Marketo] 플랫폼으로 이동하려면 먼저 다음에 대한 값을 검색해야 합니다 `munchkinId`, `clientId`, 및 `clientSecret`.

다음에 설명된 단계 참조: [Marketo 소스 커넥터 인증](./marketo-auth.md) 자격 증명을 검색하기 위한 문서입니다.

## Adobe 조직 매핑 설정

다음에 대한 매핑 세트를 설정하기 전에 [!DNL Marketo], 먼저 Adobe 조직 매핑을 설정해야 합니다. 이 작업을 완료하는 방법에 대한 자세한 단계는 의 안내서를 참조하십시오. [다음에 대한 Adobe 조직 매핑 설정 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설정

그런 다음 B2B 네임스페이스와 스키마 자동 생성 유틸리티를 사용하여 Platform 개발자 콘솔 및 Postman 환경을 설정합니다. 이렇게 하면 B2B 네임스페이스와 스키마를 자동으로 채울 수 있습니다. 자세한 지침은 의 안내서를 참조하십시오. [B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설정](./marketo-namespaces.md)

## 경험 데이터 모델(XDM)

XDM은 다운스트림 플랫폼 서비스에서 사용하기 위해 서드파티 소스에서 데이터를 수집할 수 있는 일반적인 구조 및 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 플랫폼 생태계에 균일하게 통합할 수 있으므로 데이터를 더 쉽게 전달하고 정보를 수집할 수 있습니다.

XDM과 Platform에서의 역할에 대한 자세한 내용은 다음을 참조하십시오. [XDM 시스템 개요](../../../../xdm/home.md).

## 필드 매핑 출처 [!DNL Marketo] XDM으로

소스 연결을 설정하려면 [!DNL Marketo] 및 Platform에서 Marketo 소스 데이터 필드를 Platform으로 수집하기 전에 해당 타겟 XDM 필드에 매핑해야 합니다.

간의 필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Marketo] 데이터 세트 및 플랫폼:

* [활동](../mapping/marketo.md#activities)
* [프로그램](../mapping/marketo.md#programs)
* [프로그램 멤버십](../mapping/marketo.md#program-memberships)
* [회사](../mapping/marketo.md#companies)
* [정적 목록](../mapping/marketo.md#static-lists)
* [정적 목록 멤버십](../mapping/marketo.md#static-list-memberships)
* [명명된 계정](../mapping/marketo.md#named-accounts)
* [영업 기회](../mapping/marketo.md#opportunities)
* [영업 기회 연락처 역할](../mapping/marketo.md#opportunity-contact-roles)
* [개인](../mapping/marketo.md#persons)

## 예상 대기 시간: [!DNL Marketo] 플랫폼에 있는 데이터

다음 표는 가져오기에 대한 예상 대기 시간을 설명합니다. [!DNL Marketo] 수집 특성 및 원하는 대상을 기반으로 하는 플랫폼으로의 데이터:

| 대상 | 예상 대기 시간 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | 1분 미만 |
| 데이터 레이크 | &lt; 60분 |

## 다음 단계 및 추가 리소스

다음 설명서는 를 만드는 방법에 대해 자세히 설명합니다. [!DNL Marketo] 소스 연결:

* 연결 방법에 대한 자세한 정보 [!DNL Marketo] 데이터를 플랫폼으로 보내면에서 자습서를 참조하십시오. [만들기 [!DNL Marketo] UI의 소스 연결](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * 스키마를 설정하고 사용자 지정 활동 데이터를 수집하는 방법에 대한 자세한 내용은 [소스 연결 및 데이터 흐름 만들기 [!DNL Marketo] 사용자 지정 활동 데이터](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* 에서 사용되는 B2B 네임스페이스 및 스키마의 기본 설정에 대한 자세한 내용 [!DNL Marketo], 다음 설명서를 참조하십시오. [B2B 네임스페이스 및 스키마](./marketo-namespaces.md).
* 를 찾는 방법에 대한 자세한 내용 [!DNL Marketo] munchkin ID 및 자격 증명 생성, [[!DNL Marketo] 인증 안내서](./marketo-auth.md).
* 에 적용되는 특정 매핑 규칙에 대한 정보 [!DNL Marketo] 데이터 세트 다음에 대한 설명서를 읽어 보십시오. [[!DNL Marketo] 필드 매핑](../mapping/marketo.md).
* 다음에 대한 일반적인 정보를 위하여 [!DNL Real-Time Customer Data Platform B2B Edition] 및 해당 기능에 대한 설명서를 참조하십시오. [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
