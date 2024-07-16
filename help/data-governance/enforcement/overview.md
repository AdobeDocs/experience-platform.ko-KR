---
keywords: Experience Platform;홈;인기 항목;정책 적용;자동 적용;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 정책 시행 개요
description: Adobe Experience Platform에서 데이터 사용 정책을 적용하는 방법에 대해 알아봅니다.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 정책 시행 개요

[데이터 사용 레이블](../labels/overview.md)이 적용되고 [데이터 사용 정책](../policies/overview.md)이 정의되면 정책 위반을 구성하는 데이터 작업을 방지하기 위해 이러한 정책을 적용할 수 있습니다.

>[!NOTE]
>
>이 문서는 데이터 사용 정책 시행에 중점을 두고 있습니다. 액세스 제어 정책에 대한 자세한 내용은 [특성 기반 액세스 제어](../../access-control/abac/overview.md)에 대한 안내서를 참조하세요.

Adobe Experience Platform에서 정책을 집행하는 방법에는 자동 집행과 API 기반 집행의 두 가지가 있습니다.

## 자동 적용

Experience Platform은 데이터 계보, 데이터 분류 및 정책 관리 기능을 활용하여 정책 위반을 자동으로 평가하고 표시합니다. 자세한 내용은 [자동 정책 적용](./auto-enforcement.md)에 대한 개요를 참조하십시오.

## API 기반 적용

[!DNL Policy Service] API는 정책 위반이 있는지 확인하기 위해 데이터 세트 또는 데이터 사용 레이블의 임의 조합에 대한 마케팅 작업을 테스트할 수 있는 끝점을 제공합니다. 그런 다음 API 응답을 기반으로 경험 애플리케이션 내에서 프로토콜을 설정하여 데이터 거버넌스 정책 준수를 적절하게 적용할 수 있습니다.

API를 사용하여 정책을 평가하는 방법에 대한 단계는 [API 기반 적용](./api-enforcement.md)에 대한 자습서를 참조하십시오.
