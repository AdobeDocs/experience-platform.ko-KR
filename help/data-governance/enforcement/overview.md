---
keywords: Experience Platform;홈;인기 항목;정책 적용;자동 적용;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 정책 실행 개요
topic-legacy: guide
description: 데이터 사용 레이블이 Adobe Experience Platform 데이터 세트에 적용되었고 해당 레이블에 대한 마케팅 작업을 위해 데이터 사용 정책이 정의된 경우 데이터 거버넌스 기능을 사용하여 이러한 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다. 플랫폼의 데이터 거버넌스 기능, API 기반의 적용 및 자동 실행으로 제공되는 두 가지 정책 실행 방법이 있습니다.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 정책 실행 개요

데이터 세트에 데이터 사용 레이블이 적용되고 해당 레이블에 대한 마케팅 작업을 위해 데이터 사용 정책이 정의되면 Adobe Experience Platform 데이터 거버넌스 기능을 사용하여 이러한 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다.

[!DNL Platform]의 [!DNL Data Governance] 기능에서 제공하는 2가지 정책 적용 방법이 있습니다.API 기반의 적용 및 자동 실행

## API 기반 적용

[!DNL Policy Service] API는 정책 위반이 발생하는지 확인하기 위해 데이터 세트 또는 임의 데이터 사용 레이블의 조합에 대한 마케팅 작업을 테스트할 수 있는 끝점을 제공합니다. 그런 다음 API 응답을 기준으로 경험 애플리케이션 내의 프로토콜을 설정하여 데이터 사용 정책 준수를 적절하게 적용할 수 있습니다.

API를 사용하여 정책을 평가하는 방법에 대한 자세한 내용은 [API 기반 적용](./api-enforcement.md)의 자습서를 참조하십시오.

## 자동 실행

Experience Platform은 데이터 계보, 데이터 분류 및 정책 관리 기능을 활용하여 정책 위반을 자동으로 평가하고 표시합니다. 자세한 내용은 [자동 정책 적용](./auto-enforcement.md)에 대한 개요를 참조하십시오.
