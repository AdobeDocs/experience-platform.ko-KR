---
title: Microsoft Azure 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 Microsoft Azure 확장에 대해 알아봅니다.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# [!DNL Microsoft Azure] 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

[!DNL Microsoft Azure]에서 [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview)은(는) 연결된 장치 및 응용 프로그램에서 생성되는 대량의 데이터를 처리하고 분석할 수 있도록 해주는 확장성이 뛰어난 실시간 데이터 수신 서비스입니다. 이벤트 허브에 데이터가 수집되면 실시간 분석 공급자나 일괄 처리/스토리지 어댑터를 사용하여 데이터를 변환하고 저장할 수 있습니다.

[!DNL Microsoft Azure] [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장은 [!DNL Event Hubs]을(를) 활용하여 추가 처리를 위해 Adobe Experience Platform Edge Network에서 [!DNL Azure] (으)로 이벤트를 보냅니다. 이 안내서에서는 이벤트 전달 규칙에서 확장을 설치하고 기능을 사용하는 방법을 다룹니다.

## 전제 조건

이 확장을 사용하려면 [!DNL Event Hubs]에 액세스할 수 있는 올바른 [!DNL Azure] 계정이 있어야 합니다. 또한 아래 단계를 수행하기 전에 [ [!DNL Azure] 포털](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create)을 사용하여 이벤트 허브를 만들어야 합니다.

## 확장 설치

Microsoft [!DNL Azure] 확장을 설치하려면 데이터 수집 UI 또는 Experience Platform UI로 이동한 다음 왼쪽 탐색에서 **[!UICONTROL 이벤트 전달]**&#x200B;을 선택합니다. 여기에서 확장을 추가할 속성을 선택하거나 새 속성을 대신 만듭니다.

원하는 속성을 선택하거나 만든 후에는 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. [!UICONTROL Microsoft Azure] 카드를 검색한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![데이터 수집 UI에서 [!UICONTROL Microsoft Azure] 확장에 대해 [!UICONTROL 설치] 단추를 선택하고 있습니다.](../../../images/extensions/server/azure/install.png)

확장에는 구성 속성이 없으므로 설치된 확장 목록에 즉시 추가됩니다. 이제 이벤트 전달 규칙을 구성할 때 [!DNL Event Hub] 작업 유형을 사용할 수 있습니다.

## 이벤트 전달 규칙 구성 {#rule}

새 이벤트 전달 규칙 만들기를 시작하고 원하는 대로 해당 조건을 구성합니다. 규칙에 대한 작업을 선택할 때 확장에 대해 **[!UICONTROL Microsoft Azure]**&#x200B;를 선택한 다음 작업 유형에 대해 **[!UICONTROL 이벤트 허브에 데이터 보내기]**&#x200B;를 선택합니다.

![데이터 수집 UI에서 규칙에 대해 [!UICONTROL 이벤트 허브에 데이터 보내기] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/azure/select-action-type.png)

오른쪽 패널이 업데이트되어 데이터를 전송하는 방법에 대한 구성 옵션을 표시합니다. 특히 [!DNL Event Hub] 구성을 나타내는 다양한 속성에 [데이터 요소](../../../ui/managing-resources/data-elements.md)를 할당해야 합니다.

![UI에 표시되는 [!UICONTROL 이벤트 허브에 데이터 보내기] 작업 유형에 대한 구성 옵션입니다.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL 이벤트 허브 세부 정보]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 네임스페이스] | [이벤트 허브를 설정](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)할 때 만든 [!DNL Event Hubs] 네임스페이스의 이름입니다. |
| [!UICONTROL 이름] | 이벤트 허브의 이름입니다. |
| [!UICONTROL SAS 인증 규칙 이름] | 전체 [!DNL Event Hubs] 네임스페이스 또는 데이터를 보낼 특정 이벤트 허브 인스턴스에 대한 공유 액세스 권한 부여 규칙의 이름입니다. 자세한 내용은 [SAS 인증 값 가져오기](#sas)에 대한 부록 섹션을 참조하십시오. |
| [!UICONTROL SAS 액세스 키] | 전체 [!DNL Event Hubs] 네임스페이스 또는 데이터를 보낼 특정 이벤트 허브 인스턴스에 대한 공유 액세스 권한 부여 규칙의 기본 키입니다. 자세한 내용은 [SAS 인증 값 가져오기](#sas)에 대한 부록 섹션을 참조하십시오. |
| [!UICONTROL 파티션 ID] | [!DNL Event Hubs]을(를) 사용하면 [특정 파티션으로 직접 이벤트를 전송](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka)할 수 있습니다. 이 기능을 활용하려면 이벤트를 받을 파티션의 ID를 입력하십시오. |

{style="table-layout:auto"}

**데이터**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 페이로드] | 이 필드에는 [!DNL Event Hubs] (으)로 전달될 데이터가 포함되어 있습니다. 데이터는 JSON 개체, 문자열 또는 데이터 요소일 수 있습니다. |

{style="table-layout:auto"}

완료되면 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 작업을 규칙 구성에 추가합니다. 규칙에 만족하면 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다.

마지막으로 새 이벤트 전달 [build](../../../ui/publishing/builds.md)을(를) 게시하여 라이브러리에 대한 변경 사항을 활성화하십시오.

## 다음 단계

이 안내서에서는 [!DNL Microsoft Azure] 이벤트 전달 확장을 사용하여 [!DNL Event Hubs]에 데이터를 보내는 방법을 다룹니다. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.

## 부록: SAS 인증 값 얻기 {#sas}

외부 응용 프로그램에는 [SAS(공유 액세스 서명)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature)을(를) 통해 [!DNL Event Hubs]에 대한 액세스 권한이 부여됩니다. 각 [!DNL Event Hubs] 네임스페이스 및 이벤트 허브 인스턴스에는 생성 시 자동으로 할당된 기본 SAS 권한 부여 규칙이 있지만 원하는 경우 각 리소스에 대해 추가 정책을 만들 수도 있습니다.

[이벤트 전달 규칙을 구성](#rule)할 때 [!DNL Azure] 확장을 사용하면 데이터를 보낼 네임스페이스 또는 특정 이벤트 허브를 제어하는 권한 부여 규칙의 이름과 기본 키를 제공해야 합니다. [!DNL Azure] 포털에서 이러한 값을 가져오는 방법에 대한 자세한 내용은 [!DNL Azure] 설명서의 다음 섹션을 참조하십시오.

* [네임스페이스에 대한 SAS 값 가져오기 [!DNL Event Hubs] 네임스페이스](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [네임스페이스의 특정 이벤트 허브에 대한 SAS 값 가져오기](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

필요한 값이 있으면 구성 입력에서 권한 부여 규칙 이름을 문자열로 직접 제공하거나 대신 참조할 문자열 유형 데이터 요소를 만들 수 있습니다. 그러나 기본 키는 데이터 보안을 보호하기 위해 규칙 구성에서 제공되기 전에 먼저 이벤트 전달 암호 내에 포함되어야 합니다.

이벤트 전달 UI 내에서 [새 암호를 만들고](../../../ui/event-forwarding/secrets.md) **[!UICONTROL 토큰]**&#x200B;을 암호 유형으로 선택하십시오. 토큰 값 자체에 대해 이전에 복사한 기본 키를 제공합니다. 암호를 만든 후 **[!UICONTROL 암호]** 형식의 데이터 요소를 만들고 목록에서 [!DNL Event Hubs] 암호를 선택하십시오. 비밀 데이터 요소가 설정되면 **[!UICONTROL SAS 액세스 키]** 필드에서 해당 데이터 요소를 참조할 수 있습니다.
