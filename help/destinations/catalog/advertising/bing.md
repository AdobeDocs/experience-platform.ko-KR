---
keywords: '광고;bing; '
title: Microsoft Bing 연결
description: Microsoft Bing 연결 대상을 사용하여 Microsoft 디스플레이 광고에서 리타깃팅 및 대상 타깃팅된 디지털 캠페인을 실행할 수 있습니다.
translation-type: tm+mt
source-git-commit: 0ef107963f7da377070eb845fd7c24218a99464b
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# [!DNL Microsoft Bing] 연결  {#bing-destination}

[!DNL Microsoft Bing] 대상은 프로필 데이터를 [!DNL Microsoft Display Advertising]에 보내는 데 도움이 됩니다.

프로필 데이터를 [!DNL Microsoft Bing]에 보내려면 먼저 대상에 연결해야 합니다.

## 대상 사양 {#destination-specs}

[!DNL Microsoft Bing] 대상에 대한 다음 세부 사항을 참조하십시오.

* 다음 [id](../../../identity-service/namespaces.md)를 [!DNL Microsoft Bing] 대상으로 보낼 수 있습니다.[!DNL Microsoft ID].

>[!IMPORTANT]
>
>[!DNL Microsoft Bing]을(를) 사용하여 첫 번째 대상을 만들고 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을(를) 활성화하지 않은 경우(Adobe Audience Manager 또는 다른 응용 프로그램에서) Adobe 컨설팅 또는 고객 지원 센터에 문의하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL Microsoft Bing] 통합을 설정한 경우 설정한 ID 동기화가 플랫폼으로 이월됩니다.

## 사용 사례 {#use-cases}

마케터로서 [!DNL Microsoft Advertising IDs]을(를) 기반으로 구축된 세그먼트를 사용하여 [!DNL Microsoft Advertising] 채널에 디스플레이 광고를 통해 사용자를 타깃팅할 수 있기를 바랍니다.

## 내보내기 유형 {#export-type}

**[!DNL Segment Export]** - 세그먼트(대상)의 모든 구성원을 대상으로  [!DNL Microsoft Bing] 내보냅니다.

## 전제 조건 {#prerequisites}

대상을 구성할 때 다음 정보를 제공해야 합니다.

* [!UICONTROL 계정 ID]:정수 형식 [!DNL Bing Ads CID]으로 표시됩니다.

## 대상 {#connect-destination}에 연결

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;에서 [!DNL Microsoft Bing]를 선택하고 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![Microsoft Bing 대상 구성](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시될 수 있습니다. **[!UICONTROL 활성화]**&#x200B;와 **[!UICONTROL 구성]**&#x200B;의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.
>
>![Microsoft Bing 대상 활성화](../../assets/catalog/advertising/bing/activate.png)

[!UICONTROL 인증] 단계에서 대상 연결 세부 정보를 입력해야 합니다.

* **[!UICONTROL 이름]**:나중에 이 대상을 인식할 이름.
* **[!UICONTROL 설명]**:나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**:고객 [!DNL Bing Ads CID]의
* **[!UICONTROL 마케팅 작업]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 Adobe Experience Platform](../../../data-governance/policies/overview.md) 페이지의 [데이터 거버넌스 페이지를 참조하십시오. 개별 Adobe 정의 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

![Microsoft Bing 대상 인증](../../assets/catalog/advertising/bing/authentication.png)

**[!UICONTROL 대상 만들기]**&#x200B;를 클릭합니다. 이제 대상이 만들어집니다. 나중에 세그먼트를 활성화하려면 [!UICONTROL 저장 및 종료]을 클릭하고, [!UICONTROL 다음]을 클릭하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 이 두 경우 모두 나머지 워크플로에 대해 다음 섹션 [세그먼트 활성화](#activate-segments)를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md#select-attributes)에 활성화를 참조하십시오.

[세그먼트 일정](../../ui/activate-destinations.md#segment-schedule) 단계에서 세그먼트를 대상의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑하는 경우 사용하기 쉽도록 [!DNL Platform] 세그먼트 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 그러나 대상의 세그먼트 ID 또는 이름은 [!DNL Platform] 계정의 세그먼트 ID와 일치할 필요가 없습니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

![세그먼트 매핑 ID](../../assets/common/segment-mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Microsoft Bing] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Microsoft Bing Ads] 계정을 확인하십시오. 활성화가 성공하면 고객이 계정에 채워집니다.