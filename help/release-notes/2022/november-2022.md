---
title: Adobe Experience Platform 릴리스 노트 2022년 11월
description: Adobe Experience Platform에 대한 2022년 11월 릴리스 정보입니다.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 58%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2022년 11월 23일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [경험 데이터 모델 (XDM)](#xdm)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 이벤트 전달을 위한 [!DNL AWS] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Amazon Web Services]&#x200B;([!DNL AWS])에게 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL AWS] 확장 기능 개요](../../tags/extensions/server/aws/overview.md)를 참조하십시오. |
| 이벤트 전달을 위한 [!DNL Google Ads Enhanced Conversions] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Google Ads]에 전환 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Google Ads Enhanced Conversions] 확장 기능 개요](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)를 참조하십시오. |
| 이벤트 전달을 위한 [!DNL Microsoft Azure] 확장 | 이제 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) 확장을 사용하여 [!DNL Microsoft Azure]에 데이터를 보낼 수 있습니다. 자세한 내용은 [[!DNL Microsoft Azure] 확장 기능 개요](../../tags/extensions/server/azure/overview.md)를 참조하십시오. |

Experience Platform의 데이터 수집 기능에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 직접 추가할 때 사용자 정의 클래스에 필드 할당 | [개별 필드를 스키마에 직접 추가](../../xdm/ui/resources/schemas.md#add-individual-fields)할 때 이전에는 필드를 상위 리소스로 필드 그룹에만 할당할 수 있었습니다. 이제 필드 그룹 외에 [사용자 지정 클래스에 필드를 할당](../../xdm/ui/resources/schemas.md#add-to-class)할 수 있습니다. 대신 해당 부모 리소스로 지정하십시오. |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.
