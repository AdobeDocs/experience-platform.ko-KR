---
title: 대상 활성화 워크플로에서의 ID 처리
description: 대상 유형에 따라 활성화 워크플로에서 ID 내보내기가 처리되는 방법을 알아봅니다
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 대상 활성화 워크플로에서의 ID 처리

이 페이지에서는 ID를 다양한 대상 유형으로 내보내는 방법의 세부 사항을 설명하고 대상에 따라 내보낼 수 있는 ID를 찾는 방법을 설명합니다.

>[!TIP]
>
> ID, ID 네임스페이스 및 ID 관련 용어 정의에 대한 자세한 내용은 [ID 서비스 개요](/help/identity-service/home.md)를 참조하십시오.

[catalog](/help/destinations/catalog/overview.md)의 각 대상이 약간 다르므로 모든 대상에 대해 한 가지 크기의 모든 설정이 없습니다. 그러나 아래 섹션에 설명된 대로 대상 및 ID 요구 사항 설정을 안내하는 몇 가지 패턴이 있습니다.

## 파일 기반 대상 {#file-based}

[파일 기반 대상](/help/destinations/destination-types.md#file-based)(예: [!DNL Amazon S3], SFTP, 대부분의 이메일 마케팅 대상 등 [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud])의 경우 이러한 대상 대부분에서 ID 설정이 열려 있으므로 일괄 활성화 워크플로의 [특성 선택](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) 단계에서 ID를 선택할 필요가 없습니다.

파일 내보내기에 ID를 추가하도록 선택한 경우 내보내기에서 [ID 네임스페이스](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer)의 단일 ID만 선택할 수 있습니다. 내보낼 ID를 선택하면 [필수 특성](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) 및 [중복 제거 키](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys)(으)로 자동으로 선택됩니다.

![필수 특성 및 중복 제거 키로 선택된 ID입니다.](/help/destinations/assets/how-destinations-work/selected-identity.png)

임시 해결 방법으로, ID가 속성으로 Experience Platform에 수집된 경우 내보내기에 더 많은 ID를 추가할 수 있습니다. ID 네임스페이스 `Phone_E.164`과(와) 함께 내보내기를 위해 XDM 특성 이메일 주소를 선택한 아래 예를 참조하십시오.

![내보내기를 위해 선택한 전자 메일 주소 특성의 예입니다.](/help/destinations/assets/how-destinations-work/email-selected.png)

## ID 맵에서 ID 내보내기와 ID XDM 속성으로 내보내기 - 차이점 {#identity-map-or-attribute}

내보낸 레코드 수는 ID 맵에서 ID를 내보내도록 선택했는지 또는 Experience Platform에 속성으로 수집된 ID를 내보내도록 선택했는지에 따라 다를 수 있습니다. [병합 정책](/help/profile/merge-policies/overview.md)은(는) ID 맵에서 ID를 선택할 때 내보내는 레코드 수에서도 중요한 역할을 합니다.

예를 들어, 두 개의 서로 다른 데이터 세트에서 다음 프로필 조각이 단일 고객 프로필에 병합된다고 가정해 보겠습니다.

**프로필 조각 하나**

| ID 맵 | 이름 | 성 | 이메일 속성 |
|---------|----------|---------|--------|
| email1, 충성도 ID1 | John | Do | 이메일 1 |


**프로필 조각 2**

| ID 맵 | 이름 | 성 | 이메일 속성 |
|---------|----------|---------|--------|
| email2, 충성도 ID1 | John | Do | 이메일 2 |

병합된 프로필은 다음과 같습니다.

| ID 맵 | 이름 | 성 | 이메일 속성 |
|---------|----------|---------|--------|
| 이메일 1, 이메일 2, 충성도 ID1 | John | Do | 이메일 2 |

내보내기 동작은 내보낼 `IdentityMap: Email`을(를) 선택하는지 `xdm: personalEmail.address`을(를) 선택하는지에 따라 다릅니다.

고객이 `IdentityMap: Email`을(를) 활성화하면 내보낸 파일에 email1에 대한 레코드와 email2에 대한 레코드가 있습니다.

그러나 고객이 `xdm: personalEmail.address`을(를) 활성화하면 이메일 특성 필드에 email2만 포함되므로 email2만 레코드에 표시됩니다. 이러한 상황은 고객에 대한 파일에 있는 모든 이메일 주소 또는 고객에 대한 파일에 있는 가장 최근 이메일 주소에 활성화할 수 있는 다양한 사용 사례를 처리할 수 있습니다.

중요한 것은 내보내는 레코드 수가 선택한 병합 정책 및 내보내기에서 ID 또는 속성을 선택하는지 여부에 따라 달라진다는 것입니다.

## API 기반 스트리밍 대상 {#streaming-destinations}

[Destination SDK](/help/destinations/destination-sdk/overview.md)(예: [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze] 등)으로 빌드된 [API 기반 스트리밍 대상](/help/destinations/destination-types.md#streaming-destination)은(는) 내보내기용 특정 ID만 지원합니다. 각 대상으로 내보낼 수 있는 특정 ID에 대한 자세한 내용은 각 대상 설명서 페이지의 *지원되는 ID* 섹션을 참조하십시오(예: [!DNL Pinterest] 대상 페이지의 [지원되는 ID 섹션](/help/destinations/catalog/advertising/pinterest.md) 참조).

그러나 [개인 그래프](/help/profile/merge-policies/overview.md#id-stitching) 또는 특성의 데이터를 ID로 유연하게 사용할 수 있습니다. 즉, XDM 속성을 대상에 필요한 ID 필드에 매핑할 수 있습니다. XDM 특성 `personalEmail.address`이(가) 필수 [!DNL Pinterest] ID `pinterest_audience`에 매핑되는 [!DNL Pinterest] 대상에 대한 아래 예를 참조하십시오.

>[!TIP]
>
>소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 Experience Platform이 활성화 시 데이터를 자동으로 해시하도록 합니다. [스트리밍 대상 활성화 자습서](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation)에서 **[!UICONTROL 변환 적용]** 옵션에 대해 자세히 알아보십시오.

![Pinterest 대상의 ID 필드에 매핑된 전자 메일 주소 특성의 예입니다.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 서드파티 쿠키 통합에 의존하는 Advertising 대상 {#third-party-cookie-destinations}

타사 쿠키에 의존하는 Advertising 대상(예: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk])에서는 고객이 활성화 워크플로에서 ID를 선택할 필요가 없습니다. 이러한 대상의 경우 활성화 워크플로를 설정할 때 Experience Platform은 [[!UICONTROL Experience Cloud ID 서비스]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ko-KR)에서 생성한 ID 일치 테이블을 자동으로 조회하고 프로필에 사용할 수 있으며 대상에서 지원하는 모든 ID를 내보냅니다.

이러한 대상을 사용하려면 [!UICONTROL Experience Cloud ID 서비스] 또는 [!UICONTROL Experience Platform Web SDK]를 통해 ID 동기화를 수행해야 합니다.

[!UICONTROL Experience Platform Web SDK]를 사용 중이며 기존 [!UICONTROL Experience Cloud ID 서비스]가 페이지에서 구현되지 않은 경우 [데이터 스트림 구성 설명서](/help/datastreams/configure.md#create)에 설명된 대로 해당 웹 사이트의 데이터 스트림이 타사 ID 동기화를 허용하도록 활성화되어 있는지 확인해야 합니다.

위에 연결된 설명서에 설명된 대로 데이터 스트림을 구성할 때는 **[!UICONTROL 타사 ID 동기화]** 슬라이더가 활성화되어 있는지 확인해야 합니다. 대부분의 고객은 `container_id` 필드를 비워 둡니다(기본값: 0). 레거시 Audience Manager 구현에서 특정 컨테이너 ID를 사용한 경우에만 이 값을 변경하면 됩니다(하지만, 이는 대다수의 고객이 될 수 있음).

>[!NOTE]
>
>이러한 광고 대상의 대부분은 Audience Manager에서 지원됩니다(이러한 대상 유형은 Audience Manager에서 장치 기반 대상으로 알려져 있음). [Audience Manager에서 지원되는 모든 장치 기반 대상 목록](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=ko)을 참조하세요. 몇 개만 Experience Platform에 나열되어 있습니다. Experience Platform과 Audience Manager 간의 데이터 공유에 대한 자세한 내용은 [Experience Platform에서 Audience Manager으로 데이터 공유 활성화](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ko#enable-aep-to-aam-data)에 대한 섹션을 참조하십시오. 현재 더 많은 타사 쿠키 대상을 지원할 계획이 없습니다.

## Enterprise 대상 {#enterprise-destinations}

[Enterprise 대상](/help/destinations/destination-types.md#advanced-enterprise-destinations)([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API)은(는) Enterprise 통합 사용 사례를 위해 설계되었으므로 데이터 내보내기에 특정 ID가 필요하지 않습니다. 그러나 원하는 경우 ID를 XDM 속성이나 ID 맵에서 내보낼 수 있습니다. ID 맵에서 `personalEmail.address` XDM 특성과 ID `ECID` 및 `email_lc_sha256`(해시된 이메일 주소)을(를) 모두 포함하는 HTTP 대상으로 내보낸 데이터의 [예를 봅니다](/help/destinations/catalog/streaming/http-destination.md#exported-data).

## Personalization 대상 {#personalization-destinations}

[Personalization(또는 edge) 대상](/help/destinations/destination-types.md#edge-personalization-destinations)(예: Adobe Target, [!DNL Custom Personalization])은 통합이 프로필 조회이므로 활성화 워크플로에서 ID를 선택할 필요가 없습니다. 클라이언트([!DNL Target], [!DNL Web SDK] 또는 기타)가 [[!UICONTROL Edge]](/help/collection/home.md#edge)을(를) 쿼리하고 사이트 개인화에 필요한 프로필 정보를 가져옵니다.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 개별 대상에 대해 지원되거나 필요한 ID를 찾는 방법을 이해할 수 있습니다. 이제 각 대상 유형에 대해 ID 선택이 작동하는 방식도 알 수 있습니다.

다음으로 대상 유형에 대해 공통적인 [내보내기 설정](/help/destinations/how-destinations-work/destinations-configurations.md)을 읽을 수 있습니다. 대상 유형은 개발자가 개별 대상 수준에서 구성할 수 있으며 활성화 워크플로에서 사용자가 편집할 수 있습니다.

[카탈로그](/help/destinations/catalog/overview.md)에서 사용 가능한 모든 대상을 확인할 수도 있습니다.
