---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 정책 서비스 API 안내서
description: Experience Platform 서비스 API를 통해 개발자는 정책 의 데이터 사용 레이블 및 정책을 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# [!DNL Policy Service] API 안내서

Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. 내에서 중요한 역할을 합니다. [!DNL Experience Platform] 카탈로그 작성, 데이터 계보, 데이터 사용 레이블 지정, 데이터 사용 정책 및 마케팅 작업을 위한 데이터 사용 제어 등 다양한 수준에서 사용됩니다.

다음 [!DNL Policy Service] API는 데이터 사용 레이블 및 정책을 프로그래밍 방식으로 관리하고 정책 위반에 대한 마케팅 작업을 평가할 수 있는 몇 가지 끝점을 제공합니다. 이러한 엔드포인트는 아래에 요약되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 참조하고 [시작 안내서](./getting-started.md) 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 제공합니다.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [[!DNL Policy Service] API Swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## 레이블

데이터 사용 레이블을 스키마에 적용하여 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트 및 필드를 분류합니다. 레이블은 언제든지 적용할 수 있으므로 데이터를 제어하는 방법을 유연하게 선택할 수 있습니다. 우수 사례는에 데이터가 수집되는 즉시 레이블 지정을 장려합니다. [!DNL Experience Platform]또는 에서 데이터를 사용할 수 있게 되는 즉시 [!DNL Platform]. 다음을 사용하여 레이블을 만들고, 보고, 편집하고, 삭제할 수 있습니다 `/labels` 엔드포인트. 이 끝점을 사용하는 방법을 알아보려면 다음을 방문하십시오. [labels endpoint 안내서](./labels.md).

## 마케팅 액션

데이터 거버넌스 프레임워크의 컨텍스트에서 마케팅 작업(마케팅 사용 사례라고도 함)은 [!DNL Experience Platform] 데이터 소비자는 조직에서 데이터 사용을 제한하려는 조치를 취할 수 있습니다. 마케팅 작업 작업에 대한 자세한 내용은 [마케팅 액션 엔드포인트 안내서](./marketing-actions.md).

## 정책

데이터 거버넌스 정책은 내 데이터 수행을 허용하거나 제한하는 마케팅 작업 종류를 설명하는 규칙입니다 [!DNL Experience Platform].

>[!NOTE]
>
>데이터 거버넌스 정책은 조직의 특정 플랫폼 사용자가 액세스할 수 있는 특정 데이터 속성을 결정하는 액세스 제어 정책과 혼동하지 않도록 합니다. 다음 안내서를 참조하십시오 [속성 기반 액세스 제어](../../access-control/abac/overview.md) 추가 정보.

데이터 거버넌스 정책은 다음과 같이 정의됩니다.

1. 특정 마케팅 액션
1. 작업이 수행되는 것이 제한되는 데이터 사용 레이블

API에서 정책을 관리하는 방법에 대해 알아보려면 다음을 참조하십시오. [정책 끝점 안내서](./policies.md)

## 평가

데이터 사용 레이블이 Platform 스키마에 적용되고, 데이터 사용 정책이 해당 레이블에 대한 마케팅 작업에 대해 정의되면 데이터 거버넌스 기능을 사용하여 이러한 정책을 시행하고 정책 위반을 구성하는 데이터 작업을 방지할 수 있습니다.

다음 [!DNL Policy Service] API는 정책 위반이 발생하는지 확인하기 위해 데이터 세트 또는 데이터 사용 레이블의 임의 조합에 대한 마케팅 작업을 테스트할 수 있는 끝점을 제공합니다. 그런 다음 API 응답을 기반으로 경험 애플리케이션 내에서 프로토콜을 설정하여 데이터 사용 정책 준수를 적절하게 적용할 수 있습니다. 다음을 참조하십시오. [평가 엔드포인트 안내서](./evaluation.md) 추가 정보.

## 다음 단계

을 사용하여 호출을 시작하려면 [!DNL Policy Service] API, 읽기 [시작 안내서](./getting-started.md) 그런 다음 엔드포인트 가이드 중 하나를 선택하여 특정 엔드포인트를 사용하는 방법을 알아봅니다. 를 사용하여 레이블 및 정책으로 작업하려면 [!DNL Experience Platform] UI, 다음을 참조하십시오. [레이블 사용 안내서](../labels/user-guide.md) 및 [정책 사용 안내서](../policies/user-guide.md), 각각
