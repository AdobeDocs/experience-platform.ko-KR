---
title: Demandbase 사용자 연결
description: 이 대상을 사용하여 마케팅 및 판매의 다른 다운스트림 사용 사례에서 대상을 활성화하고 Demandbase 타사 데이터로 대상자를 보강합니다.
source-git-commit: df2cb1edbf998082fca961e6d9bb567a1ad3b7e6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 3%

---


# Demandbase 사용자 연결 {#demandbase-people}

대상자 타겟팅, 개인화 및 제외를 위해 Demandbase 캠페인에 대한 프로필을 활성화합니다.

>[!IMPORTANT]
>
>[계정 대상을 활성화](../../ui/activate-account-audiences.md)해야 하는 B2B 사용 사례의 경우 대신 [Demandbase](demandbase.md) 대상 커넥터를 사용하십시오.

## 활용 사례 {#use-case}

마케터는 Adobe Real-Time CDP을 사용하여 자사 연락처의 사람 목록을 만들고 Demandbase에서 이를 활성화하여 수요 측 플랫폼(DSP) 및 LinkedIn과 같은 기타 채널에서 최적화되고 조정된 참여를 할 수 있습니다.

이 접근 방식을 통해 마케터는 자체 CRM 또는 마케팅 자동화 시스템에서 가져온 알려진 개인에 대한 캠페인 비용의 우선 순위를 지정하여 마케팅 활동이 고가치 잠재 고객에 집중되도록 할 수 있습니다.

활성화된 Demandbase는 광고 게재를 최적화하고 타깃팅 전략을 개선하여 참여, 도달 및 전환율을 극대화함으로써 궁극적으로 캠페인 효율성을 향상시킵니다.

## 지원되는 ID {#supported-identities}

[!DNL Demandbase People] 연결은 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 일반 텍스트 이메일 주소 | [!DNL Demandbase People] 연결에서는 일반 텍스트 전자 메일 주소만 지원됩니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-and-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|--------------|-----------|---------------------------|
| 내보내기 유형 | 대상자 내보내기 | *Demandbase* 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 빈도 | 스트리밍 | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

대상을 Demandbase로 내보내려면 다음이 필요합니다.

1. Demandbase 계정입니다.
2. Demandbase API 토큰. Demandbase에서 사용자와 함께 API 토큰을 생성할 수 있습니다. 토큰을 생성하려면 Demandbase 계정에 로그인한 후 [내 프로필 > API 토큰](https://web.demandbase.com/o/ad/at)&#x200B;(으)로 이동합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

![전달자 토큰 추가](../../assets/catalog/advertising/demandbase-people/bearer-token.png)

* **[!UICONTROL 전달자 토큰]**: 대상에 인증하려면 전달자 토큰을 입력하십시오. 토큰을 얻는 방법에 대한 자세한 내용은 [필수 구성 요소](#prerequisites)를 참조하십시오.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 연결에 대한 정보 추가](../../assets/catalog/advertising/demandbase-people/name-and-description.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

이제 Demandbase People 내에서 대상을 활성화할 준비가 되었습니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 추가 참고 사항 및 중요한 설명선 {#additional-notes}

* **Demandbase API 보호**: 대상을 Demandbase로 내보냈고 Experience Platform에서 내보내기가 성공했지만 일부 데이터가 Demandbase에 도달하지 못한 경우 Demandbase 측에서 API 제한이 발생할 수 있습니다. 자세한 내용은 해당 담당자에게 문의하십시오.
* **목록 삭제**: 사람 목록은 고유하므로 이미 사용 중인 이름으로 새 목록을 다시 만들 수 없습니다. 목록에서 사용자를 제거하면 더 이상 사용할 수 없지만 삭제되지는 않습니다.
* **활성화 시간**: Demandbase에서 데이터를 로드하면 익일 처리가 적용됩니다.
* **대상 이름 지정**: 같은 이름의 계정 대상이 Demandbase에 대해 이전에 활성화되었다면 다른 데이터 흐름을 통해 Demandbase 대상에 대해 다시 활성화할 수 없습니다.
