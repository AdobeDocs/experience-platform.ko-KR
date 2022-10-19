---
title: 데이터 스트림 개요
description: 클라이언트측 Experience Platform SDK 통합 기능을 Adobe 제품 및 서드파티 대상과 연결합니다.
keywords: 구성;데이터 스트림;데이터 스트림 ID;에지;데이터 스트림 ID;환경 설정;edgeConfigId;id 동기화 사용;ID 동기화 컨테이너 ID;샌드박스;스트리밍 입력;이벤트 데이터 세트;대상;클라이언트 코드;Target 환경 ID;쿠키 대상;Analytics 설정 차단 보고서 세트 ID;데이터 수집을 위한 데이터 준비;데이터 수집;데이터 매퍼;XDM 매퍼;Edge의 매퍼;Mapper;Mapper
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 2%

---

# 데이터 스트림 개요

데이터 스트림은 Adobe Experience Platform Web 및 Mobile SDK를 구현할 때 서버측 구성을 나타냅니다. 반면에 [명령 구성](../fundamentals/configuring-the-sdk.md) sdk에서 는 클라이언트(예: `edgeDomain`), 데이터 세트는 SDK에 대한 다른 모든 구성을 처리합니다. Adobe Experience Platform Edge Network에 요청이 전송되면 `edgeConfigId` 는 데이터 스트림을 참조하는 데 사용됩니다. 이렇게 하면 웹 사이트에서 코드를 변경하지 않고도 서버측 구성을 업데이트할 수 있습니다.

을(를) 선택하여 데이터 세트를 만들고 관리할 수 있습니다 **[!UICONTROL 데이터 스트림]** Adobe Experience Platform UI 또는 데이터 수집 UI 내의 왼쪽 탐색 영역에서 을 참조하십시오.

![UI의 데이터 스트림 탭](../assets/datastreams/overview/datastreams-tab.png)

UI에서 데이터 스트림을 구성하는 방법에 대한 자세한 내용은 [구성 안내서](./configure.md).

## 데이터 저장소에서 중요한 데이터 처리 {#sensitive}

>[!IMPORTANT]
>
>이 문서의 컨텐츠는 법률적인 조언이 아니며, 법률적인 조언을 대체하지 않습니다. 중요한 데이터 처리에 대한 자세한 내용은 회사의 법무 부서에 문의하십시오.

기업 데이터 관리 정책 및 규정 요구 사항은 중요한 고객 데이터를 수집, 처리 및 사용하는 방법에 대한 제한을 높이고 있습니다. 여기에는 HIPAA(Health Insurance Portability and Accountability Act)와 같은 규정을 준수하는 PHI(Protected Health Data)의 수집, 처리 및 사용이 포함됩니다.

데이터 저장소는 중요한 데이터를 안전하게 처리할 수 있도록 다음 세 가지 방법을 제공합니다.

* [향상된 암호화](#encryption)
* [데이터 거버넌스](#governance)
* [감사 로그](#audit-logs)

### 향상된 암호화 {#encryption}

에지 네트워크를 통해 전송되는 모든 데이터는 [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). 데이터 스트림이 데이터를 Experience Platform으로 가져오는 경우 데이터가 Experience Platform 데이터 레이크에서 나머지 위치에서 암호화됩니다. 다음 문서를 참조하십시오. [Experience Platform의 데이터 암호화](../../landing/governance-privacy-security/encryption.md) 추가 정보.

### 데이터 거버넌스 {#governance}

데이터 저장소는 Experience Platform의 기본 제공 데이터 거버넌스 기능을 활용하여 중요한 데이터가 HIPAA가 아닌 서비스로 전송되지 않도록 합니다. 데이터 스트림 스키마에서 중요한 데이터가 포함된 특정 필드에 레이블을 지정하여 특정 용도로 사용할 수 있는 데이터 필드를 세부적으로 제어할 수 있습니다.

다음 비디오에서는 UI의 데이터 세트에 대해 데이터 사용 제한을 구성하고 적용하는 방법에 대한 간단한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

Experience Platform에서 다음을 적용할 수 있습니다 [중요 데이터 사용 레이블](../../data-governance/labels/reference.md#sensitive) 로 변경되었습니다. 예: `RHD` 레이블은 PHI(Protected Health Information) 및 `S1` 레이블은 지리적 위치 데이터를 나타냅니다.

>[!NOTE]
>
>내에서 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용은 [!UICONTROL 스키마] Experience Platform UI 또는 데이터 수집 UI의 탭에서 다음을 참조하십시오. [스키마 레이블 지정 자습서](../../xdm/tutorials/labels.md).

새 데이터 스트림을 생성할 때 선택한 스키마에 중요한 데이터 사용 레이블이 포함되어 있으면 데이터 스트림을 HIPAA 준비 대상으로 해당 데이터를 보내도록 구성할 수만 있습니다. 현재 데이터 저장소에서 지원하는 유일한 HIPAA 지원 대상은 Adobe Experience Platform입니다. 중요 데이터 사용 레이블이 포함된 데이터 세트에 대해 Adobe Target, Adobe Analytics, Adobe Audience Manager, 이벤트 전달 및 에지 대상을 포함한 다른 대상 서비스가 비활성화됩니다.

비 HIPAA 지원 서비스가 있는 기존 데이터 스트림에 스키마가 사용되는 경우 중요한 데이터 사용 레이블을 스키마에 추가하려고 하면 정책 위반 메시지가 표시되고 작업이 수행되지 않습니다. 이 메시지는 위반을 트리거한 데이터 스트림을 지정하고 문제를 해결하기 위해 데이터 스트림에서 HIPAA 지원 서비스가 아닌 서비스를 제거하도록 제안합니다.

### 감사 로그

Experience Platform에서 데이터 스트림 활동을 감사 로그 형태로 모니터링할 수 있습니다. 감사 로그에 **who** 수행됨 **what** 작업 및 **when**, 기업의 데이터 관리 정책 및 규정 요구 사항을 준수하는 데 도움이 되는 데이터 스트림 관련 문제를 해결하는 데 도움이 되는 기타 컨텍스트 데이터와 함께 제공됩니다.

사용자가 데이터 스트림을 생성, 업데이트 또는 삭제할 때마다 작업을 기록하기 위한 감사 로그가 만들어집니다. 사용자가 매핑을 만들거나, 업데이트하거나, 삭제할 때마다 동일한 작업이 수행됩니다 [데이터 수집을 위한 데이터 준비](./data-prep.md). 업데이트한 데이터 스트림인지 또는 매핑인지에 관계없이 결과 감사 로그는 [!UICONTROL 데이터 스트림] 리소스 유형.

다음 문서를 참조하십시오. [감사 로그](../../landing/governance-privacy-security/audit-logs/overview.md) 데이터 스트림 및 기타 지원되는 서비스에서 로그를 해석하는 방법에 대한 자세한 내용을 참조하십시오.

## 다음 단계

이 안내서에서는 데이터 집합 및 데이터 수집 사용 및 중요 데이터 처리에 대한 개요 개요를 제공합니다. 새 데이터 스트림을 설정하는 방법에 대한 단계는 다음을 참조하십시오. [데이터 스트림 구성 안내서](./configure.md).
