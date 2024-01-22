---
title: PubMatic Connect
description: PubMatic은 미래의 프로그램 방식의 디지털 마케팅 공급망을 제공하여 고객 가치를 극대화합니다. PubMatic Connect는 플랫폼 기술과 전용 서비스를 결합하여 인벤토리와 데이터를 패키지하고 처리하는 방법을 개선합니다.
last-substantial-update: 2023-12-14T00:00:00Z
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---


# PubMatic Connect 대상 {#pubmatic-connect}

## 개요 {#overview}

사용 [!DNL PubMatic Connect] 미래의 프로그래밍 방식 디지털 마케팅 공급망을 제공하여 고객 가치를 극대화합니다. [!DNL PubMatic Connect] 플랫폼 기술과 전용 서비스를 결합하여 인벤토리와 데이터를 패키징하고 처리하는 방법을 향상시킵니다.

이 대상을 사용하여 대상 데이터를 [!DNL PubMatic Connect] 플랫폼.

>[!IMPORTANT]
>
>대상 커넥터 및 설명서 페이지는 [!DNL PubMatic] 팀. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. `support@pubmatic.com`.

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL PubMatic Connect] destination은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 모바일, 웹 및 CTV 플랫폼에서 사용자 타겟팅 {#targeting}

게시자 또는 데이터 공급자는 Adobe Experience Platform의 대상자를 (으)로 전송하려고 합니다. [!DNL PubMatic Connect] 다양한 식별자를 사용하여 모바일, 웹 및 CTV 플랫폼의 사용자를 타깃팅합니다.

## 전제 조건 {#prerequisites}

다음 사용자에게 문의하십시오. [!DNL PubMatic] 계정 관리자가 계정이 올바르게 구성되어 있고 대상 세그먼트의 온보딩을 지원하는지 확인합니다. 또한 설정 중에 이 대상을 사용하고 지원을 제공하기 위해 모든 관련 세부 정보가 있는지 확인합니다.

## 지원되는 ID {#supported-identities}

[!DNL PubMatic Connect] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| 대상 ID | 설명 | 고려 사항 |
| --------------- | ------ | --- |
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
| --- | --- | --- |
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | PubMatic Connect 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 세그먼트의 모든 멤버(대상자)를 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되면 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
> 대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

![인증 방법](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL 전달자 토큰]**: 대상에 인증할 전달자 토큰을 입력합니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 세부 사항](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
- **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
- **[!UICONTROL 데이터 파트너 ID]**: 다음에 설정된 데이터 파트너 ID [!DNL PubMatic] 이 통합에 대해 설명합니다.
- **[!UICONTROL 기본 국가 코드]**: 프로필에 제공되지 않은 경우 모든 ID에 적용해야 하는 기본 국가 코드.
- **[!UICONTROL 계정 ID]**: 사용자 [!DNL PubMatic Connect] 계정 ID.
- **[!UICONTROL 계정 유형]**: 의 계정 유형 [!DNL PubMatic] 플랫폼 계정입니다. 다음 사용자에게 문의하십시오. [!DNL PubMatic] 계정 관리자 를 선택합니다. 사용 가능한 옵션은 다음과 같습니다.
   - [!UICONTROL 게시자]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL 구매자]

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
>
> - 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>
> - 내보내려면 _id_, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](../../assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

### 속성 및 ID 매핑 {#map}

소스 필드 선택:

- 식별자(일반적으로 IDFA 또는 사용자 지정 ID 네임스페이스와 같은 네임스페이스)를 선택합니다.

대상 필드 선택:

- 다음 사용자에게 문의하십시오. [!DNL PubMatic] 계정 관리자가 이 단계에서 올바른 UID 유형에 대한 정보를 가져옵니다.
- 다음 항목 선택 [!DNL PubMatic UID] 첫 번째 단계에서 선택한 식별자와 일치하는 번호를 입력합니다.

![속성 및 ID 매핑](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

다음 [!DNL PubMatic] UI를 통해 데이터가 올바르게 푸시되었는지, 세그먼트를 사용할 수 있는지 확인할 수 있습니다. 데이터가 로 푸시된 후 최대 24시간 소요될 수 있습니다. [!DNL PubMatic] 업데이트할 UI.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).
