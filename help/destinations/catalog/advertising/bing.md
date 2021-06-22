---
keywords: '광고;bing; '
title: Microsoft Bing 연결
description: Microsoft Bing 연결 대상을 사용하면 Microsoft Display Advertising에서 리타겟팅 및 대상 타깃팅된 디지털 캠페인을 실행할 수 있습니다.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 2931efa6f67a042255fb1d31c0683f73d817b55b
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# [!DNL Microsoft Bing] 연결  {#bing-destination}

## 개요 {#overview}

[!DNL Microsoft Bing] 대상은 프로필 데이터를 [!DNL Microsoft Display Advertising]에 전송하는 데 도움이 됩니다.

프로필 데이터를 [!DNL Microsoft Bing]에 보내려면 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터는 [!DNL Microsoft Advertising IDs]으로 작성된 세그먼트를 사용하여 [!DNL Microsoft Advertising] 채널에서 디스플레이 광고를 통해 사용자를 타깃팅하고 싶습니다.

## 지원되는 ID {#supported-identities}

[!DNL Microsoft Bing] 은 아래 표에 설명된 id의 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 |
|---|---|
| 가정부 | Microsoft 광고 ID |

## 내보내기 유형 {#export-type}

**[!DNL Segment Export]** - 세그먼트(대상)의 모든 구성원을 대상으로  [!DNL Microsoft Bing] 내보냅니다.

## 전제 조건 {#prerequisites}

[!DNL Microsoft Bing]을(를) 사용하여 첫 번째 대상을 만들고 과거에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을 활성화하지 않은 경우(Adobe Audience Manager 또는 다른 애플리케이션 사용) Adobe 컨설팅이나 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL Microsoft Bing] 통합을 설정한 경우 설정한 ID 동기화를 Platform으로 이월합니다.

대상을 구성할 때 다음 정보를 제공해야 합니다.

* [!UICONTROL 계정 ID]:정수  [!DNL Bing Ads CID]형식으로 된 것입니다.

## 대상 {#connect-destination}에 연결

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;에서 [!DNL Microsoft Bing]을 선택하고 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![Microsoft Bing 대상 구성](../../assets/catalog/advertising/bing/configure.png)

이 대상과의 연결이 이미 있으면 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. **[!UICONTROL Activate]** 및 **[!UICONTROL Configure]**&#x200B;의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.

![Microsoft Bing 대상 활성화](../../assets/catalog/advertising/bing/activate.png)

## 인증 단계 {#authentication}

**[!UICONTROL 인증]** 단계에서 대상 연결 세부 정보를 입력해야 합니다.

* **[!UICONTROL 이름]**:나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**:나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**:사용자  [!DNL Bing Ads CID].
* **[!UICONTROL 마케팅 작업]**:마케팅 작업은 대상으로 데이터를 내보낼 의도를 나타냅니다. Adobe 정의 마케팅 작업에서 선택하거나 고유한 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [Adobe Experience Platform의 데이터 거버넌스](../../../data-governance/policies/overview.md) 페이지를 참조하십시오. 개별 Adobe 정의 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

![Microsoft Bing 대상 인증](../../assets/catalog/advertising/bing/authentication.png)

**[!UICONTROL 대상 만들기]**&#x200B;를 클릭합니다. 이제 대상이 생성되었습니다. 나중에 세그먼트를 활성화하려면 [!UICONTROL 저장 및 종료]를 클릭하거나 [!UICONTROL 다음]을 클릭하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 어느 경우든 나머지 워크플로우에는 다음 섹션인 [세그먼트 활성화](#activate-segments)를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 워크플로우에 대한 자세한 내용은 [대상에 프로필 및 세그먼트 활성화](../../ui/activate-destinations.md#select-attributes)를 참조하십시오.

[세그먼트 예약](../../ui/activate-destinations.md#segment-schedule) 단계에서 세그먼트를 대상의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑할 때는 쉽게 사용할 수 있도록 [!DNL Platform] 세그먼트 이름 또는 더 짧은 형식의 세그먼트를 사용하는 것이 좋습니다. 그러나 대상의 세그먼트 ID나 이름은 [!DNL Platform] 계정의 세그먼트 ID와 일치하지 않아도 됩니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

![세그먼트 매핑 ID](../../assets/common/segment-mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Microsoft Bing] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Microsoft Bing Ads] 계정을 확인하십시오. 활성화가 성공하면 계정에 대상이 채워집니다.
