---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f8e8ec0fb13fc988d47bb3bbe85f953e66b33f13
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 7%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 11월 23일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [XDM(경험 데이터 모델)](#xdm)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL AWS] 이벤트 전달을 위한 확장 | 이제 데이터를에 보낼 수 있습니다 [!DNL Amazon Web Services] ([!DNL AWS]) 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL AWS] 확장 개요](../../tags/extensions/server/aws/overview.md) 추가 정보. |
| [!DNL Google Ads Enhanced Conversions] 이벤트 전달을 위한 확장 | 이제 변환 데이터를에 보낼 수 있습니다 [!DNL Google Ads] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Google Ads Enhanced Conversions] 확장 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 추가 정보. |
| [!DNL Microsoft Azure] 이벤트 전달을 위한 확장 | 이제 데이터를에 보낼 수 있습니다 [!DNL Microsoft Azure] 사용 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장. 자세한 내용은 [[!DNL Microsoft Azure] 확장 개요](../../tags/extensions/server/azure/overview.md) 추가 정보. |

플랫폼의 데이터 수집 기능에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 직접 추가할 때 사용자 지정 클래스에 필드를 할당합니다 | When [스키마에 개별 필드 직접 추가](../../xdm/ui/resources/schemas.md#add-individual-fields)이전에는 필드를 필드 그룹에 상위 리소스로 할당할 수만 있었습니다. 이제 필드 그룹 외에도 다음을 수행할 수 있습니다 [사용자 지정 클래스에 필드 할당](../../xdm/ui/resources/schemas.md#add-to-class) 을 상위 리소스로 지정합니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- | 
| oracle 서비스 클라우드 소스의 베타 가용성 | oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 계정의 데이터를 Experience Platform으로 수집할 수 있습니다. 자세한 내용은 [Oracle 서비스 클라우드 소스](../../sources/connectors/customer-success/oracle-service-cloud.md). |

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).