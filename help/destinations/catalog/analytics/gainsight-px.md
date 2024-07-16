---
title: Gainsight PX 연결
description: Gainsight PX 대상을 사용하여 Gainsight PX 플랫폼으로 세그멘테이션 정보를 보냅니다.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Gainsight PX 연결 {#gainsight-px}

## 개요 {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/)은(는) 제품 팀이 사용자가 제품을 사용하는 방법을 이해하고 피드백을 수집하며 제품 연습과 같은 인앱 참여를 만들어 사용자 온보딩 및 제품 채택을 유도할 수 있도록 하는 제품 경험 플랫폼입니다.

>[!IMPORTANT]
>
>대상 커넥터 및 설명서 페이지는 *Gainsight PX* 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청이 있으면 *`pxsupport@gainsight.com`*(으)로 직접 문의하십시오.

## 사용 사례 {#use-cases}

*Gainsight PX* 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 인앱 참여 타기팅 {#targeting-in-app-engagements}

SaaS 회사는 Gainsight PX에서 작성한 애플리케이션 내 안내서를 통해 고객의 참여를 유도하려고 합니다. 이 참여를 받을 대상이 Adobe Experience Platform에 구축되었습니다. Gainsight PX 대상은 대상을 받고 Gainsight PX 환경 내에서 사용할 수 있도록 합니다.

## 전제 조건 {#prerequisites}

* [!DNL Gainsight] 지원 팀에 연락하여 구독에 대한 외부 세그먼트 기능 활성화를 요청하세요.
* [회사 세부 정보 페이지](https://app.aptrinsic.com/settings/subscription) 하단에 있는 **[!UICONTROL 새 암호 생성]** 단추를 사용하여 PX 구독에 대한 OAuth 암호 값을 생성합니다.
  ![새 암호 생성 단추를 표시하는 Gainsight PX의 회사 세부 정보 화면](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## 지원되는 ID {#supported-identities}

Gainsight PX는 아래 표에 설명된 ID 활성화를 지원합니다. [ID](../../../identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 |
|---|----|
| ID 식별 | Gainsight PX 및 Adobe Experience Platform에서 사용자를 고유하게 식별하는 공통 사용자 식별자 |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---|---|---|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---|---|---|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | [!DNL Gainsight PX] 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

![인증 스크린샷](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL 암호]**: [[!DNL Gainsight PX]에 로그인하는 데 사용되는 암호](https://app.aptrinsic.com)
* **[!UICONTROL 클라이언트 ID]**: [회사 세부 정보 페이지의 Gainsight PX 구독 ID](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL 클라이언트 암호]**: [!DNL Gainsight PX] UI의 [회사 세부 정보 페이지](https://app.aptrinsic.com/settings/subscription)의 맨 아래에 생성된 OAuth 암호입니다.
* **[!UICONTROL 사용자 이름]**: [[!DNL Gainsight PX]](https://app.aptrinsic.com) UI에 로그인하는 데 사용되는 전자 메일

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![이름 및 설명 필드를 채우는 방법을 보여 주는 Experience Platform 사용자 인터페이스의 대상 세부 정보 화면](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### ID 매핑 {#map}

이 대상은 프로필 속성 및 ID 네임스페이스의 매핑을 지원합니다. 대상 매핑은 항상 **[!UICONTROL IDENTIFY_ID]** ID 네임스페이스여야 합니다.

매핑을 구성하는 방법을 더 잘 이해하려면 아래 예를 참조하십시오.

#### 프로필 속성 매핑 {#map-profile-attribute}

아래 표시된 예에서 소스 필드는 IDENTIFY_ID 대상 네임스페이스에 매핑되는 XDM 프로필 속성입니다.

![원본 및 대상 값을 선택하는 방법을 보여 주는 ID 네임스페이스 예제 매핑 화면](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### ID 네임스페이스 매핑 {#map-identity-namespace}

아래 예제에서 소스 필드는 **[!UICONTROL IDENTIFY_ID]** 대상 네임스페이스에 매핑되는 ID 네임스페이스(**[!UICONTROL ECID]**)입니다.

![원본 및 대상 값을 선택하는 방법을 보여 주는 특성 예제 매핑 화면](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

세그멘테이션 데이터는 Experience Platform에서 Gainsight PX로 스트리밍됩니다.

세그먼트 메타데이터는 [!DNL Gainsight PX] UI의 세그먼트 화면에 표시됩니다.

![외부 세그먼트를 표시하는 Gainsight PX의 세그먼트 목록 화면입니다.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

세그먼트 멤버십 정보는 [!DNL Gainsight PX] UI의 대상 탐색기 화면에 있는 세그먼트 탭에 표시됩니다.

![Gainsight PX의 Audience Explorer 화면에서 사용자의 연결된 세그먼트를 표시합니다.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
