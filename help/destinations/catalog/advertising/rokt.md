---
title: Rokt
description: Adobe Experience Platform 대상자를 Rokt에 연결하여 더 스마트한 타기팅, 억제 및 개인화를 통해 캠페인 성과를 높이는 방법을 알아봅니다.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---


# [!DNL Rokt] 연결 {#rokt-destination}

## 개요 {#overview}

[[!DNL Rokt]](https://www.rokt.com)은(는) AI 기반의 실시간 의사 결정을 사용하여 전자 메일의 값을 잠금 해제하여 각 트랜잭션 순간™을 더욱 관련성 있게 만듭니다. 개인화된 경험을 제공하고 광고주와 고의적인 고객을 연결합니다. [!DNL Adobe Experience Platform]명의 대상자를 [!DNL Rokt]에 연결하여 보다 스마트한 타기팅, 억제 및 개인화를 통해 캠페인 성과를 높이십시오. 낭비되는 비용을 줄이면서 적절한 시간에 적절한 고객에게 도달합니다.

>[!IMPORTANT]
>
>대상 커넥터 및 문서 페이지는 [!DNL Rokt] 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청이 있으면 [!DNL Rokt] 계정 관리자에게 문의하거나 `support@rokt.com`에 문의하세요.

## 사용 사례 {#use-cases}

다음 사용 사례에서는 [!DNL Experience Platform] 고객이 [!DNL Rokt] 대상을 사용할 수 있는 방법을 보여 줍니다.

### 사용 사례 #1: 재타겟팅 {#use-case-1}

사이트 또는 앱을 방문했지만 전환하지 않은 고의적인 고객을 다시 참여시킵니다. 특정 제품 범주를 검색하거나 체크아웃 흐름을 중단한 사용자를 포함하여 [!DNL Experience Platform]에서 대상을 작성합니다. 그런 다음 해당 대상을 [!DNL Rokt]에 푸시하여 파트너 사이트에서 구매 시점에 개인화된 오퍼를 제공합니다. [!DNL Rokt]은(는) 고객이 다른 곳에서 구매를 완료한 후 즉시 트랜잭션 시간 내에 작동합니다. 재타겟팅된 대상은 구매 의도가 정점에 있을 때 도달하므로 기존 디스플레이 재타겟팅보다 높은 전환율을 유도합니다.

### 사용 사례 #2: 제외 목록 {#use-case-2}

특정 [!DNL Rokt]개의 오퍼를 받지 않아야 하는 대상을 억제하여 낭비되는 비용과 관련 없는 경험을 방지합니다. 일반적인 억제 사용 사례에는 최근 변환기, 활성 프로모션의 충성도 멤버 또는 마케팅을 옵트아웃한 사용자가 제외됩니다. 예를 들어 지난 30일 동안 구매한 고객은 제외하십시오. [!DNL Experience Platform]에서 [!DNL Rokt]&#x200B;(으)로 실시간으로 이러한 비표시 대상을 동기화합니다. 따라서 캠페인이 순-신규 또는 재참여 가능한 사용자에게 초점을 맞추게 됩니다. 이를 통해 ROI가 향상되고 고객 환경이 보호됩니다.

## 전제 조건 {#prerequisites}

[!DNL Adobe Experience Platform]에서 [!DNL Rokt] 대상을 설정하기 전에 **[!DNL Rokt]계정 관리자에서 다음 자격 증명을 가져와야 합니다**:

* **API 키**: [대상 연결 인증](#authenticate)할 때 이 키를 **[!UICONTROL Username]**(으)로 사용합니다.
* **API 암호**: [대상 연결 인증](#authenticate)할 때 이 암호를 **[!UICONTROL Password]**(으)로 사용합니다.

[!DNL Rokt] 계정 관리자가 설정 전에 [!DNL Rokt] 플랫폼에서 이러한 자격 증명을 프로비저닝합니다. 아직 받지 못한 경우 계정 관리자에게 문의하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Rokt]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 일반 텍스트 이메일 주소 | 권장. [!DNL Rokt]에서 프로필 일치에 사용됩니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소가 모두 지원됩니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| 전화 | 일반 텍스트 전화 번호 | [!DNL Rokt]에서 프로필 일치에 사용됩니다. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 지원됩니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| GAID | [!DNL Google] Advertising ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 [!DNL Apple] ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| aepProfileId | [!DNL Adobe Experience Platform] 프로필 ID | 프로필 ID(`xdm:_id`)를 대체 식별자로 매핑합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | [!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md)을(를) 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 예 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 [!DNL Experience Platform]&#x200B;(으)로 사용자 지정 업로드 대상 [가져옴](/help/segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> [!DNL Adobe Journey Optimizer]과(와) 같은 다른 [!DNL Experience Platform] 앱에서 생성된 대상, </li><li> 등. </li></ul> |

{style="table-layout:auto"}

대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필 기반. 마케팅 캠페인에 대한 특정 사용자 그룹을 타겟팅할 때 사용합니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | [!DNL Rokt] 대상에 사용된 식별자(이메일, 전화, 모바일 광고 ID 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상 평가를 기반으로 [!DNL Experience Platform]에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 [!DNL Rokt]&#x200B;(으)로 보냅니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](/help/destinations/ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL Connect to destination]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL Username]**: [!DNL Rokt] 계정 관리자가 제공한 API 키입니다.
* **[!UICONTROL Password]**: [!DNL Rokt] 계정 관리자가 제공한 API 암호입니다.

  ![계정 세부 정보, 인증 필드 및 대상 세부 정보가 채워진 [!DNL Experience Platform]의 [!DNL Rokt] 대상 구성 화면입니다.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 이름(예: &quot;[!DNL Rokt] - 대상 재타겟팅&quot;).
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](/help/destinations/ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

[!DNL Rokt] 대상은 [!DNL Experience Platform]에서 [!DNL Rokt] ID 필드로의 ID 네임스페이스 매핑을 지원합니다. 대상자를 성공적으로 활성화하려면 하나 이상의 ID를 매핑해야 합니다. 권장되는 매핑은 아래 표에 나와 있습니다.

| 소스 필드 | 대상 필드 | 고려 사항 |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | 권장 |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | 권장 |
| `IdentityMap: Phone` | `Identity: phone` | 선택 사항입니다 |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | 선택 사항입니다 |
| `IdentityMap: GAID` | `Identity: gaid` | 선택 사항입니다 |
| `IdentityMap: IDFA` | `Identity: idfa` | 선택 사항입니다 |
| `xdm: _id` | `Identity: aepProfileId` | 선택 사항입니다 |

{style="table-layout:auto"}

다음은 전체 매핑의 예입니다.

![원본 및 대상 ID 필드가 구성된 [!DNL Experience Platform]에서 [!DNL Rokt] 대상 활성화 워크플로의 매핑 단계입니다.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>[!DNL Rokt]에서 일치율을 최대화하려면 하나 이상의 전자 메일 기반 ID 매핑(`email` 또는 `emailSha256`)을 사용하는 것이 좋습니다.

### 대상자 일정 구성 {#audience-schedule}

매핑 단계를 완료한 후 선택한 각 대상에 대한 대상 일정을 구성합니다. 대상 동기화를 시작해야 할 시기에 대한 **[!UICONTROL Start date]**&#x200B;과(와) **[!UICONTROL Mapping ID]**([!DNL Rokt] 내에서 이 대상을 식별하는 데 사용되는 레이블)을(를) 제공하십시오. [!DNL Experience Platform] 대상 이름 또는 사용자 및 [!DNL Rokt] 계정 관리자가 대상을 식별하는 데 도움이 되는 모든 설명 문자열을 사용할 수 있습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

* [[!DNL Rokt] 개발자 설명서](https://docs.rokt.com)
* [Adobe Experience Platform 대상 개요](/help/destinations/home.md)
