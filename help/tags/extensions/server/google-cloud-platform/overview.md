---
title: Google Cloud Platform 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장은 Edge Network 이벤트를 Google Cloud Platform으로 전송합니다.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# [!DNL Google Cloud Platform] 이벤트 전달 확장 기능

[[!DNL Google Cloud Platform]](https://cloud.google.com/) 은 분산 컴퓨팅, 데이터베이스 스토리지, 컨텐츠 전달, CRM(고객 관계 관리) 및 ERP(전사적 자원 관리)를 위한 SaaS(Software-as-a-Service) 통합 서비스 등 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

다음 [!DNL Google Cloud Platform] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장에서 활용 [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) Adobe Experience Platform Edge Network의 이벤트를 [!DNL Google Cloud Platform] 추가 처리용. 이 안내서에서는 이벤트 전달 규칙에서 확장을 설치하고 기능을 사용하는 방법을 다룹니다.

## 전제 조건

이 확장을 사용하려면 [!DNL Google Cloud Platform] 기존 계정 [!DNL Cloud Pub/Sub] 주제. 기존 항목이 없는 경우 다음을 참조하십시오. [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) 항목 만들기 및 관리에 대한 설명서.

### 암호 및 데이터 요소 만들기

먼저, 새로 만들기 `Google OAuth 2` [이벤트 전달 암호](../../../ui/event-forwarding/secrets.md)값을 안전하게 유지하면서 계정에 대한 연결을 인증하는 데 사용됩니다.

다음, [데이터 요소 만들기](../../../ui/managing-resources/data-elements.md#create-a-data-element) 사용 **[!UICONTROL 코어]** 확장 및 a **[!UICONTROL 암호]** 참조할 데이터 요소 유형 `Google OAuth 2` 방금 생성한 암호.

## 설치 및 구성 [!DNL Google Cloud Platform] 확장 {#install}

확장을 설치하려면 [이벤트 전달 속성 만들기](../../../ui/event-forwarding/overview.md#properties) 또는 편집할 기존 속성을 대신 선택하십시오.

선택 **[!UICONTROL 확장]** 왼쪽 탐색. 다음에서 **[!UICONTROL 카탈로그]** 탭, 선택 **[!UICONTROL 설치]** 카드 사용 [!DNL Google Cloud Platform] 확장명.

![카탈로그 [!DNL Google Cloud Platform] 확장 강조 표시 설치.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

구성 화면에서 이전에 만든 데이터 요소 암호를 **[!UICONTROL 액세스 토큰]** 필드. 데이터 요소 암호에 [!DNL Google Cloud Platform] OAuth 2 토큰. 선택 **[!UICONTROL 저장]** 완료 시.

![다음 [!DNL Google Cloud Platform] 확장 구성 페이지입니다.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## 만들기 [!DNL Send Data to Cloud Pub/Sub] 규칙 {#tracking-rule}

확장이 설치되면 새 이벤트 전달을 만듭니다 [규칙](../../../ui/managing-resources/rules.md) 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 구성할 때 다음을 선택합니다 **[!UICONTROL Google 클라우드 플랫폼]** 확장을 선택한 다음 를 선택합니다 **[!UICONTROL Cloud Pub/Sub로 데이터 보내기]** 작업 유형.

![에 대한 작업 구성 보기 [!UICONTROL Google 클라우드 플랫폼], 작업이 강조 표시되고 [!UICONTROL Cloud Pub/Sub로 데이터 보내기].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 주제] | 이벤트 전달에서 이벤트를 받을 주제입니다. 값은 형식을 가져야 합니다. `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL 데이터] | 이 필드에는 로 전달할 데이터가 포함됩니다. [!DNL Cloud Pub/Sub] JSON 형식의 주제입니다.<br><br>아래 **[!UICONTROL Raw]** 옵션을 사용하면 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 세트 아이콘](../../../images/extensions/server/aws/data-element-icon.png))를 클릭하여 기존 데이터 요소 목록에서 데이터를 나타낼 수 있습니다.<br><br>다음을 사용할 수도 있습니다 **[!UICONTROL JSON 키-값 쌍 편집기]** ui 편집기를 통해 각 키-값 쌍을 수동으로 추가하는 옵션. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. |
| [!UICONTROL 속성] | 이 필드에는 메시지와 함께 보낼 추가 속성이 있는 JSON 오브젝트가 포함됩니다.<br><br>아래 **[!UICONTROL Raw]** 옵션을 사용하면 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 세트 아이콘](../../../images/extensions/server/aws/data-element-icon.png))를 클릭하여 기존 데이터 요소 목록에서 데이터를 나타낼 수 있습니다.<br><br>다음을 사용할 수도 있습니다 **[!UICONTROL JSON 키-값 쌍 편집기]** ui 편집기를 통해 각 키-값 쌍을 수동으로 추가하는 옵션. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. |

{style="table-layout:auto"}

## 다음 단계

이 안내서에서는 로 데이터를 보내는 방법을 다룹니다. [!DNL Cloud Pub/Sub] 사용 [!DNL Google Cloud Platform] 이벤트 전달 확장. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).