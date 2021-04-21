---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 정책 서비스 API 안내서
topic-legacy: developer guide
description: 개발자는 정책 서비스 API를 사용하여 Experience Platform에서 데이터 사용 레이블 및 정책을 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# [!DNL Policy Service] API 안내서

Adobe Experience Platform [!DNL Data Governance]을 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. 카탈로그 작성, 데이터 계보, 데이터 사용 표시, 데이터 사용 정책, 데이터 사용 정책, 마케팅 작업에 대한 데이터 사용 제어 등 다양한 수준에서 [!DNL Experience Platform] 내에서 주요 역할을 합니다.

[!DNL Policy Service] API는 정책 위반에 대한 마케팅 작업을 평가할 뿐만 아니라 데이터 사용 레이블 및 정책을 프로그래밍 방식으로 관리할 수 있는 여러 끝점을 제공합니다. 이러한 끝점은 아래에 요약되어 있습니다. 자세한 내용은 개별 끝점 안내선을 참조하고 [시작 안내서](./getting-started.md)에서 필수 머리글, 샘플 API 호출 읽기 등에 대한 중요한 정보를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [[!DNL Policy Service] API swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)를 방문하십시오.

## 레이블

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터 관리 방식을 유연하게 선택할 수 있습니다. 우수 사례는 [!DNL Experience Platform]으로 인제스트되거나 [!DNL Platform]에서 데이터를 사용할 수 있게 되는 즉시 레이블 지정 데이터를 권장합니다. `/labels` 끝점을 사용하여 레이블을 만들고, 보고, 편집하고, 삭제할 수 있습니다. 이 끝점을 사용하는 방법에 대해 알아보려면 [레이블 끝점 안내서](./labels.md)를 방문하십시오.

## 마케팅 작업

마케팅 작업(마케팅 사용 사례라고도 함)은 [!DNL Data Governance] 프레임워크의 컨텍스트에서 사용자가 [!DNL Experience Platform] 데이터 소비자가 할 수 있는 작업으로 조직에서 데이터 사용을 제한하려는 것입니다. 마케팅 작업 작업에 대한 자세한 내용은 [마케팅 작업 끝점 안내서](./marketing-actions.md)를 참조하십시오.

## 정책

데이터 사용 정책은 [!DNL Experience Platform] 내의 데이터에 대해 수행하도록 허용되거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다. 정책은 다음과 같이 정의됩니다.

1. 특정 마케팅 작업
1. 작업이 제한되는 데이터 사용 레이블

API에서 정책을 관리하는 방법에 대해 알아보려면 [정책 끝점 안내서](./policies.md)를 참조하십시오.

## 평가

데이터 사용 레이블이 [!DNL Platform] 데이터 세트에 적용되었고 해당 레이블에 대한 마케팅 작업을 위해 데이터 사용 정책이 정의된 경우 데이터 거버넌스 기능을 사용하여 이러한 정책을 적용하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다.

[!DNL Policy Service] API는 정책 위반이 발생하는지 확인하기 위해 데이터 세트 또는 임의 데이터 사용 레이블의 조합에 대한 마케팅 작업을 테스트할 수 있는 끝점을 제공합니다. 그런 다음 API 응답을 기준으로 경험 애플리케이션 내의 프로토콜을 설정하여 데이터 사용 정책 준수를 적절하게 적용할 수 있습니다. 자세한 내용은 [평가 끝점 안내서](./evaluation.md)를 참조하십시오.

## 다음 단계

[!DNL Policy Service] API를 사용하여 호출을 시작하려면 [시작 안내서](./getting-started.md)를 읽은 다음 끝점 안내선 중 하나를 선택하여 특정 끝점의 사용 방법을 학습합니다. [!DNL Experience Platform] UI를 사용하여 레이블 및 정책을 사용하려면 각각 [레이블 사용자 안내서](../labels/user-guide.md) 및 [정책 사용자 안내서](../policies/user-guide.md)를 참조하십시오.
