---
title: Marketo Measure Ultimate 대상
description: Marketo Measure Ultimate 대상에 데이터를 연결하고 활성화하는 방법에 대해 알아봅니다.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 47197b745bebb6564d912d9dc045593bc076ae2a
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---

# Marketo Measure Ultimate 대상 {#mmu-destination}

## 개요 {#overview}

Marketo Measure(이전 Bizible)는 마케터에게 매출을 증대시키고 투자 수익률을 극대화하는 데 가장 효과적인 마케팅 활동을 파악하는 데 도움이 됩니다. Marketo Measure은 채널 성과를 자동으로 추적 및 보고하는 마케팅 속성 솔루션으로, 가장 많은 고객 참여를 유도하는 채널에 대한 가시성을 제공하고 그에 따라 마케팅 지출을 최적화할 수 있습니다.

대상은 Adobe Experience Platform에서 Marketo Measure으로 B2B(Business-to-Business) 데이터 흐름을 활성화합니다. 이 카드는 Marketo Measure Ultimate 고객만 사용할 수 있습니다.

## 사용 사례 {#use-cases}

Marketo Measure 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다. 이 통합:

* 대기업의 복잡한 데이터 및 성능 보고 요구 사항을 충족합니다.
* 여러 CRM 및 마케팅 자동화 시스템을 사용하여 B2B 속성 보고를 활성화합니다.
* 서드파티 오프라인 터치포인트 데이터를 쉽게 가져올 수 있습니다.

## 전제 조건 {#prerequisites}

Marketo Measure 대상에 대한 다음 사전 요구 사항을 참조하십시오.

* Experience Platform 샌드박스 매핑은 관리자가 Marketo Measure 설정 페이지에서 완료해야 합니다. 샌드박스 매핑이 없으면 대상 저장에 연결하고 데이터를 활성화하기 위한 워크플로우를 완료할 수 없습니다.
* B2B XDM 클래스의 데이터 세트만 내보낼 수 있습니다(예: XDM 비즈니스 계정 및 XDM 비즈니스 영업 기회 클래스 참조). 지정된 데이터 소스에 대해 동일한 B2B XDM 클래스의 여러 데이터 세트를 가져올 수 없습니다.
* 각 데이터 세트는 Marketo Measure 대상에 대한 하나의 데이터 흐름에만 포함될 수 있습니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 데이터 세트 내보내기]** | 대상자 관심사나 자격에 따라 그룹화되거나 구조화되지 않은 원시 데이터 세트를 내보내는 경우 자세한 내용 [데이터 세트 내보내기](/help/destinations/destination-types.md#dataset-export-destinations). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 이 배치 대상은 2시간마다 Marketo Measure 플랫폼으로 파일을 내보냅니다. 자세한 내용 [데이터 세트 내보내기 예약](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 섹션에 나열된 필드를 채웁니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

![Marketo Measure 대상에 대한 대상에 연결 워크플로우입니다.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 데이터 세트 내보내기 {#export-datasets}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 데이터 세트 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [데이터 세트 내보내기](/help/destinations/ui/export-datasets.md) 이 대상으로 데이터 세트를 내보내는 방법에 대한 자세한 지침은 튜토리얼을 참조하십시오.

## 데이터 내보내기 유효성 검사 {#exported-data}

성공적인 데이터 세트 내보내기의 유효성을 검사하기 위해 데이터 세트가 성공적으로 [Snowflake 데이터 웨어하우스](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html).

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).
