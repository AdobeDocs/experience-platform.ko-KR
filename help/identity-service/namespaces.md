---
keywords: Experience Platform;홈;인기 항목;네임스페이스;네임스페이스;네임스페이스;네임스페이스;네임스페이스;네임스페이스;ID 네임스페이스;ID 네임스페이스;ID;ID;ID 서비스;ID 서비스;Identity Service
solution: Experience Platform
title: ID 네임스페이스 개요
topic-legacy: overview
description: ID 네임스페이스는 ID 서비스의 구성 요소이며 ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어, "name@email.com" 값을 이메일 주소로 구분하거나 "443522" 값을 숫자 CRM ID로 구분할 수 있습니다.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 2%

---

# ID 네임스페이스 개요

ID 네임스페이스는 ID와 관련된 컨텍스트의 표시기 역할을 하는 [[!DNL Identity Service]](./home.md)의 구성 요소입니다. 예를 들어, &quot;name<span>@email.com&quot; 값을 이메일 주소로 구분하거나 &quot;443522&quot; 값을 숫자 CRM ID로 구분할 수 있습니다.

## 시작하기

ID 네임스페이스를 사용하여 작업하려면 관련 다양한 Adobe Experience Platform 서비스를 이해해야 합니다. 네임스페이스로 작업하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../profile/home.md):여러 소스에서 수집한 데이터를 기반으로 통합된 고객 프로파일을 실시간으로 제공합니다.
- [[!DNL Identity Service]](./home.md):다양한 디바이스와 시스템에 ID를 연결함으로써 개별 고객과 고객의 행동을 보다 정확하게 파악할 수 있습니다.
- [[!DNL Privacy Service]](../privacy-service/home.md):ID 네임스페이스는 네임스페이스와 관련하여 GDPR 요청을 수행할 수 있는 GDPR(General Data Protection Regulation)을 준수하는 데 사용됩니다.

## ID 네임스페이스 이해

정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 프로필 데이터 간에 레코드 데이터를 일치시키는 경우 [!DNL Real-time Customer Profile]이 프로필 데이터를 병합할 때 ID 값과 네임스페이스가 모두 일치해야 합니다.

예를 들어, 두 프로필 조각은 다른 기본 ID를 포함할 수 있지만 &quot;이메일&quot; 네임스페이스에 대해 동일한 값을 공유하므로 [!DNL Platform]은 이러한 조각이 실제로 동일한 개인임을 확인하고 해당 데이터를 개인 ID 그래프에 가져올 수 있습니다.

![](images/identity-service-stitching.png)

### ID 유형

여러 가지 ID 유형으로 데이터를 식별할 수 있습니다. ID 유형은 ID 네임스페이스가 만들어질 때 지정되며 데이터가 ID 그래프로 유지되는지 여부와 데이터를 처리하는 방법에 대한 특별 지침을 제어합니다.

다음 ID 유형은 [!DNL Platform] 내에서 사용할 수 있습니다.

| ID 유형 | 설명 |
| --- | --- |
| 쿠키 ID | 쿠키 ID는 웹 브라우저를 식별합니다. 이러한 ID는 확장을 위해 매우 중요하며 ID 그래프의 대부분을 구성합니다. 하지만, 자연은 시간이 지남에 따라 빠르게 퇴화하고 그들의 가치를 잃는다. |
| 장치 간 ID | 장치 간 ID는 개인을 식별하며 일반적으로 다른 ID를 함께 연결합니다. 로그인 ID, CRM ID 및 충성도 ID를 예로 들 수 있습니다. 이 값은 [!DNL Identity Service]에 대한 표시이며, 이 값은 민감합니다. |
| 장치 ID | 장치 ID는 IDFA(iPhone 및 iPad), GAID(Android) 및 RIDA(Roku)와 같은 하드웨어 장치를 식별하며, 가정에서 여러 사람이 공유할 수 있습니다. |
| 이메일 주소 | 이메일 주소는 종종 한 사람과 연결되어 있으므로 다양한 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 개인 식별 정보(PII)가 포함됩니다. 이 값은 [!DNL Identity Service]에 대한 표시이며, 이 값은 민감합니다. |
| 사람이 아닌 식별자 | 사람이 아닌 ID는 네임스페이스가 필요하지만 사람 클러스터에 연결되지 않은 식별자를 저장하는 데 사용됩니다. 예를 들어 제품 SKU, 제품, 조직 또는 스토어와 관련된 데이터. |
| 전화번호 | 전화 번호는 종종 한 사람과 연결되어 있으므로 여러 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII가 포함됩니다. 이 값은 [!DNL Identity Service]에 표시되므로 섬세하게 값을 처리할 수 있습니다. |

### 표준 네임스페이스

Experience Platform은 모든 조직에서 사용할 수 있는 몇 가지 ID 네임스페이스를 제공합니다. 이러한 네임스페이스는 표준 네임스페이스라고 하며 [!DNL Identity Service] API 또는 플랫폼 UI를 통해 볼 수 있습니다.

플랫폼 내의 모든 조직에서 사용할 수 있도록 다음과 같은 표준 네임스페이스가 제공됩니다.

| 디스플레이 이름 | 설명 |
| ------------ | ----------- |
| AdCloud | Adobe AdCloud를 나타내는 네임스페이스입니다. |
| Adobe Analytics(기존 ID) | Adobe Analytics을 나타내는 네임스페이스입니다. 자세한 내용은 [Adobe Analytics 네임스페이스](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces)에 대한 다음 문서를 참조하십시오. |
| Apple IDFA(광고주의 ID) | 광고주의 Apple ID를 나타내는 네임스페이스입니다. 자세한 내용은 [관심 기반 광고](https://support.apple.com/en-us/HT202074)의 다음 문서를 참조하십시오. |
| Apple 푸시 알림 서비스 | Apple 푸시 알림 서비스를 사용하여 수집한 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Apple 푸시 알림 서비스](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)의 다음 문서를 참조하십시오. |
| CORE | Adobe Audience Manager을 나타내는 네임스페이스입니다. 이 네임스페이스는 이전 이름으로 참조할 수도 있습니다.&quot;Adobe AudienceManager&quot;. 자세한 내용은 [Audience Manager ID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids)에 있는 다음 문서를 참조하십시오. |
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 다음 별칭으로 참조할 수도 있습니다.&quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 자세한 내용은 [ECID](./ecid.md)의 다음 문서를 참조하십시오. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람과 연결되어 있으므로 다른 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. |
| 이메일(SHA256, 소문자) | 미리 해시된 이메일 주소의 네임스페이스입니다. 이 네임스페이스에 제공된 값은 SHA256으로 해싱하기 전에 소문자로 변환됩니다. 이메일 주소가 표준화되기 전에 맨 앞과 뒤에 오는 공백을 잘라내야 합니다. 이 설정은 소급 변경할 수 없습니다. 자세한 내용은 [SHA256 해싱 지원](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support)에 있는 다음 문서를 참조하십시오. |
| Firebase 클라우드 메시지 | 푸시 알림에 대해 Google Firebase 클라우드 메시지를 사용하여 수집한 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Google Firebase 클라우드 메시지](https://firebase.google.com/docs/cloud-messaging)에 있는 다음 문서를 참조하십시오. |
| Google 광고 ID(GAID) | Google 광고 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Google 광고 ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)의 다음 문서를 참조하십시오. |
| Google 클릭 ID | Google 클릭 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Google 광고](https://developers.google.com/adwords/api/docs/guides/click-tracking)의 클릭 추적에 대한 다음 문서를 참조하십시오. |
| 전화 | 전화 번호를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람과 연결되어 있으므로 다른 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. |
| 전화(E.164) | E.164 형식으로 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. E.164 형식에는 더하기 기호(`+`), 국제 전화 코드, 지역 번호 및 전화 번호가 포함되어 있습니다. 예: `(+)(country code)(area code)(phone number)`. |
| 전화(SHA256) | SHA256을 사용하여 해시해야 하는 전화 번호를 나타내는 네임스페이스입니다. 심볼, 문자 및 0을 제거해야 합니다. 국가 호출 코드도 접두사로 추가해야 합니다. |
| 전화(SHA256_E.164) | SHA256 및 E.164 형식을 모두 사용하여 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. |
| TNTID | Adobe Target을 나타내는 네임스페이스입니다. 자세한 내용은 [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en)에서 다음 문서를 참조하십시오. |
| Windows AID | Windows 광고 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Windows 광고 ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041)의 다음 문서를 참조하십시오. |

UI에서 표준 네임스페이스를 보려면 왼쪽 탐색 메뉴에서 **[!UICONTROL Identities]**&#x200B;을 선택한 다음 **[!UICONTROL Browse]** 탭을 선택하여 조직에서 액세스할 수 있는 표준 ID 네임스페이스 목록을 표시합니다. 네임스페이스를 알파벳순으로 **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]** 또는 **[!UICONTROL Owner]**&#x200B;별로 정렬할 수 있습니다. 또는 네임스페이스의 최신 업데이트 날짜별로 시간순으로 정렬할 수 있습니다.

오른쪽 레일에 대한 자세한 정보를 보려면 네임스페이스를 선택하십시오.

>[!NOTE]
>
>또한 플랫폼은 통합 용도로 네임스페이스를 제공합니다. 이러한 네임스페이스는 다른 시스템과 연결하는 데 사용되고 ID를 연결하는 데 사용되지 않으므로 기본적으로 숨겨집니다. 통합 네임스페이스를 보려면 **[!UICONTROL View integration identities]**&#x200B;을 선택합니다.

![](./images/browse-namespaces.png)

## 사용자 정의 네임스페이스 관리 {#manage-namespaces}

조직 데이터 및 사용 사례에 따라 사용자 정의 네임스페이스가 필요할 수 있습니다. 사용자 정의 네임스페이스는 [[!DNL Identity Service]](./api/create-custom-namespace.md) API를 사용하거나 UI를 통해 만들 수 있습니다.

UI를 사용하여 사용자 정의 네임스페이스를 만들려면 **[!UICONTROL Identities]** 작업 영역으로 이동하여 **[!UICONTROL Browse]**&#x200B;을 선택한 다음 **[!UICONTROL Create identity namespace]**&#x200B;를 선택합니다.

![](./images/create.png)

**[!UICONTROL Create identity namespace]** 대화 상자가 나타납니다. 고유한 **[!UICONTROL Display name]** 및 **[!UICONTROL Identity symbol]**&#x200B;을 제공한 다음 만들려는 ID 유형을 선택합니다. 네임스페이스에 대한 추가 정보에 선택적 설명을 추가할 수도 있습니다. 완료되면 **[!UICONTROL Create]**&#x200B;을 선택합니다.

>[!IMPORTANT]
>
>정의한 네임스페이스는 조직에 비공개로 설정되므로 제대로 만들려면 고유한 ID 기호가 필요합니다.

![](./images/create-namespace.png)

표준 네임스페이스와 유사하게 **[!UICONTROL Browse]** 탭에서 사용자 정의 네임스페이스를 선택하여 세부 사항을 볼 수 있습니다. 그러나 사용자 정의 네임스페이스를 사용하면 세부 사항 영역에서 표시 이름과 설명을 편집할 수도 있습니다.

>[!NOTE]
>
>네임스페이스를 만든 후에는 이를 삭제할 수 없으며 해당 ID 기호 및 유형을 변경할 수 없습니다.

## ID 데이터의 네임스페이스

ID에 대한 네임스페이스를 제공하는 것은 ID 데이터를 제공하는 데 사용하는 방법에 따라 다릅니다. 데이터 ID 데이터를 제공하는 방법에 대한 자세한 내용은 [!DNL Identity Service] 개요에서 [ID 데이터](./home.md#supplying-identity-data-to-identity-service) 제공 섹션을 참조하십시오.

## 다음 단계

이제 ID 네임스페이스의 주요 개념을 이해했으므로 [ID 그래프 뷰어](./ui/identity-graph-viewer.md)를 사용하여 ID 그래프를 사용하는 방법을 배울 수 있습니다.
