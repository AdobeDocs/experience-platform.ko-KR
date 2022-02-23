---
title: Experience Platform Web SDK에 대한 데이터 스트림 구성
description: '데이터 스트림을 구성하는 방법을 알아봅니다. '
keywords: 구성;데이터 스트림;데이터 스트림 ID;에지;데이터 스트림 ID;환경 설정;edgeConfigId;id;ID 동기화 사용;ID 동기화 컨테이너 ID;샌드박스;스트리밍 입력;이벤트 데이터 세트;target;클라이언트 코드;속성 토큰;Target 환경 ID;쿠키 대상;URL 대상;Analytics 설정 차단 보고서 세트 ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 1b3022d892ea4421e0ddd838129b86e78e4be1a2
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 1%

---

# 데이터 스트림 구성

데이터 스트림은 Adobe Experience Platform Web 및 Mobile SDK를 구현할 때 서버측 구성을 나타냅니다. 반면에 [명령 구성](configuring-the-sdk.md) sdk에서 는 클라이언트(예: `edgeDomain`), 데이터 세트는 SDK에 대한 다른 모든 구성을 처리합니다. Adobe Experience Platform Edge Network에 요청이 전송되면 `edgeConfigId` 는 데이터 스트림을 참조하는 데 사용됩니다. 이렇게 하면 웹 사이트에서 코드를 변경하지 않고도 서버측 구성을 업데이트할 수 있습니다.

이 문서에서는 Data Collection UI에서 데이터 스트림을 구성하는 절차에 대해 설명합니다.

>[!NOTE]
>
>UI에서 이 기능에 액세스하려면 조직에 이 기능이 제공되어야 합니다. 액세스 권한이 없는 경우 CSM(Customer Success Manager)에게 문의하여를 허용 목록에 추가하다 설정하십시오.

## 액세스 권한 [!UICONTROL 데이터 스트림] 작업 영역

을(를) 선택하여 데이터 수집 UI에서 데이터 세트를 만들고 관리할 수 있습니다 **[!UICONTROL 데이터 스트림]** 을 클릭합니다.

![데이터 수집 UI의 데이터 스트림 탭](../images/datastreams/datastreams-tab.png)

>[!NOTE]
>
>에 액세스할 수 있는 동안 [!UICONTROL 데이터 스트림] Platform의 태그 관리 기능을 사용하는지에 관계없이 데이터 세트를 직접 관리하려면 개발자 권한이 있어야 합니다. 자세한 내용은 [사용자 권한](../../tags/ui/administration/user-permissions.md) 자세한 내용은 태그 설명서의 문서를 참조하십시오.

다음 [!UICONTROL 데이터 스트림] 탭에는 친숙한 이름, ID 및 마지막으로 수정한 날짜를 포함하여 기존 데이터 저장소 목록이 표시됩니다. 데이터 스트림의 이름을 선택합니다 [세부 정보 보기 및 서비스 구성](#view-details).

자세히 아이콘(**...**)를 추가하여 특정 데이터 스트림에 더 많은 옵션을 표시합니다. 선택 **[!UICONTROL 편집]** 를 업데이트하려면 [기본 구성](#configure) 데이터 스트림의 경우 또는 **[!UICONTROL 삭제]** 데이터 스트림을 제거하려면 다음을 수행하십시오.

![기존 데이터 스트림을 편집하거나 삭제할 수 있는 옵션](../images/datastreams/edit-datastream.png)

## 새 데이터 스트림 만들기 {#create}

데이터 스트림을 만들려면 먼저 **[!UICONTROL 새 데이터 스트림]**.

![새 데이터 스트림 선택](../images/datastreams/new-datastream-button.png)

###  구성 {#configure}

구성 단계에서 시작하여 데이터 스트림 만들기 워크플로우가 나타납니다. 여기에서 데이터 스트림에 대한 이름과 선택적 설명을 제공해야 합니다.

Experience Platform에서 사용하도록 이 데이터 스트림을 구성하고 Platform Web SDK를 사용 중인 경우, [이벤트 기반 경험 데이터 모델(XDM) 스키마](../../xdm/classes/experienceevent.md) 수집 중인 데이터를 나타냅니다.

![데이터 스트림에 대한 기본 구성](../images/datastreams/configure.png)

이 섹션의 나머지 부분에서는 선택한 Platform 이벤트 스키마에 데이터를 매핑하는 단계에 중점을 둡니다. Mobile SDK를 사용하고 있거나 Platform에 대한 데이터 스트림을 구성하지 않는 경우 을 선택합니다 **[!UICONTROL 저장]** 의 다음 섹션으로 이동하기 전에 [데이터 스트림에 서비스 추가](#add-services).

### 데이터 수집을 위한 데이터 준비 {#data-prep}

>[!IMPORTANT]
>
>데이터 수집을 위한 데이터 준비는 현재 Mobile SDK 구현에서 지원되지 않습니다.

데이터 준비는 XDM(Experience Data Model)을 통해 데이터를 매핑, 변환 및 확인할 수 있는 Experience Platform 서비스입니다. 플랫폼 지원 데이터 스트림을 구성할 때 데이터 준비 기능을 사용하여 Platform Edge 네트워크에 소스 데이터를 전송할 때 XDM에 매핑할 수 있습니다.

아래 하위 섹션에서는 데이터 수집 UI 내에서 데이터를 매핑하는 기본 단계를 설명합니다. 계산된 필드에 대한 변형 기능을 포함하여 모든 데이터 준비 기능에 대한 포괄적인 지침은 다음 설명서를 참조하십시오.

* [데이터 준비 개요](../../data-prep/home.md)
* [데이터 준비 매핑 함수](../../data-prep/functions.md)
* [데이터 준비를 사용하여 데이터 형식 처리](../../data-prep/data-handling.md)

#### [!UICONTROL 데이터 선택]

선택 **[!UICONTROL 매핑 저장 및 추가]** 완료 후 [기본 구성 단계](#configure), 및 **[!UICONTROL 데이터 선택]** 단계가 나타납니다. 여기에서 Platform으로 전송할 데이터의 구조를 나타내는 샘플 JSON 개체를 제공해야 합니다. 옵션을 선택하여 개체를 파일로 업로드하거나 원시 개체를 제공된 텍스트 상자에 대신 붙여넣을 수 있습니다.

>[!NOTE]
>
>JSON 개체에는 단일 루트 노드가 있어야 합니다 `data` 유효성 검사를 전달하려면 다음을 수행하십시오.

JSON이 유효하면 오른쪽 패널에 미리 보기 스키마가 표시됩니다. 선택 **[!UICONTROL 다음]** 계속하십시오.

![예상 수신 데이터의 JSON 샘플](../images/datastreams/select-data.png)

#### [!UICONTROL 매핑]

다음 **[!UICONTROL 매핑]** 소스 데이터의 필드를 Platform의 target 이벤트 스키마의 필드에 매핑할 수 있는 단계가 나타납니다. 시작하려면 다음을 선택합니다 **[!UICONTROL 새 매핑 추가]** 새 매핑 행을 만들려면

![새 매핑 추가](../images/datastreams/add-new-mapping.png)

소스 아이콘(![소스 아이콘](../images/datastreams/source-icon.png))이고 표시되는 대화 상자에서 제공된 캔버스에 매핑할 소스 필드를 선택합니다. 필드를 선택한 후에는 **[!UICONTROL 선택]** 계속하려면 클릭하십시오.

![소스 스키마에 매핑할 필드 선택](../images/datastreams/source-mapping.png)

다음으로 스키마 아이콘(![스키마 아이콘](../images/datastreams/schema-icon.png))를 클릭하여 target 이벤트 스키마에 대한 유사한 대화 상자를 엽니다. 확인을 하기 전에 데이터를 매핑할 필드를 선택합니다 **[!UICONTROL 선택]**.

![대상 스키마에 매핑할 필드 선택](../images/datastreams/target-mapping.png)

완료된 필드 매핑이 표시된 채 매핑 페이지가 다시 나타납니다. 다음 **[!UICONTROL 매핑 진행률]** 섹션에 성공적으로 매핑된 총 필드 수를 반영하도록 업데이트했습니다.

![진행 상태가 반영된 필드를 매핑했습니다.](../images/datastreams/field-mapped.png)

위의 단계에 따라 나머지 필드를 대상 스키마에 매핑합니다. 사용 가능한 모든 소스 필드를 매핑할 필요는 없지만 이 단계를 완료하려면 필요에 따라 설정된 대상 스키마의 모든 필드를 매핑해야 합니다. 다음 **[!UICONTROL 필수 필드]** 카운터는 현재 구성에 아직 매핑되지 않은 필수 필드 수를 나타냅니다.

필수 필드 수가 0에 도달하고 매핑에 만족하면 을(를) 선택합니다 **[!UICONTROL 저장]** 변경 사항을 확정하려면 다음을 수행하십시오.

![매핑 완료](../images/datastreams/mapping-complete.png)

## 데이터 스트림 세부 정보 보기 {#view-details}

새 데이터 스트림을 구성하거나 기존 데이터 스트림을 선택하여 보면 해당 데이터 스트림에 대한 세부 정보 페이지가 나타납니다. 여기에서 해당 ID를 포함하여 데이터 스트림에 대한 추가 정보를 찾을 수 있습니다.

![생성된 데이터 스트림에 대한 세부 정보 페이지](../images/datastreams/view-details.png)

데이터 스트림을 만들 때 세 개의 관련 환경이 동일한 설정으로 자동으로 생성됩니다. 이 세 가지 환경은 다음과 같습니다 `dev`, `stage`, 및 `prod`에 해당하는 [태그의 기본 환경](../../tags/ui/publishing/environments.md). 태그 라이브러리를 `dev` 환경에서 라이브러리는 자동으로 `dev` 데이터 스트림의 환경입니다. 개별 환경에서 필요에 맞게 설정을 자유롭게 편집할 수 있습니다.

SDK 구현에서 `edgeConfigId` 는 해당 데이터 스트림 내의 특정 환경과 데이터 스트림을 지정하는 복합 ID입니다. 예를 들어 `stage` ID가 있는 데이터 스트림의 환경 `1c86778b-cdba-4684-9903-750e52912ad1`를 사용하려면 `edgeConfigId` `1c86778b-cdba-4684-9903-750e52912ad1:stage`.

>[!IMPORTANT]
>
>복합 ID에 환경이 없으면 프로덕션 환경(`prod`사용)

데이터 스트림 세부 사항 화면에서 다음을 수행할 수 있습니다 [서비스 추가](#add-services) 액세스 권한이 있는 Adobe Experience Cloud 제품의 기능을 활성화하기 위한 것입니다.

## 데이터 스트림에 서비스 추가 {#add-services}

데이터 스트림의 세부 정보 페이지에서 **[!UICONTROL 서비스 추가]** 해당 데이터 스트림에 사용 가능한 서비스 추가를 시작하려면 다음을 수행하십시오.

![계속하려면 [서비스 추가]를 선택하십시오](../images/datastreams/add-service.png)

다음 화면에서 드롭다운 메뉴를 사용하여 이 데이터 스트림에 대해 구성할 서비스를 선택합니다. 액세스 권한이 있는 서비스만 이 목록에 표시됩니다.

![목록에서 서비스를 선택합니다](../images/datastreams/service-selection.png)

원하는 서비스를 선택하고 나타나는 구성 옵션을 입력한 다음 선택합니다 **[!UICONTROL 저장]** 를 눌러 데이터 스트림에 서비스를 추가합니다. 추가된 모든 서비스가 데이터 스트림에 대한 세부 정보 보기에 나타납니다.

![데이터 스트림에 추가된 서비스](../images/datastreams/services-added.png)

아래 하위 섹션에서는 각 서비스의 구성 옵션에 대해 설명합니다.

>[!NOTE]
>
>각 서비스 구성에는 **[!UICONTROL 활성화됨]** 서비스를 선택하면 자동으로 활성화되는 전환합니다. 이 데이터 스트림에 대해 선택한 서비스를 비활성화하려면 **[!UICONTROL 활성화됨]** 다시 전환합니다.

### Adobe Analytics 설정

이 서비스는 Adobe Analytics으로 데이터를 전송할지 여부와 방법을 제어합니다. 자세한 내용은 [analytics에 데이터 보내기](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics 설정 블록](../images/datastreams/analytics-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 보고서 세트 ID] | **(필수)** 데이터를 전송할 Analytics 보고서 세트의 ID입니다. 이 ID는 아래의 Adobe Analytics UI에서 찾을 수 있습니다 [!UICONTROL 관리] > [!UICONTROL 보고서 세트]. 여러 보고서 세트를 지정하면 데이터가 각 보고서 세트에 복사됩니다. |

### Adobe Audience Manager 설정

이 서비스는 Adobe Audience Manager으로 데이터를 전송할지 여부와 방법을 제어합니다. Audience Manager으로 데이터를 전송하는 데 필요한 모든 것은 이 섹션을 활성화하는 것입니다. 다른 설정은 선택 사항이지만 권장됩니다.

![Adobe 대상 관리 설정 블록](../images/datastreams/audience-manager-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 쿠키 대상 활성화] | SDK가 를 통해 세그먼트 정보를 공유할 수 있도록 허용합니다 [쿠키 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 변환 전: [!DNL Audience Manager]. |
| [!UICONTROL URL 대상 사용] | SDK가 를 통해 세그먼트 정보를 공유할 수 있도록 허용합니다 [URL 대상](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) 변환 전: [!DNL Audience Manager]. |

### Adobe Experience Platform 설정

>[!IMPORTANT]
>
>Platform용 데이터 스트림을 활성화할 때 데이터 수집 UI의 위쪽 리본에 표시된 대로 현재 사용 중인 Platform 샌드박스를 주목하십시오.
>
>![선택한 샌드박스](../images/datastreams/platform-sandbox.png)
>
>샌드박스는 조직의 다른 샌드박스와 데이터 및 구현을 분리할 수 있는 Adobe Experience Platform의 가상 파티션입니다. 데이터 스트림을 만들면 해당 샌드박스를 변경할 수 없습니다. Experience Platform에서 샌드박스의 역할에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md).

이 서비스는 Adobe Experience Platform으로 데이터를 전송할지 여부와 방법을 제어합니다.

![Adobe Experience Platform 설정 블록](../images/datastreams/platform-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 이벤트 데이터 세트] | **(필수)** 고객 이벤트 데이터를 스트리밍할 플랫폼 데이터 세트를 선택합니다. 이 스키마는 [XDM ExperienceEvent 클래스](../../xdm/classes/experienceevent.md). |
| [!UICONTROL 프로필 데이터 세트] | 고객 특성 데이터를 전송할 Platform 데이터 세트를 선택합니다. 이 스키마는 [XDM 개별 프로필 클래스](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Platform Web SDK 구현에 Offer decisioning을 활성화하려면 이 확인란을 선택하십시오. 다음 안내서를 참조하십시오. [platform Web SDK에서 Offer decisioning 사용](../personalization/offer-decisioning/offer-decisioning-overview.md) 를 참조하십시오. offer decisioning 기능에 대한 자세한 내용은 [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=ko-KR). |
| [!UICONTROL 에지 세그멘테이션] | 이 확인란을 선택하여 [에지 세분화](../../segmentation/ui/edge-segmentation.md) 이 데이터 스트림에 대해 설명합니다. SDK가 에지 세그먼테이션이 활성화된 데이터 스트림을 통해 데이터를 전송하면 해당 프로필에 대해 업데이트된 세그먼트 멤버십이 응답으로 다시 전송됩니다.<br><br>이 옵션은 [!UICONTROL 개인화 대상] 대상 [다음 페이지 개인화 사용 사례](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL 개인화 대상] | 와 함께 사용하는 경우 [!UICONTROL 에지 세그멘테이션] 확인란을 선택하면 이 옵션을 사용하여 데이터 스트림이 Adobe Target과 같은 개인화 엔진에 연결할 수 있습니다. 의 특정 단계에 대해서는 대상 설명서 를 참조하십시오 [개인화 대상 구성](../../destinations/ui/configure-personalization-destinations.md). |

### Adobe Target 설정

이 서비스는 Adobe Target으로 데이터를 전송할지 여부와 방법을 제어합니다.

![Adobe Target 설정 블록](../images/datastreams/target-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 속성 토큰] | [!DNL Target] 을 사용하면 고객이 속성을 사용하여 권한을 제어할 수 있습니다. 속성에 대한 자세한 내용은 [enterprise 권한 구성](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 에서 [!DNL Target] 설명서.<br><br>속성 토큰은 아래의 Adobe Target UI에 있습니다 [!UICONTROL 설정] > [!UICONTROL 속성]. |
| [!UICONTROL Target 환경 ID] | [Adobe Target의 환경](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 은 모든 개발 단계를 통해 구현을 관리하는 데 도움이 됩니다. 이 설정은 이 데이터 스트림에 사용할 환경을 지정합니다.<br><br>가장 좋은 방법은 각 사용자 `dev`, `stage`, 및 `prod` 데이터 스트림 환경을 통해 작업을 단순화할 수 있습니다. 그러나 이미 Adobe Target 환경이 정의된 경우 해당 환경을 사용할 수 있습니다. |
| [!UICONTROL Target 타사 ID 네임스페이스] | 에 대한 ID 네임스페이스 `mbox3rdPartyId` 이 데이터 스트림에 를 사용하려는 경우 다음 안내서를 참조하십시오. [구현 `mbox3rdPartyId` 웹 SDK 사용](../personalization/adobe-target/using-mbox-3rdpartyid.md) 추가 정보. |

### [!UICONTROL 이벤트 전달] 설정

이 서비스는 로 데이터를 전송할지 여부와 방법을 제어합니다 [이벤트 전달](../../tags/ui/event-forwarding/overview.md).

![구성 UI의 이벤트 전달 섹션](../images/datastreams/event-forwarding-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL Launch 속성] | **(필수)** 데이터를 보낼 이벤트 전달 속성입니다. |
| [!UICONTROL Launch 환경] | **(필수)** 선택한 속성에 데이터를 보낼 환경입니다. |

>[!NOTE]
>
>선택할 수 있습니다 **[!UICONTROL 수동으로 ID 입력]** 드롭다운 메뉴를 사용하지 않고 속성 및 환경 이름을 입력합니다.

### [!UICONTROL 타사 ID 동기화] 설정

타사 ID 섹션은 항상 켜져 있는 유일한 섹션입니다. 사용 가능한 설정은 두 가지입니다. &quot;[!UICONTROL 타사 ID 동기화가 활성화됨]&quot; 및 &quot;[!UICONTROL 타사 ID 동기화 컨테이너 ID]&quot;.

![구성 UI의 타사 ID 동기화 섹션](../images/datastreams/third-party-id-sync-config.png)

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL 타사 ID 동기화 컨테이너 ID] | ID 동기화를 컨테이너로 그룹화하여 다른 시간에 다른 ID 동기화를 실행할 수 있습니다. 이 데이터 스트림에 대해 실행 중인 ID 동기화를 제어합니다. |

## 다음 단계

이 안내서에서는 데이터 수집 UI에서 데이터 스트림을 구성하는 방법을 다룹니다. 데이터 스트림을 설정한 후 Web SDK를 설치하고 구성하는 방법에 대한 자세한 내용은 [데이터 수집 E2E 안내서](../../collection/e2e.md#install).
