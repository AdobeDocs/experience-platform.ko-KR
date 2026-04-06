---
title: Adform
description: Adform은 프로그램 방식의 미디어 구매 및 판매 솔루션을 제공하는 선도적인 공급업체입니다. Adform을 Adobe Experience Platform에 연결하면 ECID(Experience Cloud ID)를 기반으로 하는 Adform을 통해 자사 대상을 활성화할 수 있습니다.
last-substantial-update: 2025-10-23T00:00:00Z
exl-id: b87fe57f-10e3-4c10-9156-f102244fbbe7
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 4%

---

# Adform 연결 {#adform}

## 개요 {#overview}

Adform은 프로그램 방식의 미디어 구매 및 판매 솔루션을 제공하는 선도적인 공급업체입니다. Adform을 [!DNL Adobe Experience Platform]에 연결하면 ECID(Experience Cloud ID)를 기반으로 하는 Adform을 통해 자사 대상을 활성화할 수 있습니다.

>[!IMPORTANT]
>
>대상 커넥터 및 설명서 페이지는 Adform 팀에서 만들고 관리합니다. 문의 사항이나 업데이트 요청이 있으면 `support@adform.com`(으)로 직접 문의하십시오.

## 사용 사례 {#use-cases}

Adform 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Adobe Experience Platform] 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### Adobe [!DNL Real-Time CDP] 대상 활성화 {#use-case-1}

이 대상을 사용하여 ECID(Experience Cloud ID) 및 Adform의 ID Fusion을 기반으로 활성화할 Adobe [!DNL Real-Time CDP] 대상을 Adform으로 보냅니다. Adform의 ID Fusion은 Experience Cloud ID(ECID)를 기반으로 자사 대상을 활성화하기 위한 Adform의 ID 확인 서비스입니다.

일반적인 사례는 ECID(Experience Cloud ID)를 기반으로 웹 사이트 또는 앱에 대한 웹 사이트 방문자를 재타겟팅하는 것입니다. 이제 즉시 사용 가능한 [이벤트 스트리밍](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) 또는 [클라이언트측](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/analytics/adform) Adform 확장을 통해 ECID(Experience Cloud ID)를 Adform으로 전송하기만 하면 됩니다. 이후 활성화를 위해 Adform 대상을 통해 ECID(Experience Cloud ID)만을 기준으로 Adform과 대상을 공유할 수 있습니다.

## 전제 조건 {#prerequisites}

* 이 대상을 사용하려면 기존 Adform 고객이어야 합니다.
* Adform 대상자 기본 데이터 연결 자격 증명이 있어야 합니다.
   * Adform 대상자 기본 데이터 연결 자격 증명이 없는 경우 Adform 담당자에게 문의하십시오.
* 적절한 동기화를 위해 엔터티에서 Adobe 사이트 추적에 대해 [이벤트 스트리밍](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) 또는 [클라이언트측](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/analytics/adform) 연결이 있어야 합니다.
   * 엔티티에서 Adform 사이트 추적에 대한 이벤트 스트리밍 또는 클라이언트측 연결이 없는 경우 Adform 담당자에게 문의하십시오.
   * Adform은 [!DNL Adobe Experience Cloud]이벤트 스트리밍[&#x200B; 및 &#x200B;](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking)클라이언트측[&#x200B; 모두에 대해 &#x200B;](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/analytics/adform) 확장을 제공합니다.


## 지원되는 ID {#supported-identities}

Adform은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;[!DNL Adobe Experience Cloud] ID&quot;, &quot;[!DNL Adobe Experience Platform] ID&quot; 별칭에서도 참조할 수 있습니다. 자세한 내용은 [ECID](/help/identity-service/features/ecid.md)에서 다음 문서를 참조하십시오. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 아니요 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> [!DNL Adobe Journey Optimizer]과(와) 같은 다른 Experience Platform 앱에서 생성된 대상, </li><li> 등. </li></ul> |

{style="table-layout:auto"}



대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}


## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Segment export]** | *YourDestination* 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 세그먼트의 모든 구성원(대상)을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL Batch]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL Connect to destination]**&#x200B;을(를) 선택하십시오.

![대상에 인증](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL Account name]**: 나중에 이 대상 연결을 식별할 수 있는 계정 이름을 입력하십시오.
* **[!UICONTROL S3 Access Key ID]**: Adform에서 제공한 S3 액세스 키를 입력합니다.
* **[!UICONTROL S3 Secret Access Key]**: Adform에서 제공한 S3 암호 액세스 키를 입력하십시오.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 세부 정보를 입력하십시오](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Provider Name]**: Adform에서 제공한 Adform 계정 이름입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

* **ECID**(Experience Cloud ID)

매핑 단계에서 [!DNL ECID] 대상 ID 매핑만 사용하십시오. 다른 ID 필드를 포함하지 마십시오. 이렇게 하면 활성화가 성공적으로 완료되지 않습니다.

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

대상 커넥터는 ECID ID만 대상으로 내보냅니다. 다른 ID는 내보내지지 않습니다. 데이터 내보내기가 성공했는지 확인하려면 Adobe Audience Base 계정에 로그인하여 대상을 사용할 수 있는지 확인하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

Adform Audience Base에 대한 자세한 내용은 [Adform Audience Base 설명서](https://www.adformhelp.com/hc/en-us/categories/9738365991697-Data-Management-Platform)를 참조하십시오.
