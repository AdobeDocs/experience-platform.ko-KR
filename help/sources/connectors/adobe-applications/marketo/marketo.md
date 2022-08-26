---
keywords: Experience Platform;홈;인기 항목;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo Engage 커넥터
topic-legacy: overview
description: 이 문서에서는 인증, 매핑 및 데이터 지연에 대한 정보를 포함하여 Marketo Engage 소스 커넥터에 대한 개요를 제공합니다.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: efa6891024cacd383f4cd958162a7a4f8ead0624
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# [!DNL Marketo Engage] 커넥터

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (이하 &quot;라 한다)[!DNL Marketo]&quot;)는 리드 관리를 위한 완전한 솔루션이며, 복잡한 구매 여정의 모든 단계에서 고객 경험을 전환하여 고객 경험을 혁신하고자 하는 B2B 마케터입니다.

사용 [!DNL Marketo] 소스 커넥터에서는 B2B 데이터를 가져올 수 있습니다 [!DNL Marketo] 플랫폼 연결 응용 프로그램을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다.

>[!IMPORTANT]
>
>액세스 권한이 있어야 합니다. [Real-time Customer Data Platform B2B 에디션](../../../../rtcdp/b2b-overview.md) 을 사용하여 세그먼테이션에 모든 Marketo 데이터 세트를 사용하려면 [실시간 고객 프로필](../../../../profile/home.md). 실시간 CDP B2B Edition이 없어도 Marketo 소스를 사용하여 사람 및 활동 데이터 세트에서 세그멘테이션을 위해 실시간 고객 프로필로 데이터를 가져올 수 있습니다.

이 문서에서는 [!DNL Marketo] 커넥터 인증 방법, 매핑 방법 정보가 포함된 소스 커넥터 [!DNL Marketo] experience 데이터 모델(XDM) 및 커넥터의 데이터 지연 필드.

## 인증 [!DNL Marketo] 커넥터

연결하려면 [!DNL Marketo] 플랫폼에서는 먼저 `munchkinId`, `clientId`, 및 `clientSecret`.

다음 사항에 설명된 단계를 참조하십시오. [Marketo 소스 커넥터 인증](./marketo-auth.md) 자격 증명을 검색할 문서입니다.

## Adobe 조직 매핑 설정

매핑 세트를 설정하기 전에 [!DNL Marketo]를 지정하는 경우 먼저 Adobe 조직 매핑을 설정해야 합니다. 이 작업을 완료하는 방법에 대한 자세한 단계는 다음 안내서를 참조하십시오. [Adobe 조직 매핑 설정 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## B2B 네임스페이스 및 스키마 자동 생성 유틸리티를 설정합니다

다음으로, B2B 네임스페이스 및 스키마 자동 생성 유틸리티를 사용하여 플랫폼 개발자 콘솔 및 Postman 환경을 설정합니다. 이렇게 하면 B2B 네임스페이스 및 스키마를 자동으로 채울 수 있습니다. 자세한 지침은 [B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설정](./marketo-namespaces.md)

## XDM(경험 데이터 모델)

XDM은 다운스트림 플랫폼 서비스에서 사용할 타사 소스의 데이터를 수집할 수 있도록 하는 일반적인 구조 및 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 플랫폼 에코시스템에 균일하게 통합할 수 있으므로 데이터를 쉽게 전달하고 정보를 수집할 수 있습니다.

Platform의 XDM 및 역할에 대한 자세한 내용은 [XDM 시스템 개요](../../../../xdm/home.md).

## 필드 매핑 위치 [!DNL Marketo] XDM으로

소스 연결을 설정하려면 [!DNL Marketo] 및 Platform에서 Marketo 소스 데이터 필드를 Platform에 수집하기 전에 적절한 대상 XDM 필드에 매핑해야 합니다.

필드 매핑 규칙에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Marketo] 데이터 세트 및 플랫폼:

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

## 예상 지연 시간 [!DNL Marketo] 플랫폼의 데이터

다음 표에서는 가져올 예상 지연 시간을 간략하게 설명합니다 [!DNL Marketo] 수집 특성 및 원하는 대상에 따라 플랫폼으로 데이터 전송:

| 대상 | 예상 지연 |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1분 |
| Data Lake | &lt; 60분 |

## 다음 단계 및 추가 리소스

다음 설명서는 [!DNL Marketo] 소스 연결:

* 연결 방법에 대한 자세한 내용 [!DNL Marketo] 데이터를 Platform으로 변환하려면 [UI에서 Marketo 소스 커넥터 만들기](../../../tutorials/ui/create/adobe-applications/marketo.md).
* 와 함께 사용되는 B2B 네임스페이스 및 스키마에 대한 기본 설정에 대한 정보 [!DNL Marketo]의 경우 설명서 를 참조하십시오. [B2B 네임스페이스 및 스키마](./marketo-namespaces.md).
* 검색 결과에 대한 자세한 정보 [!DNL Marketo] munchkin ID를 생성하고 자격 증명을 생성하는 방법은 [[!DNL Marketo] 인증 안내서](./marketo-auth.md).
* 에 적용되는 특정 매핑 규칙에 대한 정보 [!DNL Marketo] 데이터 세트에 대한 자세한 내용은 [[!DNL Marketo] 필드 매핑](../mapping/marketo.md).
* 에 대한 일반적인 정보 [!DNL Real-time Customer Data Platform B2B Edition] 및 해당 기능은 [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
