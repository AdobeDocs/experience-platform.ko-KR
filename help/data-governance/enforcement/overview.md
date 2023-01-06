---
keywords: Experience Platform;홈;인기 항목;정책 적용;자동 적용;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 정책 적용 개요
description: Adobe Experience Platform에서 데이터 사용 정책이 적용되는 방법을 알아봅니다.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 정책 적용 개요

한 번 [데이터 사용 레이블](../labels/overview.md) 이 적용되었으며 [데이터 사용 정책](../policies/overview.md) 가 정의되어 있으면 정책 위반을 구성하는 데이터 작업을 방지하기 위해 이러한 정책을 적용할 수 있습니다.

>[!NOTE]
>
>이 문서에서는 데이터 사용 정책 적용에 중점을 둡니다. 액세스 제어 정책에 대한 자세한 내용은 [속성 기반 액세스 제어](../../access-control/abac/overview.md).

Adobe Experience Platform에서 정책을 적용하는 방법에는 두 가지가 있습니다. 자동 적용 및 API 기반 적용.

## 자동 적용

Experience Platform은 데이터 계보, 데이터 분류 및 정책 관리 기능을 활용하여 정책 위반을 자동으로 평가하고 표시합니다. 다음 사항에 대한 개요를 참조하십시오. [자동 정책 적용](./auto-enforcement.md) 추가 정보.

## API 기반 적용

다음 [!DNL Policy Service] API는 정책 위반이 발생하는지 확인하기 위해 데이터 세트 또는 데이터 사용 레이블의 임의 조합에 대한 마케팅 작업을 테스트할 수 있는 엔드포인트를 제공합니다. API 응답을 기반으로 경험 애플리케이션 내에 프로토콜을 설정하여 데이터 거버넌스 정책 준수를 적절하게 적용할 수 있습니다.

다음에서 자습서를 참조하십시오. [API 기반 적용](./api-enforcement.md) api를 사용하여 정책을 평가하는 방법에 대한 단계를 설명합니다.
