---
keywords: Experience Platform;홈;인기 항목;Adobe Campaign Managed Cloud Services;캠페인;캠페인 관리 서비스
title: Adobe Campaign Managed Cloud Services
description: 사용자 인터페이스를 사용하여 Campaign 관리 Cloud Services을 Platform에 연결하는 방법을 알아봅니다
source-git-commit: 99f65889aecf8c045dbb72053ebaca9429c3ebe1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Adobe Campaign Managed Cloud Services은 크로스채널 고객 경험을 디자인할 수 있는 Managed Services 플랫폼을 제공하며 시각적 캠페인 오케스트레이션, 실시간 상호 작용 관리 및 크로스 채널 실행 환경을 제공합니다. 다음 방문 [Adobe Campaign v8 설명서](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) 추가 정보.

Adobe Campaign Managed Cloud Services 소스를 사용하면 Adobe Campaign v8 게재 로그 및 추적 로그 데이터를 Adobe Experience Platform으로 가져올 수 있습니다.

## 전제 조건

소스 연결을 만들어 Campaign v8을 Experience Platform에 가져오려면 먼저 다음 사전 요구 사항을 완료해야 합니다.

* [Adobe Campaign 클라이언트 콘솔을 사용하여 이벤트 로그 가져오기를 설정합니다](#view-delivery-and-tracking-log-data)
* [XDM ExperienceEvent 스키마 만들기](#create-a-schema)
* [데이터 집합 만들기](#create-a-dataset)

### 게재 및 추적 로그 데이터 보기 {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Campaign에서 로그 데이터를 보려면 Adobe Campaign v8 클라이언트 콘솔에 액세스할 수 있어야 합니다. 다음 방문 [Campaign v8 설명서](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) 클라이언트 콘솔 다운로드 및 설치 방법에 대한 자세한 내용을 참조하십시오.

클라이언트 콘솔을 통해 Campaign v8 인스턴스에 로그인합니다. 아래에 [!DNL Explorer] 탭, 선택 [!DNL Administration] 그런 다음 [!DNL Configuration]. 다음 을 선택합니다. [!DNL Data schemas] 그런 다음 `broadLog` 이름 또는 레이블에 대해 필터링합니다. 표시되는 목록에서 이름이 인 수신자 게재 로그 소스 스키마를 선택합니다 `broadLogRcp`.

![탐색기 탭이 선택된 Adobe Campaign v8 클라이언트 콘솔에서는 관리, 구성 및 데이터 스키마 노드가 확장되고 필터링이 &quot;광범위한&quot;으로 설정됩니다.](./images/campaign/explorer.png)

다음으로, **데이터** 탭.

![데이터 탭이 선택된 Adobe Campaign v8 클라이언트 콘솔입니다.](./images/campaign/data.png)

데이터 패널에서 마우스 오른쪽 단추 클릭/키를 눌러 상황별 메뉴를 엽니다. 여기에서 을 선택합니다. **목록 구성...**

![상황별 메뉴가 열리고 목록 구성 옵션이 선택된 Adobe Campaign v8 클라이언트 콘솔입니다.](./images/campaign/configure.png)

목록 구성 창이 나타나고, 기존 목록에 원하는 필드를 추가하여 데이터 패널에서 데이터를 볼 수 있는 인터페이스를 제공합니다.

![보기 위해 추가할 수 있는 수신자 게재 로그에 대한 구성 목록입니다.](./images/campaign/list-configuration.png)

이제 이전 단계에서 추가된 구성 필드를 포함하여 수신자 게재 로그를 볼 수 있습니다.

>[!TIP]
>
>동일한 단계를 반복할 수 있지만 을(를) 필터링합니다 `tracking` 추적 로그 데이터를 보려면

![마지막으로 수정된 이름, 게재 채널, 내부 게재 이름 및 레이블에 대한 정보가 포함된 수신자 게재 로그가 표시됩니다.](./images/campaign/recipient-delivery-logs.png)

### 스키마 만들기 {#create-a-schema}

다음으로, 게재 로그와 추적 로그를 위한 XDM ExperienceEvent 스키마를 만듭니다. 캠페인 게재 로그 필드 그룹을 게재 로그 스키마와 캠페인 추적 로그 필드 그룹에 적용해야 합니다. 또한 `externalID` 필드를 스키마의 기본 ID로 지정합니다.

>[!NOTE]
>
>Campaign 데이터를 로 수집하려면 XDM ExperienceEvent 스키마가 프로필을 사용하도록 설정해야 합니다 [!DNL Real-time Customer Profile].

스키마를 만드는 방법에 대한 자세한 지침은 [UI에서 XDM 스키마 만들기](../../../xdm/tutorials/create-schema-ui.md).

### 데이터 집합 만들기 {#create-a-dataset}

마지막으로 스키마에 대한 데이터 세트를 만들어야 합니다. 데이터 세트를 만드는 방법에 대한 자세한 지침은 [UI에서 데이터 세트 만들기](../../../catalog/datasets/user-guide.md).

## Platform UI를 사용하여 Adobe Campaign Managed Cloud Services 소스 연결 만들기

이제 Campaign 클라이언트 콘솔에서 데이터 로그에 액세스하고, 스키마 및 데이터 세트를 만들었으므로 이제 소스 연결을 만들어 Campaign Managed Services 데이터를 플랫폼으로 가져올 수 있습니다.

Campaign v8 게재 로그 및 추적 로그 데이터를 Experience Platform으로 가져오는 방법에 대한 자세한 지침은 위의 안내서를 참조하십시오 [UI에서 Campaign Managed Services 소스 연결 만들기](../../tutorials/ui/create/adobe-applications/campaign.md).