---
title: ID 네임스페이스 개요
description: ID 네임스페이스는 ID 서비스의 구성 요소이며 ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어 이메일 주소로 "name@email.com" 값을 구별하거나 숫자 CRM ID로 "443522"값을 구별합니다.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 58fefcc0a590341922f0769a416e27cd1f13a617
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 8%

---

# ID 네임스페이스 개요

ID 네임스페이스는 의 구성 요소입니다. [[!DNL Identity Service]](./home.md) id가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어, &quot;name&quot;의 값을 구별합니다<span>@email.com&quot; 을 이메일 주소로 사용하거나 &quot;443522&quot;를 숫자 CRM ID로 사용합니다.

## 시작하기

신원 네임스페이스를 사용하여 작업하려면 다양한 관련 Adobe Experience Platform 서비스를 이해해야 합니다. 네임스페이스 작업을 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 고객 프로필을 실시간으로 제공합니다.
- [[!DNL Identity Service]](./home.md): 디바이스와 시스템 간에 ID를 연결하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
- [[!DNL Privacy Service]](../privacy-service/home.md): ID 네임스페이스는 GDPR(일반 데이터 보호 규정)과 같은 법적 개인 정보 보호 규정에 대한 준수 요청에 사용됩니다. 각 개인 정보 보호 요청은 영향을 받아야 하는 소비자의 데이터를 식별하기 위해 네임스페이스를 기준으로 수행됩니다.

## ID 네임스페이스 이해

정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 다음과 같이 프로필 조각 간에 레코드 데이터를 일치시킬 때 [!DNL Real-Time Customer Profile] 프로필 데이터를 병합합니다. id 값과 네임스페이스가 모두 일치해야 합니다.

예를 들어 두 프로필 조각은 서로 다른 기본 ID를 포함할 수 있지만 &quot;이메일&quot; 네임스페이스에 대해 동일한 값을 공유합니다 [!DNL Platform] 는 이러한 조각이 실제로 동일한 개인이며 해당 개인의 id 그래프에 데이터를 함께 가져온다는 것을 알 수 있습니다.

![](images/identity-service-stitching.png)

### ID 유형 {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="ID 유형 지정"
>abstract="ID 유형은 데이터가 ID 그래프에 저장되는지 여부를 제어합니다. 사람이 아닌 식별자는 저장되지 않으며, 다른 모든 ID 유형은 저장됩니다."
>text="Learn more in documentation"

데이터는 여러 가지 다른 ID 유형으로 식별할 수 있습니다. ID 유형은 ID 네임스페이스가 생성될 때 지정되며 데이터가 ID 그래프로 유지되는지 여부와 데이터 처리 방법에 대한 특수 지침을 제어합니다. 다음을 제외한 모든 ID 유형 **비사용자 식별자** 네임스페이스와 해당 ID 값을 id 그래프 클러스터에 결합하는 것과 동일한 동작을 따르십시오. 를 사용할 때 데이터가 함께 결합되지 않음 **비사용자 식별자**.

다음 ID 유형은 내에서 사용할 수 있습니다. [!DNL Platform]:

| ID 유형 | 설명 |
| --- | --- |
| 쿠키 ID | 쿠키 ID는 웹 브라우저를 식별합니다. 이러한 ID는 확장에 중요하며 ID 그래프의 대부분을 구성합니다. 그러나 자연적으로 그들은 빠르게 부패하고 시간이 지남에 따라 가치를 잃습니다. |
| 교차 장치 ID | 크로스 디바이스 ID는 개인을 식별하며 일반적으로 다른 ID를 함께 연결합니다. 예를 들면 로그인 ID, CRM ID 및 충성도 ID가 있습니다. 다음에 대한 표시입니다. [!DNL Identity Service] 를 입력하여 값을 민감하게 처리합니다. |
| 장치 ID | 장치 ID는 IDFA(iPhone 및 iPad), GAID(Android) 및 RIDA(Roku)와 같은 하드웨어 장치를 식별하며 가정에서 여러 사람이 공유할 수 있습니다. |
| 이메일 주소 | 이메일 주소는 종종 단일 사용자와 연결되므로, 다양한 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII(개인 식별 정보)가 포함됩니다. 다음에 대한 표시입니다. [!DNL Identity Service] 를 입력하여 값을 민감하게 처리합니다. |
| 비인물 식별자 | 비사용자 ID는 네임스페이스가 필요하지만 개인 클러스터에 연결되지 않은 식별자를 저장하는 데 사용됩니다. 예: 제품 SKU, 제품, 조직 또는 스토어와 관련된 데이터. |
| 파트너 ID | 파트너 ID는 데이터 파트너가 사람을 나타내는 데 사용하는 식별자입니다. 파트너 ID는 종종 개인의 진짜 신분을 밝히지 않기 위해 가명으로 사용되며 확률적일 수 있습니다. Real-time Customer Data Platform에서 파트너 ID는 주로 확장된 대상 활성화 및 데이터 보강에 사용되며 결정론적 ID 그래프 링크 구축에는 사용되지 않습니다. |
| 전화번호 | 전화번호는 종종 한 사람과 연관되어 있으므로 다른 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII가 포함됩니다. 다음에 대한 표시입니다 [!DNL Identity Service] 를 입력하여 값을 민감하게 처리합니다. |

### 표준 네임스페이스 {#standard}

Experience Platform은 모든 조직에서 사용할 수 있는 여러 ID 네임스페이스를 제공합니다. 이러한 네임스페이스를 표준 네임스페이스라고 하며 [!DNL Identity Service] API 또는 Platform UI를 통해

다음 표준 네임스페이스는 Platform 내의 모든 조직에서 사용할 수 있도록 제공됩니다.

| 표시 이름 | 설명 |
| ------------ | ----------- |
| AdCloud | Adobe AdCloud를 나타내는 네임스페이스입니다. |
| Adobe Analytics (이전 ID) | Adobe Analytics을 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Adobe Analytics 네임스페이스](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) 추가 정보. |
| Apple IDFA (광고주용 ID) | 광고주용 Apple ID를 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [관심 기반 광고](https://support.apple.com/en-us/HT202074) 추가 정보. |
| Apple 푸시 알림 서비스 | Apple 푸시 알림 서비스를 사용하여 수집된 ID를 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Apple 푸시 알림 서비스](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 추가 정보. |
| CORE | Adobe Audience Manager을 나타내는 네임스페이스입니다. 이 네임스페이스는 기존 이름 &quot;Adobe AudienceManager&quot;로도 참조할 수 있습니다. 에 대한 다음 문서를 참조하십시오. [AUDIENCE MANAGER ID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) 추가 정보. |
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 에 대한 다음 문서를 참조하십시오. [ECID](./ecid.md) 추가 정보. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 단일 사용자와 연결되므로 여러 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |
| 이메일(SHA256, 소문자) | 사전 해시된 이메일 주소를 위한 네임스페이스입니다. 이 네임스페이스에 제공된 값은 SHA256으로 해싱하기 전에 소문자로 변환됩니다. 전자 메일 주소가 정규화되기 전에 선행 및 후행 공백을 잘라내야 합니다. 이 설정은 소급하여 변경할 수 없습니다. 에 대한 다음 문서를 참조하십시오. [SHA256 해시 지원](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 추가 정보. |
| Firebase 클라우드 메시징 | 푸시 알림용 Google Firebase Cloud Messaging을 사용하여 수집된 ID를 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Google Firebase 클라우드 메시징](https://firebase.google.com/docs/cloud-messaging) 추가 정보. |
| Google 광고 ID (GAID) | Google 광고 ID를 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Google 광고 ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 추가 정보. |
| Google 클릭 ID | Google Click ID를 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Google 광고의 클릭 추적](https://developers.google.com/adwords/api/docs/guides/click-tracking) 추가 정보. |
| 전화 | 전화 번호를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 단일 사용자와 연결되므로 여러 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |
| 전화(E.164) | E.164 형식으로 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. E.164 형식에는 더하기 기호(`+`), 국제 국가 호출 코드, 현지 지역 코드 및 전화번호. 예: `(+)(country code)(area code)(phone number)`. |
| 전화(SHA256) | SHA256을 사용하여 해시해야 하는 전화 번호를 나타내는 네임스페이스입니다. 기호, 문자 및 앞에 오는 0을 제거해야 합니다. 국가 호출 코드도 접두사로 추가해야 합니다. |
| 전화(SHA256_E.164) | SHA256과 E.164 형식을 모두 사용하여 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. |
| TNTID | Adobe Target을 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) 자세한 내용을 확인하십시오. |
| Windows AID | Windows 광고 ID를 나타내는 네임스페이스입니다. 에 대한 다음 문서를 참조하십시오. [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 추가 정보. |

### ID 네임스페이스 보기 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="통합 ID 보기"
>abstract="통합 ID는 다른 시스템에 연결하는 데 사용되는 네임스페이스이며, ID 확인 또는 연결 ID에는 사용되지 않습니다. <br> 이러한 ID는 기본적으로 숨겨져 있습니다. 토글을 사용하여 통합 네임스페이스를 봅니다."

UI에서 ID 네임스페이스를 보려면 **[!UICONTROL ID]** 왼쪽 탐색에서 을(를) 선택한 다음 **[!UICONTROL 찾아보기]**.

![검색](./images/browse.png)

페이지의 기본 인터페이스에 ID 네임스페이스 목록이 표시되어 이름, ID 기호, 마지막 업데이트 날짜 및 표준 네임스페이스인지 사용자 지정 네임스페이스인지에 대한 정보를 표시합니다. 오른쪽 레일에는 다음 정보가 포함됩니다. [!UICONTROL ID 그래프 강도].

![id](./images/identities.png)

또한 Platform은 통합을 위해 네임스페이스를 제공합니다. 이러한 네임스페이스는 다른 시스템과 연결하는 데 사용되고 ID를 결합하는 데 사용되지 않으므로 기본적으로 숨겨집니다. 통합 네임스페이스를 보려면 다음을 선택합니다. **[!UICONTROL 통합 ID 보기]**.

![view-integration-id](./images/view-integration-identities.png)

특정 네임스페이스에 대한 정보를 보려면 목록에서 ID 네임스페이스를 선택하십시오. ID 네임스페이스를 선택하면 오른쪽 레일의 표시가 업데이트되어 수집된 ID 수와 실패 및 건너뛴 레코드 수 등 선택한 ID 네임스페이스와 관련된 메타데이터가 표시됩니다.

![select-네임스페이스](./images/select-namespace.png)

## 사용자 정의 네임스페이스 관리 {#manage-namespaces}

조직 데이터 및 사용 사례에 따라 사용자 정의 네임스페이스가 필요할 수 있습니다. 다음을 사용하여 사용자 정의 네임스페이스를 만들 수 있습니다. [[!DNL Identity Service]](./api/create-custom-namespace.md) API 또는 UI를 통해.

UI를 사용하여 사용자 지정 네임스페이스를 만들려면 다음 위치로 이동합니다. **[!UICONTROL ID]** 작업 영역, 선택 **[!UICONTROL 찾아보기]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL ID 네임스페이스 만들기]**.

![select-create](./images/select-create.png)

다음 **[!UICONTROL ID 네임스페이스 만들기]** 대화 상자가 나타납니다. 고유한 값 제공 **[!UICONTROL 표시 이름]** 및 **[!UICONTROL ID 심볼]** 그런 다음 만들려는 id 유형을 선택합니다. 선택적 설명을 추가하여 네임스페이스에 대한 추가 정보를 추가할 수도 있습니다. 다음을 제외한 모든 ID 유형 **비사용자 식별자** 는 동일한 결합 동작을 따릅니다. 다음을 선택하는 경우 **비사용자 식별자** 네임스페이스를 만들 때 id 유형으로 연결이 발생하지 않습니다. 각 ID 유형에 대한 특정 정보는 의 표를 참조하십시오 [id 유형](#identity-types).

완료되면 다음을 선택합니다. **[!UICONTROL 만들기]**.

>[!IMPORTANT]
>
>정의한 네임스페이스는 조직의 개인 네임스페이스이며 성공적으로 생성하려면 고유한 ID 기호가 필요합니다.

![create-identity-namespace](./images/create-identity-namespace.png)

표준 네임스페이스와 마찬가지로 **[!UICONTROL 찾아보기]** 탭하여 세부 정보를 볼 수 있습니다. 그러나 사용자 지정 네임스페이스를 사용하면 세부 정보 영역에서 표시 이름 및 설명을 편집할 수도 있습니다.

>[!NOTE]
>
>네임스페이스를 만든 후에는 삭제할 수 없으며 ID 기호 및 유형을 변경할 수 없습니다.

## ID 데이터의 네임스페이스

ID에 대한 네임스페이스를 제공하는 것은 ID 데이터를 제공하는 데 사용하는 메서드에 따라 다릅니다. 데이터 ID 데이터 제공에 대한 자세한 내용은 [id 데이터 제공](./home.md#supplying-identity-data-to-identity-service) 다음에서 [!DNL Identity Service] 개요.

## 다음 단계

이제 ID 네임스페이스의 주요 개념을 이해했으므로 다음을 사용하여 ID 그래프로 작업하는 방법을 배울 수 있습니다. [id 그래프 뷰어](./ui/identity-graph-viewer.md).
