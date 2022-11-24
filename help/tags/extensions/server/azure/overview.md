---
title: Microsoft Azure 확장 개요
description: Adobe Experience Platform에서 이벤트 전달을 위한 Microsoft Azure 확장에 대해 알아봅니다.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---

# [!DNL Microsoft Azure] 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

in [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) 는 연결된 디바이스 및 애플리케이션에서 생성된 대량의 데이터를 처리 및 분석할 수 있는 확장성이 뛰어난 실시간 데이터 수집 서비스입니다. 데이터가 이벤트 허브로 수집되면 실시간 분석 공급자나 일괄 처리/스토리지 어댑터를 사용하여 데이터를 변환하여 저장할 수 있습니다.

다음 [!DNL Microsoft Azure] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장 활용 [!DNL Event Hubs] Adobe Experience Platform Edge Network에서 로 이벤트를 전송하려면 [!DNL Azure] 추가 처리. 이 안내서에서는 확장을 설치하고 이벤트 전달 규칙에서 해당 기능을 사용하는 방법을 다룹니다.

## 전제 조건

이 확장을 사용하려면 유효한 가 있어야 합니다 [!DNL Azure] 액세스 권한이 있는 계정 [!DNL Event Hubs]. 또한 [를 사용하여 이벤트 허브 만들기 [!DNL Azure] 포털](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) 를 클릭하여 제품에서 사용할 수 있습니다.

## 확장 설치

Microsoft을 설치하려면 [!DNL Azure] 확장, 데이터 수집 UI 또는 Experience Platform UI로 이동하고 다음을 선택합니다 **[!UICONTROL 이벤트 전달]** 왼쪽 탐색에서 를 클릭합니다. 여기에서 확장을 추가할 속성을 선택하거나 대신 새 속성을 만듭니다.

원하는 속성을 선택하거나 만들었으면 을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색에서 **[!UICONTROL 카탈로그]** 탭. 을 검색합니다. [!UICONTROL Microsoft Azure] 카드를 선택한 다음 **[!UICONTROL 설치]**.

![다음 [!UICONTROL 설치] 버튼 선택 중 [!UICONTROL Microsoft Azure] 확장)을 클릭하여 제품에서 사용할 수 있습니다.](../../../images/extensions/server/azure/install.png)

확장에는 구성 속성이 없으므로 설치된 확장 목록에 즉시 추가됩니다. 이제 다음을 사용할 수 있습니다 [!DNL Event Hub] 이벤트 전달 규칙을 구성할 때 작업 유형.

## 이벤트 전달 규칙 구성 {#rule}

새 이벤트 전달 규칙 만들기를 시작하고 원하는 대로 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 **[!UICONTROL Microsoft Azure]** 확장을 위해 를 선택한 다음 **[!UICONTROL 이벤트 허브에 데이터 보내기]** 용.

![다음 [!UICONTROL 이벤트 허브에 데이터 보내기] 데이터 수집 UI에서 규칙에 대해 선택되는 작업 유형입니다.](../../../images/extensions/server/azure/select-action-type.png)

올바른 패널이 업데이트되어 데이터를 전송하는 방법에 대한 구성 옵션을 보여줍니다. 특히, [데이터 요소](../../../ui/managing-resources/data-elements.md) 를 나타내는 다양한 속성에 [!DNL Event Hub] 구성.

![에 대한 구성 옵션 [!UICONTROL 이벤트 허브에 데이터 보내기] UI에 표시된 작업 유형입니다.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL 이벤트 허브 세부 정보]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 네임스페이스] | 의 이름 [!DNL Event Hubs] 네임스페이스를 만들 때 [이벤트 허브 설정](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL 이름] | 이벤트 허브의 이름입니다. |
| [!UICONTROL SAS 인증 규칙 이름] | 전체 액세스 권한 부여 규칙의 이름입니다. [!DNL Event Hubs] 네임스페이스 또는 데이터를 보낼 특정 이벤트 허브 인스턴스입니다. 의 부록 섹션을 참조하십시오. [SAS 인증 값 가져오기](#sas) 추가 정보. |
| [!UICONTROL SAS 액세스 키] | 전체 공유 액세스 권한 부여 규칙의 기본 키 [!DNL Event Hubs] 네임스페이스 또는 데이터를 보낼 특정 이벤트 허브 인스턴스입니다. 의 부록 섹션을 참조하십시오. [SAS 인증 값 가져오기](#sas) 추가 정보. |
| [!UICONTROL 파티션 ID] | [!DNL Event Hubs] 을(를) 통해 [특정 파티션으로 직접 이벤트 보내기](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). 이 기능을 활용하려면 이벤트를 받을 파티션의 ID를 제공합니다. |

{style=&quot;table-layout:auto&quot;}

**데이터**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 페이로드] | 이 필드에는 다음 위치로 전달될 데이터가 포함됩니다 [!DNL Event Hubs]. 데이터는 JSON 개체, 문자열 또는 데이터 요소일 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

완료되면 을 선택합니다 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다. 규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**.

마지막으로 새 이벤트 전달 게시 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 다음 단계

이 안내서에서는 로 데이터를 전송하는 방법을 다룹니다 [!DNL Event Hubs] 사용 [!DNL Microsoft Azure] 이벤트 전달 확장. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).

## 부록: SAS 인증 값 획득 {#sas}

외부 응용 프로그램에는 [!DNL Event Hubs] through [공유 액세스 서명(SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). 각 [!DNL Event Hubs] 네임스페이스 및 이벤트 허브 인스턴스에는 생성 시 자동으로 기본 SAS 인증 규칙이 지정되지만 원할 경우 각 리소스에 대한 추가 정책을 만들 수도 있습니다.

When [이벤트 전달 규칙 구성](#rule) 사용 [!DNL Azure] 확장을 사용하려면 데이터를 보낼 네임스페이스 또는 특정 이벤트 허브를 제어하는 인증 규칙의 이름 및 기본 키를 제공해야 합니다. 에서 이러한 값을 가져오는 방법에 대한 자세한 내용은 [!DNL Azure] 포털에서 다음 섹션을 참조하십시오 [!DNL Azure] 설명서:

* [에 대한 SAS 값 가져오기 [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [네임스페이스에서 특정 이벤트 허브에 대한 SAS 값 가져오기](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

필요한 값이 있으면 구성 입력에서 인증 규칙 이름을 문자열로 직접 제공하거나 문자열 유형 데이터 요소를 만들어 대신 참조할 수 있습니다. 그러나 데이터 보안을 위해 규칙 구성에서 제공하려면 먼저 기본 키가 이벤트 전달 암호 내에 포함되어야 합니다.

이벤트 전달 UI 내에서 [새 암호 만들기](../../../ui/event-forwarding/secrets.md) 을(를) 선택합니다. **[!UICONTROL 토큰]** 비밀 종류로 토큰 값 자체에 대해 이전에 복사한 기본 키를 제공합니다. 암호를 만든 후 유형을 사용하여 데이터 요소를 만듭니다 **[!UICONTROL 비밀]** 을(를) 선택하고 을(를) 선택합니다. [!DNL Event Hubs] 비밀입니다. 비밀 데이터 요소가 설정되면 **[!UICONTROL SAS 액세스 키]** 필드.
