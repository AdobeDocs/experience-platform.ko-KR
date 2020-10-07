---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: 정책 실행 개요
topic: enforcement
description: 데이터 사용 레이블이 Adobe Experience Platform 데이터 세트에 적용되고 해당 레이블에 대한 마케팅 작업을 위해 데이터 사용 정책이 정의된 경우 데이터 거버넌스 기능을 사용하면 해당 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다. 플랫폼의 데이터 거버넌스 기능, API 기반 적용 및 자동 실행에서 제공하는 두 가지 정책 실행 방법이 있습니다.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 정책 실행 개요

데이터 세트 [!DNL Platform] [!DNL Data Governance] 에 데이터 사용 레이블이 적용되고 해당 레이블에 대한 마케팅 작업을 위해 데이터 사용 정책이 정의되면, 기능을 통해 해당 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다.

다음과 같은 두 가지 방법으로 정책 실행 [!DNL Data Governance] 을 수행할 수 있습니다 [!DNL Platform].API 기반의 적용 및 자동 실행

## API 기반 적용

API는 정책 위반이 발생하는지 확인하기 위해 데이터 세트 또는 임의 데이터 사용 레이블 조합에 대한 마케팅 작업을 테스트할 수 있도록 해주는 끝점을 제공합니다. [!DNL Policy Service] 그런 다음 API 응답을 기반으로, 경험 애플리케이션 내에 프로토콜을 설정하여 데이터 사용 정책 준수를 적절하게 적용할 수 있습니다.

API를 사용하여 정책을 평가하는 방법에 대한 단계는 [정책](api-enforcement.md) 집행에 대한 자습서를 참조하십시오.

## 자동 실행

(예:) 위에 구축된 특정 응용 프로그램 [!DNL Experience Platform] 은 데이터 사용 정책을 자동으로 [!DNL Real-time Customer Data Platform]적용합니다. 각 애플리케이션은 정책 위반을 표시하고 문제 해결 단계를 제공하는 고유한 방법을 유지합니다.

자동 데이터 사용 정책 실행에 대한 자세한 내용은 사용 중인 [!DNL Platform]기반 응용 프로그램의 설명서를 참조하십시오. 실시간 CDP의 자동 정책 실행에 대한 자세한 내용은 [실시간 CDP 데이터 거버넌스 개요를 참조하십시오](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).