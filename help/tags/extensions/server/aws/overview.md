---
title: AWS 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 AWS 확장에 대해 알아봅니다.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# [!DNL AWS] 확장 개요

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/)은(는) CRM(고객 관계 관리) 및 ERP(전사적 자원 관리)를 위한 분산 컴퓨팅, 데이터베이스 스토리지, 콘텐츠 전달 및 SaaS(Software-as-a-Service) 통합 서비스 등 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

[!DNL AWS] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장은 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)을(를) 활용하여 추가 처리를 위해 Adobe Experience Platform Edge Network에서 [!DNL AWS]&#x200B;(으)로 이벤트를 보냅니다. 이 안내서에서는 이벤트 전달 규칙에서 확장을 설치하고 기능을 사용하는 방법을 다룹니다.

## 전제 조건

이 확장을 사용하려면 기존 [!DNL AWS] 데이터 스트림을 가진 [!DNL Kinesis] 계정이 있어야 합니다. 기존 데이터 스트림이 없는 경우 [!DNL AWS]관리 콘솔을 사용하여 새 데이터 스트림 만들기[3}에 대한  [!DNL AWS]  설명서를 참조하십시오.](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html)

## 확장 설치 {#install}

[!DNL AWS] 확장을 설치하려면 데이터 수집 UI 또는 Experience Platform UI로 이동한 다음 왼쪽 탐색에서 **[!UICONTROL Event Forwarding]**&#x200B;을(를) 선택합니다. 여기에서 확장을 추가할 속성을 선택하거나 새 속성을 대신 만듭니다.

원하는 속성을 선택하거나 만들었으면 왼쪽 탐색에서 **[!UICONTROL Extensions]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Catalog]** 탭을 선택합니다. [!UICONTROL AWS] 카드를 검색한 다음 **[!UICONTROL Install]**&#x200B;을(를) 선택합니다.

![데이터 수집 UI에서 [!UICONTROL Install] 확장에 대해 [!UICONTROL AWS] 단추를 선택하고 있습니다.](../../../images/extensions/server/aws/install.png)

다음 화면에서는 [!DNL AWS] 계정에 대한 연결 자격 증명을 제공해야 합니다. 특히 [!DNL AWS] 액세스 키 ID와 비밀 액세스 키를 제공해야 합니다. 이러한 값을 모를 경우 [!DNL AWS]액세스 키 ID와 비밀 액세스 키를 얻는 방법[에 대한 ](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html) 설명서를 참조하십시오.

![확장 구성 보기에 추가된 액세스 키 ID 및 비밀 액세스 키입니다.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>액세스 자격 증명을 생성하는 데 사용되는 [!DNL AWS] 계정에 액세스 정책을 첨부해야 합니다. 데이터를 [!DNL Kinesis] 데이터 스트림으로 보낼 수 있는 액세스 권한을 부여하려면 이 정책을 구성해야 합니다. **예제 정책**[!DNL AWS]에 대한 [ 문서의  [!DNL Kinesis Data Streams]예제 2](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples)을(를) 참조하여 정책을 정의하는 방법을 확인하십시오.

완료되면 **[!UICONTROL Save]**&#x200B;을(를) 선택하고 확장이 설치되었습니다.

## 이벤트 전달 규칙 구성 {#rule}

확장을 설치한 후 새 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)을(를) 만들고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 구성할 때 **[!UICONTROL AWS]** 확장을 선택한 다음 작업 유형으로 **[!UICONTROL Send Data to Kinesis Data Stream]**&#x200B;을(를) 선택하십시오.

![데이터 수집 UI에서 규칙에 대해 [!UICONTROL Send Data to Kinesis Data Stream] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/aws/select-action-type.png)

오른쪽 패널이 업데이트되어 데이터를 전송하는 방법에 대한 구성 옵션을 표시합니다. 특히 [ 구성을 나타내는 다양한 속성에 ](../../../ui/managing-resources/data-elements.md)데이터 요소[!DNL Event Hub]를 할당해야 합니다.

![UI에 표시된 [!UICONTROL Send Data to Kinesis Data Stream] 작업 형식에 대한 구성 옵션입니다.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL Stream Name] | 이 이벤트 전달 규칙이 데이터 레코드를 보낼 스트림 이름입니다. |
| [!UICONTROL AWS Region] | [!DNL AWS] 데이터 스트림이 만들어지는 [!DNL Kinesis] 영역입니다. |
| [!UICONTROL Partition Key] | 데이터 스트림으로 데이터를 보낼 때 확장에서 사용할 [파티션 키](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key)입니다.<br><br>[!DNL Kinesis Data Streams]은(는) 스트림에 속하는 데이터 레코드를 여러 개의 조각으로 분리합니다. 각 데이터 레코드와 함께 전송되는 파티션 키를 사용하여 주어진 데이터 레코드가 속하는 분할을 결정합니다.<br><br>각 고객마다 다르므로 고객을 배포하기 위한 올바른 파티션 키가 고객 번호일 수 있습니다. 파티션 키가 좋지 않으면 모두 근처에 같은 지역에 거주할 수 있으므로 우편 번호가 낮을 수 있습니다. 일반적으로 서로 다른 잠재적 값의 범위가 가장 높은 파티션 키를 선택해야 합니다. 파티션 키 관리에 대한 모범 사례를 보려면 [!DNL AWS]데이터 스트림 크기 조정[의  [!DNL Kinesis] 에 대한 ](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 문서를 참조하십시오. |

{style="table-layout:auto"}

**[!UICONTROL Data]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL Payload] | 이 필드에는 JSON 형식의 [!DNL Kinesis] 데이터 스트림으로 전달될 데이터가 포함되어 있습니다.<br><br>**[!UICONTROL Raw]** 옵션에서 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 세트 아이콘](/help/images/icons/database.png))을 선택하여 페이로드를 나타낼 기존 데이터 요소 목록에서 선택할 수 있습니다.<br><br>UI 편집기를 통해 각 키-값 쌍을 수동으로 추가하려면 **[!UICONTROL JSON Key-Value Pairs Editor]** 옵션을 사용할 수도 있습니다. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. |

{style="table-layout:auto"}

완료되면 **[!UICONTROL Keep Changes]**&#x200B;을(를) 선택하여 작업을 규칙 구성에 추가합니다. 규칙에 만족하면 **[!UICONTROL Save to Library]**&#x200B;을(를) 선택합니다.

마지막으로 새 이벤트 전달 [build](../../../ui/publishing/builds.md)을(를) 게시하여 라이브러리에 대한 변경 사항을 활성화하십시오.

## 다음 단계

이 안내서에서는 [!DNL Kinesis Data Streams] 이벤트 전달 확장을 사용하여 [!DNL AWS]에 데이터를 보내는 방법을 다룹니다. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
