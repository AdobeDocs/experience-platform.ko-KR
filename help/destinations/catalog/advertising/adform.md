---
title: Adform
description: Adform은 프로그램 방식의 미디어 구매 및 판매 솔루션을 제공하는 선도적인 공급업체입니다. Adform을 Adobe Experience Platform에 연결하면 ECID(Experience Cloud ID)를 기반으로 하는 Adform을 통해 자사 대상을 활성화할 수 있습니다.
source-git-commit: 823b2142366ac218ad93279de5f31d60bdc07bbf
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 3%

---


# Adform 연결 {#adform}

## 개요 {#overview}

Adform은 프로그램 방식의 미디어 구매 및 판매 솔루션을 제공하는 선도적인 공급업체입니다. Adform을 Adobe Experience Platform에 연결하면 ECID(Experience Cloud ID)를 기반으로 하는 Adform을 통해 자사 대상을 활성화할 수 있습니다.

>[!IMPORTANT]
>
>대상 커넥터 및 설명서 페이지는 Adform 팀에서 만들고 관리합니다. 문의 사항이나 업데이트 요청이 있으면 `support@adform.com`(으)로 직접 연락하십시오.

## 사용 사례 {#use-cases}

Adobe Form 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### Adobe Real-Time CDP 대상자 활성화 {#use-case-1}

이 대상을 사용하여 Experience Cloud ID(ECID) 및 Adform의 ID Fusion을 기반으로 활성화를 위해 Adobe Real-Time CDP 대상을 Adform으로 보냅니다. Adform의 ID Fusion은 Experience Cloud ID(ECID)를 기반으로 자사 대상을 활성화할 수 있는 Adform의 ID 확인 서비스입니다.

일반적인 사례는 ECID(Experience Cloud ID)를 기반으로 웹 사이트 또는 앱에 대한 웹 사이트 방문자를 재타겟팅하는 것입니다. 이제 즉시 사용 가능한 [이벤트 스트리밍](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) 또는 [클라이언트측](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/analytics/adform) Adform 확장을 통해 ECID(Experience Cloud ID)를 Adform으로 전송하기만 하면 됩니다. 이후 활성화를 위해 Adform 대상을 통해 ECID(Experience Cloud ID)만을 기준으로 Adform과 대상을 공유할 수 있습니다.

## 전제 조건 {#prerequisites}

* 이 대상을 사용하려면 기존 Adform 고객이어야 합니다.
* Adform 대상자 기본 데이터 연결 자격 증명이 있어야 합니다.
   * Adform 대상자 기본 데이터 연결 자격 증명이 없는 경우 Adform 담당자에게 문의하십시오.
* 적절한 동기화를 위해 엔터티에서 Adobe 사이트 추적에 대해 [이벤트 스트리밍](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) 또는 [클라이언트측](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/analytics/adform) 연결이 있어야 합니다.
   * 엔티티에서 Adform 사이트 추적에 대한 이벤트 스트리밍 또는 클라이언트측 연결이 없는 경우 Adform 담당자에게 문의하십시오.
   * Adform은 [이벤트 스트리밍](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) 및 [클라이언트측](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/analytics/adform)에 모두 Adobe Experience Cloud 확장을 제공합니다.


## 지원되는 ID {#supported-identities}

Adform은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 자세한 내용은 [ECID](/help/identity-service/features/ecid.md)에서 다음 문서를 참조하십시오. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | *YourDestination* 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 세그먼트의 모든 구성원(대상)을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

![대상에 인증](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL 계정 이름]**: 나중에 이 대상 연결을 식별할 수 있는 계정 이름을 입력하십시오.
* **[!UICONTROL S3 액세스 키 ID]**: Adform에서 제공한 S3 액세스 키를 입력하십시오.
* **[!UICONTROL S3 암호 액세스 키]**: Adform에서 제공한 S3 암호 액세스 키를 입력하십시오.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 세부 정보를 입력하십시오](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 공급자 이름]**: Adform에서 제공한 Adform 계정 이름입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

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