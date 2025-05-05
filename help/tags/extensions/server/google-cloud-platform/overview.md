---
title: Google Cloud Platform 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장은 Edge Network 이벤트를 Google Cloud Platform으로 전송합니다.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---

# [!DNL Google Cloud Platform] 이벤트 전달 확장 기능

[[!DNL Google Cloud Platform]](https://cloud.google.com/)은(는) CRM(고객 관계 관리) 및 ERP(전사적 자원 관리)를 위한 분산 컴퓨팅, 데이터베이스 스토리지, 컨텐츠 전달 및 SaaS(Software-as-a-Service) 통합 서비스와 같은 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

[!DNL Google Cloud Platform] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장은 [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub)을(를) 활용하여 추가 처리를 위해 Adobe Experience Platform Edge Network에서 [!DNL Google Cloud Platform] (으)로 이벤트를 보냅니다. 이 안내서에서는 이벤트 전달 규칙에서 확장을 설치하고 기능을 사용하는 방법을 다룹니다.

## 전제 조건

이 확장을 사용하려면 기존 [!DNL Cloud Pub/Sub] 주제가 있는 [!DNL Google Cloud Platform] 계정이 있어야 합니다. 기존 주제가 없는 경우 주제 만들기 및 관리에 대한 [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) 설명서를 참조하십시오.

### 암호 및 데이터 요소 만들기

먼저 값을 안전하게 유지하면서 계정에 대한 연결을 인증하는 데 사용할 새 `Google OAuth 2` [이벤트 전달 암호](../../../ui/event-forwarding/secrets.md)를 만듭니다.

그런 다음 **[!UICONTROL Core]** 확장 및 **[!UICONTROL Secret]** 데이터 요소 형식을 사용하여 [데이터 요소를 만듭니다](../../../ui/managing-resources/data-elements.md#create-a-data-element). 방금 만든 `Google OAuth 2` 암호를 참조합니다.

## [!DNL Google Cloud Platform] 확장 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 대신 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 [!DNL Google Cloud Platform] 확장의 카드에서 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![카탈로그 [!DNL Google Cloud Platform] 확장이 설치를 강조 표시합니다.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

구성 화면에서 **[!UICONTROL 액세스 토큰]** 필드에 이전에 만든 데이터 요소 암호를 입력하십시오. 데이터 요소 암호에 [!DNL Google Cloud Platform] OAuth 2 토큰이 포함됩니다. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![확장 구성 페이지 [!DNL Google Cloud Platform]입니다.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## [!DNL Send Data to Cloud Pub/Sub] 규칙 만들기 {#tracking-rule}

확장이 설치되면 새 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)을(를) 만들고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 구성할 때 **[!UICONTROL Google Cloud Platform]** 확장을 선택한 다음 작업 유형으로 **[!UICONTROL Cloud Pub/Sub로 데이터 보내기]**&#x200B;를 선택합니다.

![작업이 강조 표시된 [!UICONTROL Google Cloud Platform]에 대한 작업 구성 보기 및 [!UICONTROL Cloud Pub/Sub로 데이터 보내기].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 주제] | 이벤트 전달에서 이벤트를 받을 주제입니다. 값의 형식은 `projects/{projectName}/topics/{topicName}`이어야 합니다. |
| [!UICONTROL 데이터] | 이 필드에는 JSON 형식으로 [!DNL Cloud Pub/Sub] 주제에 전달될 데이터가 포함되어 있습니다.<br><br>**[!UICONTROL 원본]** 옵션에서 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 집합 아이콘](/help/images/icons/database.png))을 선택하여 기존 데이터 요소 목록에서 데이터를 나타낼 수 있습니다.<br><br>UI 편집기를 통해 각 키-값 쌍을 수동으로 추가하려면 **[!UICONTROL JSON 키-값 쌍 편집기]** 옵션을 사용할 수도 있습니다. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. |
| [!UICONTROL 특성] | 이 필드에는 메시지와 함께 보낼 추가 속성이 있는 JSON 오브젝트가 포함됩니다.<br><br>**[!UICONTROL 원본]** 옵션에서 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 집합 아이콘](/help/images/icons/database.png))을 선택하여 기존 데이터 요소 목록에서 데이터를 나타낼 수 있습니다.<br><br>UI 편집기를 통해 각 키-값 쌍을 수동으로 추가하려면 **[!UICONTROL JSON 키-값 쌍 편집기]** 옵션을 사용할 수도 있습니다. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. |

{style="table-layout:auto"}

## 다음 단계

이 안내서에서는 [!DNL Google Cloud Platform] 이벤트 전달 확장을 사용하여 [!DNL Cloud Pub/Sub]에 데이터를 보내는 방법을 다룹니다. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
