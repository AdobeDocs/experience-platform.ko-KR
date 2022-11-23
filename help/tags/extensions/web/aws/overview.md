---
title: AWS 확장 개요
description: Adobe Experience Platform에서 이벤트 전달을 위한 AWS 확장에 대해 알아봅니다.
source-git-commit: ac8fe0c0a5d061b34eee26db10883755234d0c1e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 4%

---

# [!DNL AWS] 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) 은 분산 컴퓨팅, 데이터베이스 스토리지, 콘텐츠 전달 및 CRM(고객 관계 관리)과 같은 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

다음 [!DNL AWS] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장 활용 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) Adobe Experience Platform Edge Network에서 로 이벤트를 전송하려면 [!DNL AWS] 추가 처리. 이 안내서에서는 확장을 설치하고 이벤트 전달 규칙에서 해당 기능을 사용하는 방법을 다룹니다.

## 전제 조건

다음을 수행해야 합니다. [!DNL AWS] 기존 [!DNL Kinesis] 이 확장을 사용하기 위한 데이터 스트림. 기존 데이터 스트림이 없는 경우 [!DNL AWS] 설명서 [를 사용하여 새 데이터 스트림 만들기 [!DNL AWS] 관리 콘솔](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## 확장 설치 {#install}

를 설치하려면 [!DNL AWS] 확장, 데이터 수집 UI 또는 Experience Platform UI로 이동하고 다음을 선택합니다 **[!UICONTROL 이벤트 전달]** 왼쪽 탐색에서 를 클릭합니다. 여기에서 확장을 추가할 속성을 선택하거나 대신 새 속성을 만듭니다.

원하는 속성을 선택하거나 만들었으면 을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색에서 **[!UICONTROL 카탈로그]** 탭. 을 검색합니다. [!UICONTROL AWS] 카드를 선택한 다음 **[!UICONTROL 설치]**.

![다음 [!UICONTROL 설치] 버튼 선택 중 [!UICONTROL AWS] 확장)을 클릭하여 제품에서 사용할 수 있습니다.](../../../images/extensions/aws/install.png)

다음 화면에서 다음에 대한 연결 자격 증명을 제공해야 합니다 [!DNL AWS] 계정이 필요합니다. 특히 [!DNL AWS] 키 ID 및 암호 액세스 키에 액세스합니다. 이 값을 모를 경우 [!DNL AWS] 설명서 [액세스 키 ID 및 비밀 액세스 키를 가져오는 방법](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![확장 구성 보기에 추가된 액세스 키 ID 및 암호 액세스 키.](../../../images/extensions/aws/credentials.png)

>[!IMPORTANT]
>
>액세스 정책을 [!DNL AWS] 액세스 자격 증명을 생성하는 데 사용되는 계정입니다. 이 정책은 액세스 권한을 부여하여 [!DNL Kinesis] 데이터 스트림. 을(를) 참조하십시오. **예제 2** 에서 [!DNL AWS] 문서 [정책 예 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) 정책을 정의하는 방법을 확인하십시오.

완료되면 을 선택합니다 **[!UICONTROL 저장]** 확장이 설치됩니다.

## 이벤트 전달 규칙 구성 {#rule}

확장을 설치한 후 새 이벤트 전달을 만듭니다 [규칙](../../../ui/managing-resources/rules.md) 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 구성할 때 **[!UICONTROL AWS]** 확장을 선택한 다음 **[!UICONTROL Kinesis 데이터 스트림으로 데이터 보내기]** 를 사용 중입니다.

![다음 [!UICONTROL Kinesis 데이터 스트림으로 데이터 보내기] 데이터 수집 UI에서 규칙에 대해 선택되는 작업 유형입니다.](../../../images/extensions/aws/select-action-type.png)

올바른 패널이 업데이트되어 데이터를 전송하는 방법에 대한 구성 옵션을 보여줍니다. 특히, [데이터 요소](../../../ui/managing-resources/data-elements.md) 를 나타내는 다양한 속성에 [!DNL Event Hub] 구성.

![에 대한 구성 옵션 [!UICONTROL Kinesis 데이터 스트림으로 데이터 보내기] UI에 표시된 작업 유형입니다.](../../../images/extensions/aws/data-stream-details.png)

**[!UICONTROL Kinesis 데이터 스트림 세부 정보]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 스트림 이름] | 이 이벤트 전달 규칙이 데이터 레코드를에 전송하는 스트림의 이름입니다. |
| [!UICONTROL AWS 지역] | 다음 [!DNL AWS] 지역 [!DNL Kinesis] 데이터 스트림이 만들어집니다. |
| [!UICONTROL 파티션 키] | 다음 [파티션 키](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) 확장 프로그램은 데이터를 데이터 스트림에 보낼 때 사용됩니다.<br><br>[!DNL Kinesis Data Streams] 스트림에 속하는 데이터 레코드를 여러 화면으로 구분합니다. 각 데이터 레코드와 함께 전송되는 파티션 키를 사용하여 지정된 데이터 레코드가 속한 분할자를 결정합니다.<br><br>각 고객에 대해 다르기 때문에 고객 배포에 적합한 파티션 키는 고객 번호일 수 있습니다. 낮은 파티션 키는 모두 근처 동일한 영역에 있을 수 있으므로 우편 번호를 사용할 수 있습니다. 일반적으로 서로 다른 잠재적 값의 범위가 가장 큰 파티션 키를 선택해야 합니다. 자세한 내용은 [!DNL AWS] 문서 [크기 조절 [!DNL Kinesis] 데이터 스트림](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 파티션 키 관리에 대한 우수 사례를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**[!UICONTROL 데이터]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 페이로드] | 이 필드에는 다음 위치로 전달될 데이터가 포함됩니다 [!DNL Kinesis] 데이터 스트림(JSON 형식)입니다.<br><br>아래에 **[!UICONTROL Raw]** 옵션을 사용하면 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘( )을 선택할 수 있습니다.![데이터 세트 아이콘](../../../images/extensions/aws/data-element-icon.png))을 클릭하여 기존 데이터 요소 목록에서 페이로드를 나타냅니다.<br><br>를 사용할 수도 있습니다 **[!UICONTROL JSON 키-값 쌍 편집기]** ui 편집기를 통해 각 키-값 쌍을 수동으로 추가하는 옵션. 각 값은 원시 입력으로 나타낼 수 있고 대신 데이터 요소를 선택할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

완료되면 을 선택합니다 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다. 규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**.

마지막으로 새 이벤트 전달 게시 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 다음 단계

이 안내서에서는 로 데이터를 전송하는 방법을 다룹니다 [!DNL Kinesis Data Streams] 사용 [!DNL AWS] 이벤트 전달 확장. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).
