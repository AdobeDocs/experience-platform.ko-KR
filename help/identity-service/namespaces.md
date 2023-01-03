---
keywords: Experience Platform;홈;인기 항목;네임스페이스;네임스페이스;네임스페이스;네임스페이스;ID 네임스페이스;ID 네임스페이스;ID;ID;ID 서비스;ID 서비스
solution: Experience Platform
title: ID 네임스페이스 개요
topic-legacy: overview
description: ID 네임스페이스는 ID 서비스의 구성 요소이며 ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어 "name@email.com"이라는 값을 이메일 주소로 또는 "443522"이라는 값을 숫자 CRM ID로 구분합니다.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 3%

---

# ID 네임스페이스 개요

ID 네임스페이스는 [[!DNL Identity Service]](./home.md) ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어 &quot;name&quot;이라는 값을 구분합니다<span>@email.com&quot; 을 이메일 주소로 보내거나 &quot;443522&quot;을 숫자 CRM ID로 사용합니다.

## 시작하기

ID 네임스페이스로 작업하려면 관련된 다양한 Adobe Experience Platform 서비스를 이해해야 합니다. 네임스페이스로 작업을 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
- [[!DNL Identity Service]](./home.md): 여러 장치와 시스템에서 ID를 브리징하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
- [[!DNL Privacy Service]](../privacy-service/home.md): ID 네임스페이스는 GDPR(일반 데이터 보호 규정)과 같은 법적 개인 정보 보호 규정에 대한 규정 준수 요청에 사용됩니다. 각 개인 정보 보호 요청은 영향을 받아야 하는 소비자의 데이터를 식별하기 위해 네임스페이스에 대해 수행됩니다.

## ID 네임스페이스 이해

정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 프로필 조각에서 레코드 데이터를 일치시킬 때 [!DNL Real-time Customer Profile] 프로필 데이터를 병합하고 ID 값과 네임스페이스가 모두 일치해야 합니다.

예를 들어, 두 프로필 조각은 서로 다른 기본 ID를 포함할 수 있지만 &quot;이메일&quot; 네임스페이스에 대해 동일한 값을 공유합니다 [!DNL Platform] 이러한 조각이 실제로 동일한 개인임을 확인하고 해당 데이터를 개별 id 그래프에 통합합니다.

![](images/identity-service-stitching.png)

### ID 유형 {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="ID 유형 지정"
>abstract="ID 유형은 데이터가 ID 그래프에 저장되는지 여부를 제어합니다. 사람이 아닌 식별자는 저장되지 않으며 다른 모든 ID 유형은 저장됩니다."
>text="Learn more in documentation"

데이터는 여러 가지 ID 유형으로 식별할 수 있습니다. ID 유형은 ID 네임스페이스가 생성될 때 지정되며 데이터가 ID 그래프로 유지되는지 여부와 데이터를 처리하는 방법에 대한 특수 지침을 제어합니다. ID 유형을 제외한 모든 ID 유형 **비사용자 식별자** 네임스페이스 및 해당 ID 값을 id 그래프 클러스터에 결합하는 동일한 동작을 따릅니다. 를 사용할 때 데이터가 함께 결합되지 않습니다 **비사용자 식별자**.

내에서 다음 ID 유형을 사용할 수 있습니다 [!DNL Platform]:

| ID 유형 | 설명 |
| --- | --- |
| 쿠키 ID | 쿠키 ID는 웹 브라우저를 식별합니다. 이러한 ID는 확장에 매우 중요하며 ID 그래프의 대부분을 구성합니다. 그러나, 자연에 의해 그들은 빠르게 부패하고 시간이 지남에 따라 그들의 가치를 잃는다. |
| 교차 장치 ID | 교차 장치 ID는 개인을 식별하고 일반적으로 다른 ID를 함께 연결합니다. 예를 들면 로그인 ID, CRM ID 및 충성도 ID가 있습니다. 이것은 [!DNL Identity Service] 섬세하게 가치를 다루다. |
| 장치 ID | 장치 ID는 IDFA(iPhone 및 iPad), GAID(Android) 및 RIDA(Roku)와 같은 하드웨어 장치를 식별하며, 가정에서 여러 사람이 공유할 수 있습니다. |
| 이메일 주소 | 이메일 주소는 종종 한 사람과 연결되어 있으므로 다양한 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII(개인 식별 정보)가 포함됩니다. 이것은 [!DNL Identity Service] 섬세하게 가치를 다루다. |
| 비사용자 식별자 | 개인이 아닌 ID는 네임스페이스가 필요하지만 개인 클러스터에는 연결되어 있지 않은 식별자를 저장하는 데 사용됩니다. 예를 들어 제품 SKU, 제품, 조직 또는 스토어와 관련된 데이터. |
| 전화번호 | 전화 번호는 한 사람과 종종 연결되어 있으므로 다양한 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII가 포함됩니다. 이것은 [!DNL Identity Service] 섬세하게 가치를 다루다. |

### 표준 네임스페이스 {#standard}

Experience Platform은 모든 조직에서 사용할 수 있는 몇 가지 ID 네임스페이스를 제공합니다. 이러한 네임스페이스는 표준 네임스페이스라고 하며 [!DNL Identity Service] API 또는 플랫폼 UI 사용.

Platform 내의 모든 조직에서 사용할 수 있도록 다음과 같은 표준 네임스페이스가 제공됩니다.

| 디스플레이 이름 | 설명 |
| ------------ | ----------- |
| AdCloud | Adobe AdCloud를 나타내는 네임스페이스입니다. |
| Adobe Analytics (기존 ID) | Adobe Analytics을 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Adobe Analytics 네임스페이스](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) 추가 정보. |
| Apple IDFA(광고주용 ID) | 광고주용 Apple ID를 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [관심 기반 광고](https://support.apple.com/en-us/HT202074) 추가 정보. |
| Apple 푸시 알림 서비스 | Apple 푸시 알림 서비스를 사용하여 수집된 ID를 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Apple 푸시 알림 서비스](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 추가 정보. |
| CORE | Adobe Audience Manager을 나타내는 네임스페이스입니다. 이 네임스페이스를 이전 이름으로 참조할 수도 있습니다. &quot;Adobe AudienceManager&quot;. 다음 문서를 참조하십시오. [Audience Manager ID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) 추가 정보. |
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 다음 문서를 참조하십시오. [ECID](./ecid.md) 추가 정보. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람에게 연결되므로 다른 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |
| 이메일(SHA256, 소문자로) | 미리 해시된 이메일 주소를 위한 네임스페이스. 이 네임스페이스에 제공된 값은 SHA256으로 해싱하기 전에 소문자로 변환됩니다. 전자 메일 주소가 표준화되기 전에 선행 및 후행 공백을 트림해야 합니다. 이 설정은 소급하여 변경할 수 없습니다. 다음 문서를 참조하십시오. [SHA256 해시 지원](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 추가 정보. |
| Firebase Cloud Messaging | 푸시 알림에 Google Firebase Cloud Messaging을 사용하여 수집한 ID를 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) 추가 정보. |
| Google 광고 ID(GAID) | Google 광고 ID를 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Google 광고 ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 추가 정보. |
| Google 클릭 ID | Google 클릭 ID를 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Google 광고에서 클릭 추적](https://developers.google.com/adwords/api/docs/guides/click-tracking) 추가 정보. |
| 전화 | 전화 번호를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람에게 연결되므로 다른 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |
| 전화(E.164) | E.164 형식으로 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. E.164 형식에는 더하기 기호(`+`), 국제 전화 코드, 지역 번호 및 전화 번호. 예: `(+)(country code)(area code)(phone number)`. |
| 전화(SHA256) | SHA256을 사용하여 해시해야 하는 전화 번호를 나타내는 네임스페이스입니다. 기호, 문자 및 0을 제거해야 합니다. 국가 호출 코드도 접두사로 추가해야 합니다. |
| 전화(SHA256_E.164) | SHA256과 E.164 형식을 모두 사용하여 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. |
| TNTID | Adobe Target을 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) 추가 정보. |
| Windows AID | Windows 광고 ID를 나타내는 네임스페이스입니다. 다음 문서를 참조하십시오. [Windows 광고 ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 추가 정보. |

### ID 네임스페이스 보기

UI에서 ID 네임스페이스를 보려면 **[!UICONTROL ID]** 왼쪽 탐색에서 를 선택하고 을 선택합니다. **[!UICONTROL 찾아보기]**.

![검색](./images/browse.png)

ID 네임스페이스 목록은 페이지의 기본 인터페이스에 나타나며 해당 이름, ID 기호, 최근 업데이트 날짜 및 ID가 표준 네임스페이스인지 사용자 지정 네임스페이스인지에 대한 정보를 표시합니다. 오른쪽 레일에는 다음 정보가 있습니다. [!UICONTROL ID 그래프 강도].

![id](./images/identities.png)

또한 플랫폼은 통합을 위해 네임스페이스를 제공합니다. 이러한 네임스페이스는 다른 시스템과 연결하는 데 사용되므로 기본적으로 숨겨져 있으며 ID를 연결하는 데 사용되지 않습니다. 통합 네임스페이스를 보려면 **[!UICONTROL 통합 ID 보기]**.

![view-integration-identities](./images/view-integration-identities.png)

특정 네임스페이스에 대한 정보를 보려면 목록에서 ID 네임스페이스를 선택합니다. ID 네임스페이스를 선택하면 오른쪽 레일의 디스플레이가 업데이트되어 수집된 ID 수 및 실패 또는 건너뛴 레코드 수를 포함하여 선택한 ID 네임스페이스에 대한 메타데이터를 표시합니다.

![select-namespace](./images/select-namespace.png)

## 사용자 지정 네임스페이스 관리 {#manage-namespaces}

조직 데이터 및 사용 사례에 따라 사용자 지정 네임스페이스가 필요할 수 있습니다. 사용자 지정 네임스페이스는 [[!DNL Identity Service]](./api/create-custom-namespace.md) API 또는 UI 사용.

UI를 사용하여 사용자 지정 네임스페이스를 만들려면 **[!UICONTROL ID]** 작업 영역, 선택 **[!UICONTROL 찾아보기]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL ID 네임스페이스 만들기]**.

![select-create](./images/select-create.png)

다음 **[!UICONTROL ID 네임스페이스 만들기]** 대화 상자가 나타납니다. 고유 정보 제공 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL ID 기호]** 그런 다음 만들려는 id 유형을 선택합니다. 선택적 설명을 추가하여 네임스페이스에 대한 추가 정보를 추가할 수도 있습니다. ID 유형을 제외한 모든 유형 **비사용자 식별자** 는 결합의 동일한 동작을 따릅니다. 선택하는 경우 **비사용자 식별자** 네임스페이스를 만들 때 id 유형으로 결합이 발생하지 않습니다. 각 ID 유형에 대한 자세한 내용은 [id 유형](#identity-types).

완료되면 을 선택합니다 **[!UICONTROL 만들기]**.

>[!IMPORTANT]
>
>사용자가 정의하는 네임스페이스는 조직의 개인 정보이며 성공적으로 만들려면 고유한 ID 기호가 필요합니다.

![create-identity-namespace](./images/create-identity-namespace.png)

표준 네임스페이스와 유사하게 **[!UICONTROL 찾아보기]** 탭을 클릭하여 세부 사항을 확인합니다. 그러나 사용자 지정 네임스페이스를 사용하면 세부 정보 영역에서 표시 이름과 설명을 편집할 수도 있습니다.

>[!NOTE]
>
>네임스페이스를 만들면 해당 네임스페이스를 삭제할 수 없으며 ID 기호와 유형을 변경할 수 없습니다.

## ID 데이터의 네임스페이스

ID에 대한 네임스페이스를 제공하는 것은 ID 데이터를 제공하는 데 사용하는 방법에 따라 다릅니다. 데이터 ID 데이터 제공에 대한 자세한 내용은 [id 데이터 공급](./home.md#supplying-identity-data-to-identity-service) 에서 [!DNL Identity Service] 개요.

## 다음 단계

ID 네임스페이스의 주요 개념을 이해했으므로 다음을 사용하여 ID 그래프를 사용하는 방법을 배울 수 있습니다 [id 그래프 뷰어](./ui/identity-graph-viewer.md).
