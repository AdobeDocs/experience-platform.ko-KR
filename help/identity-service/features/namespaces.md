---
title: ID 네임스페이스 개요
description: ID 서비스의 ID 네임스페이스에 대해 알아봅니다.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 16%

---

# ID 네임스페이스 개요

Adobe Experience Platform ID 서비스에서 ID 네임스페이스로 수행할 수 있는 작업에 대해 자세히 알아보려면 다음 문서를 참조하십시오.

## 시작하기

ID 네임스페이스를 사용하려면 다양한 Adobe Experience Platform 서비스에 대한 이해가 필요합니다. 네임스페이스 작업을 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 고객 프로필을 실시간으로 제공합니다.
* [[!DNL Identity Service]](../home.md): 장치 및 시스템 간에 ID를 연결하여 개별 고객 및 개별 고객의 행동을 더 잘 볼 수 있습니다.
* [[!DNL Privacy Service]](../../privacy-service/home.md): ID 네임스페이스는 GDPR(일반 데이터 보호 규정)과 같은 법적 개인 정보 보호 규정에 대한 준수 요청에 사용됩니다. 각 개인 정보 보호 요청은 영향을 받아야 하는 소비자의 데이터를 식별하기 위해 네임스페이스를 기준으로 수행됩니다.

## ID 네임스페이스 이해 {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="ID 네임스페이스"
>abstract="ID 네임스페이스는 특정 ID의 컨텍스트입니다. 예를 들어 `Email`의 네임스페이스는 **name<span>@acme.com**&#x200B;에 해당할 수 있습니다. 마찬가지로 `Phone`의 네임스페이스는 `555-555-1234`에 해당할 수 있습니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="ID 값"
>abstract="ID 값은 고유 개인, 조직 또는 자산을 나타내는 식별자입니다. 값이 표시하는 ID의 컨텍스트 또는 유형은 해당 ID 네임스페이스에 의해 정의됩니다. 프로필 조각 전체에서 레코드 데이터를 일치시킬 때 네임스페이스와 ID 값이 일치해야 합니다. 프로필 조각 전체에서 레코드 데이터를 일치시킬 때 네임스페이스와 ID 값이 일치해야 합니다."
>text="Learn more in documentation"

정규화된 ID에는 **ID 값**&#x200B;과(와) **ID 네임스페이스**&#x200B;의 두 가지 구성 요소가 있습니다. 예를 들어 ID의 값이 `scott@acme.com`인 경우 네임스페이스는 이 값을 이메일 주소로 구별하여 컨텍스트를 제공합니다. 마찬가지로 네임스페이스는 `555-123-456`을(를) 전화 번호로, `3126ABC`을(를) CRMID로 구분할 수 있습니다. 기본적으로 **네임스페이스는 특정 ID에 컨텍스트를 제공합니다**. [!DNL Real-Time Customer Profile]이(가) 프로필 데이터를 병합할 때와 같이 프로필 조각 간에 레코드 데이터를 일치시킬 때는 ID 값과 네임스페이스가 모두 일치해야 합니다.

예를 들어 두 개의 프로필 조각에 서로 다른 기본 ID가 포함되어 있을 수 있지만 &quot;이메일&quot; 네임스페이스에 대해 동일한 값을 공유하므로 Experience Platform은 이러한 조각이 실제로 동일한 개인임을 확인할 수 있으며 해당 개인의 ID 그래프에 데이터를 함께 가져옵니다.

>[!BEGINSHADEBOX]

**ID 네임스페이스 설명**

네임스페이스의 개념을 더 잘 이해할 수 있는 또 다른 방법은 도시 및 해당 상태와 같은 실제 사례를 고려하는 것입니다. 예를 들어, 포틀랜드, 메인, 그리고 오리건 포틀랜드는 미국에서 두 개의 다른 장소입니다. 도시는 같은 이름을 공유하는 반면, 국가는 네임스페이스로 작동하며 두 도시를 서로 구분하는 필요한 컨텍스트를 제공한다.

ID 서비스에 동일한 논리 적용:

* `1-234-567-8900`의 ID 값이 전화 번호처럼 보일 수 있습니다. 그러나 시스템 관점에서 이 값은 CRMID로 구성할 수 있습니다. ID 서비스에서는 해당 네임스페이스 없이 필요한 컨텍스트를 이 ID 값에 적용할 수 없습니다.
* 또 다른 예는 `john@gmail.com`의 ID 값입니다. 이 ID 값은 쉽게 이메일로 가정할 수 있지만 사용자 지정 네임스페이스 CRMID로 구성될 수 있습니다. 네임스페이스를 사용하면 `Email:john@gmail.com`과(와) `CRMID:john@gmail.com`을(를) 구분할 수 있습니다.

>[!ENDSHADEBOX]

### 네임스페이스의 구성 요소

네임스페이스는 다음 구성 요소로 구성됩니다.

* **표시 이름**: 지정한 네임스페이스에 대한 알기 쉬운 이름입니다.
* **ID 기호**: 네임스페이스를 나타내기 위해 ID 서비스에서 내부적으로 사용하는 코드입니다.
* **ID 형식**: 지정된 네임스페이스의 분류입니다.
* **설명**: (선택 사항) 특정 네임스페이스와 관련하여 제공할 수 있는 모든 추가 정보입니다.

### ID 유형 {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="ID 유형 지정"
>abstract="ID 유형은 데이터가 ID 그래프에 저장되는지 여부를 제어합니다. 비개인 식별자 및 파트너 ID 등의 신원 유형에 대해서는 아이덴티티 그래프가 생성되지 않습니다."
>text="Learn more in documentation"

ID 네임스페이스의 요소 중 하나는 **ID 유형**&#x200B;입니다. ID 유형은 다음을 결정합니다.

* ID 그래프 생성 여부:
   * 비개인 식별자 및 파트너 ID 등의 신원 유형에 대해서는 아이덴티티 그래프가 생성되지 않습니다.
   * ID 그래프는 다른 모든 ID 유형에 대해 생성됩니다.
* 시스템 제한에 도달하면 ID 그래프에서 제거되는 ID입니다. 자세한 내용은 [ID 데이터 보호](../guardrails.md)를 참조하십시오.

Experience Platform 내에서 사용할 수 있는 ID 유형은 다음과 같습니다.

| ID 유형 | 설명 |
| --- | --- |
| 쿠키 ID | 쿠키 ID는 웹 브라우저를 식별합니다. 이러한 ID는 확장에 중요하며 ID 그래프의 대부분을 구성합니다. 그러나 자연적으로 그들은 빠르게 부패하고 시간이 지남에 따라 가치를 잃습니다. |
| 교차 장치 ID | 크로스 디바이스 ID는 개인을 식별하며 일반적으로 다른 ID를 함께 연결합니다. 예를 들면 로그인 ID, CRMID 및 충성도 ID가 있습니다. 값을 민감하게 처리하기 위해 [!DNL Identity Service]에 대한 표시입니다. |
| 디바이스 ID | 디바이스 ID는 IDFA(iPhone 및 iPad), GAID(Android) 및 RIDA(Roku) 등 하드웨어 디바이스를 식별해 가정에서 여러 명이 공유할 수 있습니다. |
| 이메일 주소 | 이메일 주소는 종종 단일 사용자와 연결되므로, 다양한 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII(개인 식별 정보)가 포함됩니다. 값을 민감하게 처리하기 위해 [!DNL Identity Service]에 대한 표시입니다. |
| 비개인 식별자 | 비사용자 ID는 네임스페이스가 필요하지만 사용자 클러스터에 연결되지 않은 식별자를 저장하는 데 사용됩니다. 예를 들어 제품 SKU, 제품, 조직 또는 스토어와 관련된 데이터입니다. |
| 파트너 ID | <ul><li>파트너 ID는 데이터 파트너가 사람을 나타내기 위해 사용하는 식별자입니다. 파트너 ID는 종종 개인의 진짜 신분을 밝히지 않기 위해 가명으로 사용되며 확률적일 수 있습니다. Real-time Customer Data Platform에서 파트너 ID는 ID 그래프 링크 구축이 아니라 주로 확장된 대상 활성화 및 데이터 보강에 사용됩니다.</li><li>파트너 ID 유형으로 지정된 ID 네임스페이스가 포함된 ID를 수집할 때 ID 그래프가 생성되지 않습니다.</li><li>파트너 ID의 ID 유형을 사용하여 파트너 데이터를 수집하지 않으면 ID 서비스의 시스템 그래프 제한에 도달할 수 있을 뿐만 아니라 원치 않는 프로필 병합이 발생할 수 있습니다.</li><ul> |
| 전화번호 | 전화번호는 종종 한 사람과 연관되어 있으므로 다른 채널에서 해당 사람을 식별하는 데 사용할 수 있습니다. 이 유형의 ID에는 PII가 포함됩니다. 값을 민감하게 처리하기 위해 [!DNL Identity Service]에 대한 표시입니다. |

{style="table-layout:auto"}

### 표준 네임스페이스 {#standard}

Experience Platform은 모든 조직에서 사용할 수 있는 여러 ID 네임스페이스를 제공합니다. 표준 네임스페이스라고 하며 [!DNL Identity Service] API를 사용하거나 Platform UI를 통해 볼 수 있습니다.

다음 표준 네임스페이스는 Platform 내의 모든 조직에서 사용할 수 있도록 제공됩니다.

| 표시 이름 | 설명 |
| ------------ | ----------- |
| AdCloud | Adobe AdCloud를 나타내는 네임스페이스입니다. |
| Adobe Analytics (기존 ID) | Adobe Analytics을 나타내는 네임스페이스입니다. 자세한 내용은 [Adobe Analytics 네임스페이스](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces)에서 다음 문서를 참조하십시오. |
| Apple IDFA (광고주용 ID) | 광고주용 Apple ID를 나타내는 네임스페이스입니다. 자세한 내용은 [관심 기반 광고](https://support.apple.com/en-us/HT202074)에 대한 다음 문서를 참조하십시오. |
| Apple 푸시 알림 서비스 | Apple 푸시 알림 서비스를 사용하여 수집된 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Apple 푸시 알림 서비스](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)에 대한 다음 문서를 참조하십시오. |
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 자세한 내용은 [ECID](./ecid.md)에서 다음 문서를 참조하십시오. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 단일 사용자와 연결되므로 여러 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |
| 이메일(SHA256, 소문자) | 사전 해시된 이메일 주소를 위한 네임스페이스입니다. 이 네임스페이스에 제공된 값은 SHA256으로 해싱하기 전에 소문자로 변환됩니다. 전자 메일 주소가 정규화되기 전에 선행 및 후행 공백을 잘라내야 합니다. 이 설정은 소급하여 변경할 수 없습니다. 자세한 내용은 [SHA256 해시 지원](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support)에 대한 다음 문서를 참조하십시오. |
| Firebase 클라우드 메시징 | 푸시 알림용 Google Firebase Cloud Messaging을 사용하여 수집된 ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)에 대한 다음 문서를 참조하십시오. |
| Google 광고 ID (GAID) | Google Advertising ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)에 대한 다음 문서를 참조하십시오. |
| 휴대폰 | 전화 번호를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 단일 사용자와 연결되므로 여러 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |
| 전화(E.164) | E.164 형식으로 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. E.164 형식에는 더하기 기호(`+`), 국제 국가 호출 코드, 지역 번호 및 전화 번호가 포함됩니다. 예: `(+)(country code)(area code)(phone number)`. |
| 휴대폰 (SHA256) | SHA256을 사용하여 해시해야 하는 전화 번호를 나타내는 네임스페이스입니다. 기호, 문자 및 앞에 오는 0을 제거해야 합니다. 국가 호출 코드도 접두사로 추가해야 합니다. |
| 전화(SHA256_E.164) | SHA256과 E.164 형식을 모두 사용하여 해시해야 하는 원시 전화 번호를 나타내는 네임스페이스입니다. |
| TNTID | Adobe Target을 나타내는 네임스페이스입니다. 자세한 내용은 [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html)에 대한 다음 문서를 참조하십시오. |
| Windows AID | Windows Advertising ID를 나타내는 네임스페이스입니다. 자세한 내용은 [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041)에서 다음 문서를 참조하십시오. |

### ID 네임스페이스 보기 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="통합 ID 보기"
>abstract="통합 ID는 다른 시스템에 연결하는 데 사용되는 네임스페이스이며 ID 확인 또는 연결 ID에는 사용되지 않습니다. <br> 이러한 ID는 기본적으로 숨겨져 있습니다. 토글을 사용하여 통합 네임스페이스를 봅니다."

UI에서 ID 네임스페이스를 보려면 왼쪽 탐색에서 **[!UICONTROL ID]**&#x200B;를 선택한 다음 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.

조직의 네임스페이스 디렉터리가 나타나고 이름, ID 기호, 마지막으로 업데이트된 날짜, 해당 ID 유형 및 설명에 대한 정보가 표시됩니다.

![조직에 있는 사용자 지정 ID 네임스페이스의 디렉터리입니다.](../images/namespace/browse.png)

## 사용자 정의 네임스페이스 만들기 {#create-namespaces}

조직 데이터 및 사용 사례에 따라 사용자 정의 네임스페이스가 필요할 수 있습니다. [[!DNL Identity Service]](../api/create-custom-namespace.md) API를 사용하거나 UI를 통해 사용자 지정 네임스페이스를 만들 수 있습니다.

사용자 지정 네임스페이스를 만들려면 **[!UICONTROL ID 네임스페이스 만들기]**&#x200B;를 선택합니다.

>[!TIP]
>
>통합 ID는 다른 시스템과 연결하는 데 사용되는 네임스페이스입니다. ID 해결에는 사용되지 않으며 ID를 결합하는 데도 사용되지 않습니다. 목록을 업데이트하고 통합 ID를 포함하려면 **[!UICONTROL 통합 ID 보기]**&#x200B;를 선택하십시오. 그러나 통합 ID는 보기 전용이므로 구성할 필요가 없으므로 기본적으로 숨겨집니다.

![ID 작업 영역의 ID 네임스페이스 만들기 단추입니다.](../images/namespace/create-identity-namespace.png)

[!UICONTROL ID 네임스페이스 만들기] 창이 나타납니다. 먼저 만들려는 사용자 지정 네임스페이스에 대한 표시 이름과 ID 기호를 제공해야 합니다. 필요한 경우 만들고 있는 사용자 지정 네임스페이스에 더 많은 컨텍스트를 추가하는 설명을 제공할 수도 있습니다.

![사용자 지정 ID 네임스페이스와 관련된 정보를 입력할 수 있는 팝업 창입니다.](../images/namespace/name-and-symbol.png)

그런 다음 사용자 지정 네임스페이스에 할당할 ID 유형을 선택합니다. 완료되면 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

![사용자 지정 ID 네임스페이스에서 선택하고 할당할 수 있는 ID 유형 선택.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* 정의한 네임스페이스는 조직의 개인 네임스페이스이며 성공적으로 생성하려면 고유한 ID 기호가 필요합니다.
>
>* 네임스페이스를 만든 후에는 삭제할 수 없으며 ID 기호 및 유형을 변경할 수 없습니다.
>
>* 중복 네임스페이스는 지원되지 않습니다. 새 네임스페이스를 만들 때 기존 표시 이름과 ID 기호를 사용할 수 없습니다.

## ID 데이터의 네임스페이스

ID에 대한 네임스페이스를 제공하는 것은 ID 데이터를 제공하는 데 사용하는 메서드에 따라 다릅니다. 데이터 ID 데이터 제공에 대한 자세한 내용은 [[!DNL Identity Service] 구현 가이드](../implementation.md)를 참조하십시오.

## 다음 단계

ID 네임스페이스의 주요 개념을 이해했으므로 [ID 그래프 뷰어](../features/identity-graph-viewer.md)를 사용하여 ID 그래프를 사용하는 방법을 배울 수 있습니다.
