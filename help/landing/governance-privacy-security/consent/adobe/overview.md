---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: Adobe Experience Platform의 동의 처리
topic-legacy: getting started
description: Adobe 2.0 표준을 사용하여 Adobe Experience Platform에서 고객 동의 신호를 처리하는 방법을 알아봅니다.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# Adobe Experience Platform의 동의 처리

Adobe Experience Platform을 사용하면 고객으로부터 수집한 동의 데이터를 처리하고 저장된 고객 프로파일에 통합할 수 있습니다. 그런 다음 다운스트림 프로세스에서 이 데이터를 사용하여 특정 고객에 대해 데이터 수집이 발생하는지 또는 해당 프로필이 특정 용도로 사용되는지 여부를 결정할 수 있습니다. 예를 들어 특정 프로필에 대한 동의 데이터는 내보낸 대상 세그먼트에 해당 프로필을 포함할 수 있는지, 이메일, 문자 메시지 또는 푸시 알림과 같은 특정 마케팅 채널에 참여할 수 있는지 여부를 결정할 수 있습니다.

이 문서에서는 CMP(Consent-Management Platform)에서 생성된 고객 동의 데이터를 인제스트하고 다운스트림 사용 사례를 위해 해당 데이터를 고객 프로파일에 통합하기 위해 플랫폼 데이터 작업을 구성하는 방법에 대한 개요를 제공합니다.

>[!NOTE]
>
>이 문서는 Adobe 표준을 사용하여 동의 데이터를 처리하는 데 중점을 둡니다. IAB 투명도 및 동의 프레임워크(TCF) 2.0을 준수하여 동의 데이터를 처리하는 경우 실시간 고객 데이터 플랫폼](../iab/overview.md)에서 [TCF 2.0 지원에 대한 안내서를 참조하십시오.

## 전제 조건

이 안내서는 동의 데이터 처리와 관련된 다양한 Experience Platform 서비스에 대해 제대로 이해해야 합니다.

* [경험 데이터 모델(XDM)](../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [Adobe Experience Platform ID 서비스](../../../../identity-service/home.md):디바이스 및 시스템 간의 ID를 결합함으로써 고객 경험 데이터의 세분화로 인해 발생하는 기본적인 문제를 해결합니다.
* [실시간 고객 프로필](../../../../profile/home.md):데이터 세트 [!DNL Identity Service] 에서 실시간으로 상세한 고객 프로파일을 만들 수 있습니다. 실시간 고객 프로필은 데이터 레이크에서 데이터를 가져와 별도의 데이터 저장소에 있는 고객 프로필을 유지합니다.
* [Adobe Experience Platform 웹 SDK](../../../../edge/home.md):다양한 플랫폼 서비스를 고객 중심의 웹 사이트에 통합할 수 있는 클라이언트측 JavaScript 라이브러리입니다.
   * [SDK 동의 명령](../../../../edge/consent/supporting-consent.md):이 안내서에 나와 있는 동의 관련 SDK 명령의 사용 사례 개요입니다.
* [Adobe Experience Platform 세그멘테이션 서비스](../../../../segmentation/home.md):실시간 고객 프로필 데이터를 비슷한 트레이트를 공유하고 마케팅 전략과 비슷하게 반응하는 개인 그룹으로 나눌 수 있습니다.

## 동의 처리 흐름 요약 {#summary}

다음은 시스템이 올바르게 구성된 후 동의 데이터가 처리되는 방식에 대한 설명입니다.

1. 고객은 웹 사이트의 대화 상자를 통해 데이터 수집에 대한 동의 기본 설정을 제공합니다.
1. 각 페이지 로드 시(또는 CMP에서 동의 환경 설정의 변경 사항을 감지하면) 사이트의 사용자 지정 스크립트는 현재 환경 설정을 표준 XDM 객체에 매핑합니다. 그런 다음 이 개체는 플랫폼 웹 SDK `setConsent` 명령으로 전달됩니다.
1. `setConsent`이(가) 호출되면 플랫폼 웹 SDK는 동의 값이 마지막으로 수신한 값과 다른지 확인합니다. 값이 다르거나 이전 값이 없는 경우 구조화된 동의/기본 설정 데이터가 Adobe Experience Platform으로 전송됩니다.
1. 동의/기본 설정 데이터는 스키마에 동의/기본 설정 필드가 포함된 [!DNL Profile] 사용 가능한 데이터 세트에 수집됩니다.

CMP 동의-변경 갈고리로 트리거되는 SDK 명령 외에도 동의 데이터는 고객이 생성한 XDM 데이터를 통해 Experience Platform으로 전달될 수 있으며, 이 데이터는 [!DNL Profile] 사용 가능한 데이터세트에 직접 업로드됩니다.

### 동의 집행

플랫폼의 동의 처리 지원의 현재 릴리스에서는 데이터 수집 권한(`collect.val`)만 플랫폼 웹 SDK에 의해 자동으로 적용됩니다. 보다 세부적인 동의 및 환경 설정을 수집하고 고객 프로파일에 유지할 수 있지만 이러한 추가 신호는 다운스트림 프로세스에서 수동으로 적용해야 합니다.

>[!NOTE]
>
>위에 언급된 XDM 동의 필드의 구조에 대한 자세한 내용은 [동의 및 기본 설정 데이터 유형](../../../../xdm/data-types/consents.md)의 안내서를 참조하십시오.

시스템이 구성되면 플랫폼 웹 SDK는 현재 사용자에 대한 데이터 수집 동의 값을 해석하여 데이터를 Adobe Experience Platform Edge Network로 전송할지, 클라이언트에서 전송할지, 데이터 수집 권한이 yes 또는 no로 설정될 때까지 유지할지 여부를 결정합니다.

## CMP {#consent-data} 내에서 고객 동의 데이터를 생성하는 방법 결정

각 CMP 시스템이 고유하므로 고객이 서비스와 상호 작용할 때 동의를 제공할 수 있는 최상의 방법을 결정해야 합니다. 이를 실현하는 일반적인 방법은 다음 예와 유사한 쿠키 동의 대화 상자를 사용하는 것입니다.

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

이 대화 상자를 통해 고객은 데이터에 대한 특정 마케팅 및 개인화 사용 사례를 옵트인 또는 옵트아웃할 수 있습니다. 동의 및 기본 설정은 다음 단계에서 [!DNL Profile] 사용 가능한 데이터 세트에 대해 정의하는 데이터 모델을 따라야 합니다.

## 표준 동의 필드를 [!DNL Profile] 사용 가능한 데이터 세트 {#dataset}에 추가합니다.

고객 동의 데이터는 스키마에 동의 필드가 포함된 [!DNL Profile] 사용 가능한 데이터 세트에 전송해야 합니다. 이러한 필드는 개별 고객에 대한 속성 정보를 캡처하는 데 사용하는 동일한 스키마 및 데이터 세트에 포함되어야 합니다.

이 안내서를 계속하기 전에 이러한 필수 필드를 [!DNL Profile] 사용 가능한 데이터 세트에 추가하는 방법에 대한 자세한 단계는 [동의 데이터 세트 구성을 위한 자습서를 참조하십시오.](./dataset.md)

## 동의 데이터 {#merge-policies}를 포함하도록 [!DNL Profile] 병합 정책을 업데이트합니다.

동의 데이터를 처리하기 위해 [!DNL Profile] 사용 가능한 데이터 세트를 만들었다면 병합 정책이 각 고객 프로필에 항상 동의 필드를 포함하도록 구성되어 있는지 확인해야 합니다. 데이터세트의 우선 순위를 설정하여 잠재적으로 충돌하는 다른 데이터세트보다 동의 데이터 세트에 대한 우선 순위를 지정합니다.

>[!NOTE]
>
>충돌하는 데이터세트가 없는 경우 병합 정책에 대해 타임스탬프 우선 순위를 설정해야 합니다. 이렇게 하면 고객이 지정한 최신 동의가 사용되는 동의 설정인지 확인할 수 있습니다.

병합 정책을 사용하는 방법에 대한 자세한 내용은 [병합 정책 사용 안내서](../../../../profile/ui/merge-policies.md)를 참조하십시오. 병합 정책을 설정할 때 [데이터세트 준비](./dataset.md)에 대한 안내서에 설명된 대로 동의 및 기본 설정 스키마 필드 그룹에서 제공하는 모든 필수 동의 속성이 프로필에 포함되어 있는지 확인해야 합니다.

## 동의 데이터를 플랫폼에 가져오기

데이터 세트를 생성하고 고객 프로파일에서 필수 동의 필드를 나타내는 정책을 통합하면 다음 단계는 동의 데이터를 Platform(플랫폼)으로 가져오는 것입니다.

주로 CMP에서 동의 변경 이벤트를 탐지할 때마다 Adobe Experience Platform 웹 SDK를 사용하여 동의 데이터를 플랫폼에 보내야 합니다. 모바일 플랫폼에서 동의 데이터를 수집하는 경우 Adobe Experience Platform Mobile SDK를 사용해야 합니다. 또한 동의 데이터 집합의 XDM 스키마에 수신한 동의 데이터를 직접 매핑하여 일괄 처리를 통해 플랫폼에 전송함으로써 수집된 동의 데이터를 인제스트하도록 선택할 수 있습니다.

이러한 각 방법에 대한 세부 사항은 아래 하위 섹션에 제공됩니다.

### Experience Platform 웹 SDK를 구성하여 동의 데이터 {#web-sdk} 처리

웹 사이트에서 동의-변경 이벤트를 수신하도록 CMP를 구성한 경우, Experience Platform 웹 SDK를 통합하여 업데이트된 동의 설정을 받아 페이지 로드 및 동의-변경 이벤트가 발생할 때마다 플랫폼에 보낼 수 있습니다. 자세한 내용은 [고객 동의 데이터](./sdk.md)를 처리하도록 웹 SDK를 구성하는 지침을 참조하십시오.

### Experience Platform Mobile SDK를 구성하여 동의 데이터 {#mobile-sdk} 처리

모바일 애플리케이션에서 고객 동의 기본 설정이 필요한 경우 Experience Platform Mobile SDK를 통합하여 동의 API가 호출될 때마다 동의 설정을 검색 및 업데이트하여 Platform으로 전송할 수 있습니다.

동의 API](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent/edge-consent-api-reference)를 사용하여 [동의 모바일 확장 구성](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent) 및 [에 대한 모바일 SDK 설명서를 참조하십시오. Mobile SDK를 사용하여 개인 정보 보호 문제를 처리하는 방법에 대한 자세한 내용은 [개인 정보 보호 및 GDPR](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/resources/privacy-and-gdpr) 섹션을 참조하십시오.

### XDM 호환 동의 데이터를 직접 인제스트 {#batch}

일괄 처리를 사용하여 CSV 파일에서 XDM 호환 동의 데이터를 수집할 수 있습니다. 이 기능은 고객 프로필에 아직 통합되지 않은 이전에 수집한 동의 데이터의 백로그가 있는 경우에 유용합니다.

데이터 필드를 XDM으로 변환하고 Platform으로 인제스트하는 방법을 알아보려면 [CSV 파일을 XDM](../../../../ingestion/tutorials/map-a-csv-file.md)에 매핑의 자습서를 따릅니다. 매핑에 대해 [!UICONTROL Destination]을 선택할 때 **[!UICONTROL Use existing dataset]** 옵션을 선택하고 이전에 만든 [!DNL Profile] 사용 동의 데이터 세트를 선택합니다.

## 구현 테스트 {#test-implementation}

고객 동의 데이터를 [!DNL Profile] 사용 데이터세트에 인제스트한 후 업데이트된 프로파일에 동의 속성이 포함되어 있는지 확인할 수 있습니다.

>[!IMPORTANT]
>
>UI에서 기존 프로필의 속성을 보려면 해당 프로필과 연결된 ID 값(및 해당 네임스페이스)을 하나 이상 알아야 합니다.
>
>이 정보에 대한 액세스 권한이 없는 경우 자체 테스트 동의 데이터를 인제스트하도록 선택하고 대신 사용자에게 알려진 ID 값/네임스페이스와 연결할 수 있습니다.

프로필의 세부 사항을 찾는 방법에 대한 특정 단계는 [!DNL Profile] UI 안내서의 [ID](../../../../profile/ui/user-guide.md#browse)로 프로필 검색 섹션을 참조하십시오.

새 동의 속성은 기본적으로 프로필의 대시보드에 나타나지 않습니다. 따라서 예상대로 인제스트되었는지 확인하려면 프로필의 세부 정보 페이지에서 **[!UICONTROL Attributes]** 탭으로 이동해야 합니다. 요구 사항에 맞게 대시보드를 사용자 지정하는 방법을 알아보려면 [프로필 대시보드](../../../../profile/ui/profile-dashboard.md)의 안내서를 참조하십시오.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 다음 단계

이 안내서에서는 Adobe 표준을 사용하여 고객 동의 데이터를 처리하고 이러한 속성을 고객 프로파일에 표시하도록 플랫폼 작업을 구성하는 방법에 대해 설명합니다. 이제 세그먼트 자격 조건 및 기타 다운스트림 사용 사례 결정 요소로 고객 동의 기본 설정을 통합할 수 있습니다.

Experience Platform의 개인정보 보호 관련 기능에 대한 자세한 내용은 플랫폼](../../overview.md)의 [거버넌스, 개인 정보 및 보안에 대한 개요를 참조하십시오.
