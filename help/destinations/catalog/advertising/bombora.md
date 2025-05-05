---
title: 봄보라 접속
description: 계정 대상자를 기반으로 대상자 타겟팅, 개인화 및 억제에 대한 Bombora 캠페인에 대한 프로필을 활성화합니다.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko#rtcdp-editions newtab=true"
badgeB2P: label="B2P 버전" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ko#rtcdp-editions newtab=true"
source-git-commit: 026d8e4c2bcea407d2a750e66b11766b1114b758
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 3%

---


# 봄보라 접속 {#bombora}

>[!AVAILABILITY]
>
>Real-Time Customer Data Platform의 [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) 에디션을 구매하는 회사는 Bombora 대상에 대한 계정 대상을 활성화할 수 있습니다.

[계정 대상자](/help/segmentation/types/account-audiences.md)를 기반으로 대상자 타겟팅, 개인화 및 억제에 대한 Bombora 캠페인에 대한 프로필을 활성화합니다.

## 사용 사례 {#use-case}

Bombora 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### DSP 통합 {#dsp-integration}

B2B 마케터는 Real-time CDP에서 계정 목록을 만들어 제품에 대한 높은 의도를 보이는 회사를 식별한 다음 이 대상을 사용하여 Bombora에서 이 목록을 활성화할 수 있습니다.

Bombora와 DSP의 통합을 통해 Bombora 데이터를 사용하여 타깃팅된 광고 캠페인을 실행할 수 있습니다. 이렇게 하면 광고 지출이 전환 가능성이 가장 높은 회사에 집중되도록 할 수 있습니다.

### Account-Based Marketing {#abm}

B2B 마케터는 CRM 및 마케팅 신호를 기반으로 계정 목록을 만들 수 있습니다. 그런 다음 이 대상을 사용하여 Bombora에서 이 목록을 활성화할 수 있습니다. 여기서 ABM 인식 컨트롤은 이러한 회사의 의사 결정자를 타겟팅하는 데 도움이 됩니다.

### 다중 채널 계정 기반 마케팅 활성화 {#multi-channel-abm}

B2B 마케터는 Real-time CDP에서 계정 목록을 만들어 높은 의도를 가진 회사를 식별할 수 있습니다. 그런 다음 이 대상을 사용하여 Bombora에서 목록을 활성화하여 여러 채널에서 타겟팅된 캠페인을 실행할 수 있습니다.

유료 소셜 미디어에서는 [!DNL LinkedIn] 및 [!DNL Facebook]과(와) 같은 플랫폼의 대상 계정에서 전문가에게 개인화된 광고를 제공할 수 있습니다. 기본 광고 플랫폼을 사용하면 콘텐츠가 관련 의사 결정자에게 도달하는지 확인할 수 있습니다.

캠페인을 고급 TV로 확장하여 주요 계정에 광고를 게재할 수도 있습니다.

이 다중 채널 접근 방식은 플랫폼 간에 일관된 메시지를 보장하여 참여 및 전환율을 극대화합니다.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 지원되는 ID {#supported-identities}

Bombora에는 아래 표에 설명된 대상 ID의 매핑이 필요합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 |
|---|---|
| `primaryId` | 통합이 제대로 작동하려면 Bombora에 이 대상 ID의 매핑이 필요합니다. 모든 소스 필드를 이 ID에 매핑할 수 있습니다. 이 매핑은 필수 사항이지만 Bombora로 데이터를 엑스포트하지 않습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-and-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | [!DNL Bombora] 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

계정 대상을 Bombora로 내보내려면 다음 정보가 필요합니다.

1. 봄보라 계정입니다.
2. Bombora **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]**.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

![전달자 토큰 추가](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL 클라이언트 ID]**: [!DNL Bombora] 클라이언트 ID를 입력하십시오.
* **[!UICONTROL 클라이언트 암호]**: [!DNL Bombora] 클라이언트 암호를 입력하십시오.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 연결에 대한 정보 추가](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

이제 Bombora 내에서 대상을 활성화할 준비가 되었습니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 계정 대상을 활성화하는 방법에 대한 지침은 [계정 대상 활성화](/help/destinations/ui/activate-account-audiences.md)를 참조하십시오.

### 필수 매핑 {#mapping}

Bombora 대상을 사용하려면 성공적인 데이터 활성화를 위해 다음 매핑을 구성해야 합니다.



| 소스 필드 | 대상 필드 | 설명 |
|---------|----------|---------|
| 모든 값 | `Identity: primaryId` | 이 매핑은 Experience Platform이 Bombora에 대한 연결을 설정하는 데 필수입니다. 이 값은 Bombora로 익스포트되지 않지만 대상 구성에 필요합니다. 소스 필드에 대한 속성을 선택할 수 있습니다. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora는 웹 사이트 또는 도메인 주소를 사용하여 계정 목록을 생성합니다. |

![필수 매핑 추가](../..//assets/catalog/advertising/bombora/mappings.png)


## 추가 참고 사항 및 중요한 설명선 {#additional-notes}

동일한 이름의 계정 대상이 이전에 Bombora에 대해 활성화된 경우 다른 데이터 흐름을 통해 Bombora 대상에 대해 다시 활성화하려고 하면 오류가 표시됩니다.

