---
title: Adobe Experience Platform 릴리스 노트 2022년 11월
description: Adobe Experience Platform에 대한 2022년 11월 릴리스 정보입니다.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 11월 23일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [경험 데이터 모델(XDM)](#xdm)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL AWS] 이벤트 전달을 위한 확장 | 이제 로 데이터를 보낼 수 있습니다. [!DNL Amazon Web Services] ([!DNL AWS]) 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL AWS] 확장 개요](../../tags/extensions/server/aws/overview.md) 추가 정보. |
| [!DNL Google Ads Enhanced Conversions] 이벤트 전달을 위한 확장 | 이제 변환 데이터를 로 보낼 수 있습니다. [!DNL Google Ads] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL Google Ads Enhanced Conversions] 확장 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 추가 정보. |
| [!DNL Microsoft Azure] 이벤트 전달을 위한 확장 | 이제 로 데이터를 보낼 수 있습니다. [!DNL Microsoft Azure] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장명. 다음을 참조하십시오. [[!DNL Microsoft Azure] 확장 개요](../../tags/extensions/server/azure/overview.md) 추가 정보. |

플랫폼의 데이터 수집 기능에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## 경험 데이터 모델(XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 직접 추가할 때 사용자 정의 클래스에 필드 할당 | 날짜 [스키마에 직접 개별 필드 추가](../../xdm/ui/resources/schemas.md#add-individual-fields), 이전에는 필드를 상위 리소스로 필드 그룹에만 할당할 수 있었습니다. 이제 필드 그룹 외에 다음 작업을 수행할 수 있습니다 [필드를 사용자 정의 클래스에 할당](../../xdm/ui/resources/schemas.md#add-to-class) 을(를) 상위 리소스로 사용하십시오. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- | 
| oracle 서비스 클라우드 소스의 Beta 가용성 | oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 계정에서 Experience Platform으로 데이터를 수집합니다. 자세한 내용은 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
