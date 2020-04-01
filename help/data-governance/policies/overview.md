---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 사용 정책 개요
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# 데이터 사용 정책 개요

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 구현해야 합니다. 데이터 사용 정책은 경험 플랫폼 내에서 데이터에 대해 수행하도록 허용되거나 제한된 마케팅 활동의 종류를 설명하는 규칙입니다.

마케팅 활동의 예는 데이터 세트를 타사 서비스로 내보내려는 것일 수 있습니다. PII(개인 식별 정보)와 같은 특정 유형의 데이터를 내보낼 수 없고 데이터 세트에 &quot;I&quot; 레이블(ID 데이터)이 적용되었다면 정책 서비스에서 데이터 사용 정책을 위반했다는 응답을 받게 됩니다.

## 데이터 사용 정책을 만들고 사용하는 방법

데이터 사용 레이블이 적용되면 데이터 관리자는 DULE Policy Service API를 사용하여 정책을 [만들 수 있습니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

데이터 관리자로서 정책 서비스 API를 사용하여 DULE 레이블이 포함된 데이터에 대해 수행되는 마케팅 작업과 관련된 정책을 관리하고 평가할 수 있습니다. API를 사용하여 정책을 만들고 업데이트하고, 정책의 상태를 확인하고, 마케팅 작업을 통해 특정 작업이 데이터 사용 정책을 위반하는지 평가할 수 있습니다.

정책 서비스 API 내에서 모든 정책 및 마케팅 작업을 `core` 또는 `custom` 리소스라고 합니다. `core` 리소스는 Adobe에서 정의하고 유지 관리하는 반면, `custom` 리소스는 개별 고객이 만들고 유지 관리합니다. 따라서 이러한 `custom` 리소스는 해당 리소스를 만든 조직에서만 고유하며 볼 수 있습니다.

DULE Policy Service API에서 제공하는 주요 작업을 수행하는 방법에 대한 자세한 내용은 정책 [서비스 개발자 안내서를](../api/getting-started.md)참조하십시오. DULE 정책 작업에 대한 단계별 지침은 DULE 정책 [작성 및 평가에 대한 자습서를 참조하십시오](create.md).