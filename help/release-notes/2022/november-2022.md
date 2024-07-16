---
title: Adobe Experience Platform 릴리스 노트 2022년 11월
description: Adobe Experience Platform에 대한 2022년 11월 릴리스 정보입니다.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 52%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2022년 11월 23일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [경험 데이터 모델 (XDM)](#xdm)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 이벤트 전달을 위한 [!DNL AWS] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Amazon Web Services]([!DNL AWS])에게 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL AWS] 확장 개요](../../tags/extensions/server/aws/overview.md)를 참조하십시오. |
| 이벤트 전달을 위한 [!DNL Google Ads Enhanced Conversions] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Google Ads]에 전환 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Google Ads Enhanced Conversions] 확장 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)를 참조하십시오. |
| 이벤트 전달을 위한 [!DNL Microsoft Azure] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Microsoft Azure]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Microsoft Azure] 확장 개요](../../tags/extensions/server/azure/overview.md)를 참조하십시오. |

플랫폼의 데이터 수집 기능에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 직접 추가할 때 사용자 정의 클래스에 필드 할당 | [개별 필드를 스키마에 직접 추가](../../xdm/ui/resources/schemas.md#add-individual-fields)할 때 이전에는 필드를 상위 리소스로 필드 그룹에만 할당할 수 있었습니다. 이제 필드 그룹 외에 [사용자 지정 클래스에 필드를 할당](../../xdm/ui/resources/schemas.md#add-to-class)할 수 있습니다. 대신 해당 부모 리소스로 지정하십시오. |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- | 
| Oracle 서비스 클라우드 소스의 Beta 가용성 | oracle 서비스 클라우드 소스를 사용하여 Oracle 서비스 클라우드 계정에서 Experience Platform으로 데이터를 수집합니다. 자세한 내용은 [Oracle 서비스 클라우드 원본](../../sources/connectors/customer-success/oracle-service-cloud.md)에 대한 설명서를 참조하세요. |

소스에 대해 자세히 알아보려면 [소스 개요 ](../../sources/home.md)를 참조하십시오.
