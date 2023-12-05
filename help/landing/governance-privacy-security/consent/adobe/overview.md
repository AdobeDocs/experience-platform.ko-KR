---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Adobe Experience Platform의 동의 처리
description: Adobe 2.0 표준을 사용하여 Adobe Experience Platform에서 고객 동의 신호를 처리하는 방법에 대해 알아봅니다.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: d23f1cc9dd0155aceae78bf938d35463e9c38181
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Adobe Experience Platform에서 동의 처리

Adobe Experience Platform을 사용하면 고객으로부터 수집한 동의 데이터를 처리하고 저장된 고객 프로필에 통합할 수 있습니다. 그런 다음 다운스트림 프로세스에서 이 데이터를 사용하여 특정 고객에 대해 데이터 수집이 발생하는지 또는 해당 프로필이 특정 용도로 사용되는지 여부를 확인할 수 있습니다. 예를 들어 특정 프로필에 대한 동의 데이터는 내보낸 대상 세그먼트에 포함할 수 있는지 여부 또는 이메일, 텍스트 메시지 또는 푸시 알림과 같은 특정 마케팅 채널에 참여할 수 있는지 여부를 결정할 수 있습니다.

이 문서에서는 CMP(동의 관리 플랫폼)에서 생성된 고객 동의 데이터를 수집하고 다운스트림 사용 사례를 위해 해당 데이터를 고객 프로필에 통합하도록 플랫폼 데이터 작업을 구성하는 방법에 대한 개요를 제공합니다.

>[!NOTE]
>
>이 문서는 Adobe 표준을 사용하는 동의 데이터 처리에 중점을 둡니다. IAB TCF(Transparency and Consent Framework) 2.0을 준수하여 동의 데이터를 처리하는 경우 의 안내서를 참조하십시오. [Adobe Real-time Customer Data Platform의 TCF 2.0 지원](../iab/overview.md).

## 전제 조건

이 안내서를 사용하려면 동의 데이터 처리와 관련된 다양한 Experience Platform 서비스에 대한 작업 이해가 필요합니다.

* [경험 데이터 모델(XDM)](../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [Adobe Experience Platform ID 서비스](../../../../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인해 발생하는 근본적인 문제를 해결합니다.
* [실시간 고객 프로필](../../../../profile/home.md): 사용 [!DNL Identity Service] 데이터 세트에서 실시간으로 세부 고객 프로필을 만드는 기능. 실시간 고객 프로필은 데이터 레이크에서 데이터를 가져와 별도의 데이터 저장소에 고객 프로필을 유지합니다.
* [Adobe Experience Platform 웹 SDK](../../../../edge/home.md): 다양한 Platform 서비스를 고객 응대 웹 사이트에 통합할 수 있는 클라이언트측 JavaScript 라이브러리.
   * [SDK 동의 명령](../../../../edge/consent/supporting-consent.md): 이 안내서에 표시된 동의 관련 SDK 명령에 대한 사용 사례 개요.
* [Adobe Experience Platform 세그멘테이션 서비스](../../../../segmentation/home.md): 실시간 고객 프로필 데이터를 유사한 트레이트를 공유하고 마케팅 전략에 유사하게 반응하는 개인 그룹으로 나눌 수 있습니다.

## 동의 처리 흐름 요약 {#summary}

다음은 시스템이 제대로 구성된 후 동의 데이터를 처리하는 방법에 대해 설명합니다.

1. 고객은 웹 사이트의 대화 상자를 통해 데이터 수집에 대한 동의 환경 설정을 제공합니다.
1. 페이지를 로드할 때마다(또는 CMP에서 동의 환경 설정이 변경될 때) 사이트의 사용자 지정 스크립트는 현재 환경 설정을 표준 XDM 개체에 매핑합니다. 그런 다음 이 개체가 Platform Web SDK에 전달됩니다 `setConsent` 명령입니다.
1. 날짜 `setConsent` 가 호출되면 Platform Web SDK는 동의 값이 마지막으로 받은 값과 다른지 확인합니다. 값이 다르거나 이전 값이 없는 경우 구조화된 동의/환경 설정 데이터가 Adobe Experience Platform으로 전송됩니다.
1. 동의/환경 설정 데이터는에 수집됩니다. [!DNL Profile]- 스키마에 동의/환경 설정 필드가 포함된 데이터 세트가 활성화되었습니다.

CMP 동의 변경 후크에서 트리거한 SDK 명령 외에도 동의 데이터는에 직접 업로드되는 고객 생성 XDM 데이터를 통해 Experience Platform으로 유입될 수 있습니다. [!DNL Profile]-활성화된 데이터 세트.

### 동의 적용

현재 Platform의 동의 처리 지원 릴리스에서는 데이터 수집 권한만 필요합니다(`collect.val`)은 Platform Web SDK에 의해 자동으로 적용됩니다. 보다 세분화된 동의와 환경 설정을 수집하여 고객 프로필에서 지속할 수 있지만, 이러한 추가 신호는 자체 다운스트림 프로세스에서 수동으로 적용되어야 합니다.

>[!NOTE]
>
>위에 언급된 XDM 동의 필드의 구조에 대한 자세한 내용은 [[!UICONTROL 동의 및 환경 설정] 데이터 유형](../../../../xdm/data-types/consents.md).

시스템이 구성되면 Platform Web SDK는 현재 사용자에 대한 데이터 수집 동의 값을 해석하여 데이터를 Adobe Experience Platform Edge Network로 전송할지, 클라이언트에서 삭제할지, 데이터 수집 권한이 yes 또는 no로 설정될 때까지 유지할지를 결정합니다.

## CMP 내에서 고객 동의 데이터를 생성하는 방법 결정 {#consent-data}

각 CMP 시스템은 고유하므로 고객이 서비스와 상호 작용할 때 동의를 제공할 수 있는 최상의 방법을 결정해야 합니다. 이를 위해 다음 예제와 유사한 쿠키 동의 대화 상자를 사용하는 것이 일반적인 방법입니다.

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

이 대화 상자를 통해 고객은 데이터에 대한 특정 마케팅 및 개인화 사용 사례를 옵트인 또는 옵트아웃할 수 있습니다. 이러한 동의 및 환경 설정은 다음에 대해 정의한 데이터 모델을 준수해야 합니다. [!DNL Profile]- 다음 단계에서 데이터 세트를 활성화했습니다.

## 에 표준화된 동의 필드 추가 [!DNL Profile]-enabled dataset {#dataset}

고객 동의 데이터를 (으)로 보내야 합니다. [!DNL Profile]- 스키마에 동의 필드가 포함된 데이터 세트가 활성화되었습니다. 이러한 필드는 개별 고객에 대한 속성 정보를 캡처하는 데 사용하는 것과 동일한 스키마 및 데이터 세트에 포함되어야 합니다.

다음 튜토리얼 참조: [동의 데이터 캡처를 위한 데이터 세트 구성](./dataset.md) 이러한 필수 필드를 추가하는 방법에 대한 자세한 단계는 [!DNL Profile]-이 안내서를 계속하기 전에 데이터 세트를 활성화했습니다.

## 업데이트 [!DNL Profile] 동의 데이터를 포함하는 정책 병합 {#merge-policies}

을(를) 생성한 후 [!DNL Profile]동의 데이터를 처리하기 위해 데이터 세트를 활성화했습니다. 병합 정책이 각 고객 프로필에 동의 필드를 항상 포함하도록 구성되었는지 확인해야 합니다. 여기에는 데이터 세트 우선 순위를 설정하여 동의 데이터 세트가 잠재적으로 충돌할 수 있는 다른 데이터 세트보다 우선하도록 하는 작업이 포함됩니다.

>[!NOTE]
>
>충돌하는 데이터 세트가 없는 경우 병합 정책에 대한 타임스탬프 우선 순위를 대신 설정해야 합니다. 이렇게 하면 고객이 지정한 최신 동의가 사용된 동의 설정인지 확인하는 데 도움이 됩니다.

병합 정책으로 작업하는 방법에 대한 자세한 내용은 [병합 정책 개요](../../../../profile/merge-policies/overview.md). 병합 정책을 설정할 때에는 프로필에 에서 제공하는 모든 필수 동의 속성이 포함되어 있는지 확인해야 합니다 [!UICONTROL 동의 및 환경 설정] 의 안내서에 요약된 스키마 필드 그룹 [데이터 세트 준비](./dataset.md).

## 플랫폼으로 동의 데이터 가져오기

고객 프로필의 필수 동의 필드를 표시하는 데이터 세트와 병합 정책이 있으면 다음 단계에서 동의 데이터 자체를 플랫폼으로 가져오는 것입니다.

주로 CMP에서 동의 변경 이벤트가 감지될 때마다 Adobe Experience Platform 웹 SDK를 사용하여 플랫폼에 동의 데이터를 보내야 합니다. 모바일 플랫폼에서 동의 데이터를 수집하는 경우 Adobe Experience Platform Mobile SDK를 사용해야 합니다. 수집된 동의 데이터를 동의 데이터 세트의 XDM 스키마에 매핑하고 일괄 수집을 통해 플랫폼으로 전송하여 직접 수집하도록 선택할 수도 있습니다.

이러한 각 방법에 대한 자세한 내용은 아래 하위 섹션에 나와 있습니다.

### 동의 데이터를 처리하도록 Experience Platform Web SDK 구성 {#web-sdk}

웹 사이트에서 동의 변경 이벤트를 수신하도록 CMP를 구성했으면 Experience Platform 웹 SDK를 통합하여 업데이트된 동의 설정을 수신하고 모든 페이지 로드 및 동의 변경 이벤트가 발생할 때마다 플랫폼으로 전송할 수 있습니다. 다음 안내서를 참조하십시오 [고객 동의 데이터를 처리하도록 Web SDK 구성](../sdk.md) 추가 정보.

### 동의 데이터를 처리하도록 Experience Platform Mobile SDK 구성 {#mobile-sdk}

모바일 애플리케이션에 고객 동의 환경 설정이 필요한 경우 Experience Platform Mobile SDK를 통합하여 동의 설정을 검색하고 업데이트할 수 있으며, 동의 API가 호출될 때마다 이를 Platform으로 전송할 수 있습니다.

용 Mobile SDK 설명서 를 참조하십시오. [동의 모바일 확장 구성](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) 및 [동의 API 사용](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Mobile SDK를 사용하여 개인 정보 문제를 처리하는 방법에 대한 자세한 내용은 섹션을 참조하십시오 [개인 정보 및 GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### XDM 호환 동의 데이터 직접 수집 {#batch}

일괄 처리 수집을 사용하여 CSV 파일에서 XDM 호환 동의 데이터를 수집할 수 있습니다. 이 기능은 고객 프로필에 아직 통합되지 않은 이전에 수집된 동의 데이터의 백로그가 있는 경우 유용할 수 있습니다.

다음에 대한 자습서를 따르십시오 [XDM에 CSV 파일 매핑](../../../../ingestion/tutorials/map-csv/overview.md) 데이터 필드를 XDM으로 변환하고 Platform으로 수집하는 방법에 대해 알아봅니다. 을(를) 선택할 때 [!UICONTROL 대상] 매핑에 대해 다음을 선택해야 합니다. **[!UICONTROL 기존 데이터 세트 사용]** 옵션을 선택하고 [!DNL Profile]이전에 생성한 동의 데이터 세트가 활성화되었습니다.

## 구현 테스트 {#test-implementation}

고객 동의 데이터를 로 수집한 후 [!DNL Profile]-활성화된 데이터 세트에서는 업데이트된 프로필에서 동의 속성을 포함하는지 확인할 수 있습니다.

>[!IMPORTANT]
>
>UI에서 기존 프로필의 속성을 보려면 해당 프로필과 연결된 ID 값(및 해당 네임스페이스)을 하나 이상 알고 있어야 합니다.
>
>이 정보에 대한 액세스 권한이 없는 경우 자체 테스트 동의 데이터를 수집하여 대신 사용자에게 알려진 ID 값/네임스페이스와 연결하도록 선택할 수 있습니다.

의 섹션을 참조하십시오. [id별 프로필 검색](../../../../profile/ui/user-guide.md#browse) 다음에서 [!DNL Profile] 프로필 세부 정보를 조회하는 방법에 대한 특정 단계는 UI 안내서를 참조하십시오.

새 동의 속성은 기본적으로 프로필의 대시보드에 표시되지 않습니다. 따라서 다음 위치로 이동해야 합니다 **[!UICONTROL 속성]** 프로필의 세부 정보 페이지에 있는 탭으로서, 예상대로 수집되었는지 확인할 수 있습니다. 에서 안내서 참조 [프로필 대시보드](../../../../profile/ui/profile-dashboard.md) 필요에 따라 대시보드를 사용자 지정하는 방법을 알아봅니다.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## 다음 단계

이 안내서에서는 Adobe 표준을 사용하여 고객 동의 데이터를 처리하고 이러한 속성을 고객 프로필에 나타내도록 플랫폼 작업을 구성하는 방법을 다룹니다. 이제 세그먼트 자격 및 기타 다운스트림 사용 사례에서 결정 요소로 고객 동의 환경 설정을 통합할 수 있습니다.

Experience Platform의 개인 정보 보호 관련 기능에 대한 자세한 내용은 [플랫폼의 거버넌스, 개인정보 보호 및 보안](../../overview.md).
