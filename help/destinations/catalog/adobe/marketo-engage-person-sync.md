---
title: Marketo Engage 사용자 동기화
description: 개인 대상의 업데이트를 Marketo Engage의 해당 레코드로 스트리밍하려면 Marketo Engage 개인 동기화 커넥터를 사용하십시오.
last-substantial-update: 2025-01-14T00:00:00Z
badgeBeta: label="Beta" type="Informative"
source-git-commit: c5543997747daa336b0a5bb40c46aa720e8bcadd
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 3%

---


# Marketo Engage 사용자 동기화 연결 {#marketo-engage-person-sync}

>[!IMPORTANT]
>
>이 대상 커넥터는 베타 버전이며 일부 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오.

## 개요 {#overview}

개인 동기화 Marketo Engage 커넥터를 사용하여 개인 대상의 업데이트를 Marketo Engage 인스턴스의 해당 레코드로 스트리밍합니다.

>[!IMPORTANT]
> 
>프로필 업데이트 동기화 커넥터와 함께 만들기 모드에서 [Marketo V2 대상 동기화 커넥터](/help/destinations/catalog/adobe/marketo-engage.md)를 사용하면 안 됩니다

## 지원되는 ID 및 속성 {#support-identities-and-attributes}

### 지원되는 ID {#supported-identities}

| 대상 ID | 설명 |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 단일 사용자와 연결되므로 여러 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |

{style="table-layout:auto"}

### 지원되는 속성 {#supported-attributes}

Experience Platform의 속성을 조직이 Marketo에서 액세스할 수 있는 모든 속성에 매핑할 수 있습니다. Marketo에서는 [Describe API](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_6) 요청을 사용하여 조직에서 액세스할 수 있는 특성 필드를 검색할 수 있습니다.

## 지원되는 대상 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
| -------------------- | :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Segmentation Service | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ 덧신 | CSV 파일에서 Experience Platform으로 가져온 대상자입니다. |

## 내보내기 유형 및 빈도 {#export-type-and-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 내보내기 빈도 | 스트리밍 | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상 설정 {#set-up-destination}

>[!IMPORTANT]
>
>* 대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.

회사에서 여러 조직에 액세스할 수 있는 경우 Marketo Engage과 Real-Time CDP 모두에서 동일한 조직을 사용해야 합니다. 여기서 Marketo에 대상 커넥터를 설정합니다.  이미 대상을 구성한 경우 새 구성에 사용할 기존 Marketo 계정을 선택할 수 있습니다.  그렇지 않은 경우 대상 커넥터 프롬프트를 클릭하십시오. 그러면 원하는 대상의 이름, 설명 및 Marketo Munchkin ID를 설정할 수 있습니다.  Marketo 인스턴스의 Munchkin ID는 관리->Munchkin 메뉴에서 찾을 수 있습니다.

>[!IMPORTANT]
>
>대상을 설정하는 사용자는 Marketo 인스턴스 및 파티션에서 [사용자 편집](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) 권한이 있어야 합니다.

![대상에 연결](../../assets/catalog/adobe/marketo-engage-person-sync/connect-to-destination.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Munchkin ID]**: Munchkin ID는 특정 Marketo 인스턴스의 고유 식별자입니다.
* **[!UICONTROL Partition]**: 비즈니스 관심사별로 잠재 고객 레코드를 구분하는 데 사용되는 Marketo Engage의 개념입니다.
* **[!UICONTROL 첫 번째 검색 가능한 필드]**: 중복을 제거할 필드입니다. 필드는 입력의 각 리드 레코드에 있어야 합니다. 기본값은 이메일입니다
* **[!UICONTROL 첫 번째 검색 가능한 필드]**: 중복을 제거할 보조 필드입니다. 필드는 입력의 각 리드 레코드에 있어야 합니다. 선택 사항입니다

인스턴스를 선택한 후에는 구성을 통합할 Lead Partition도 선택해야 합니다. [리드 파티션](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions)은(는) 브랜드나 영업 지역과 같은 비즈니스 관심사별로 리드 레코드를 구분하는 데 사용되는 Marketo Engage의 개념입니다. Marketo 구독에 작업 공간 및 파티션 기능이 없거나 구독에 추가 파티션이 만들어지지 않은 경우 기본 파티션만 사용할 수 있습니다. 단일 구성은 구성된 파티션에 있는 리드 레코드만 업데이트할 수 있습니다.

>[!IMPORTANT]
> 
>대상자가 Marketo 대상에 처음 활성화되면 Marketo 대상을 활성화하기 전에 대상자에 이미 있던 프로필을 다시 채우는 데 *최대 24시간*&#x200B;이 걸릴 수 있습니다. 앞으로 프로필이 대상자에 추가될 때마다 Marketo에 즉시 추가됩니다.

### 중복 제거 필드 {#deduplication-fields}

Marketo engage에 업데이트를 보낼 때 선택한 파티션 및 하나 또는 두 개의 사용자 선택 필드를 기반으로 레코드가 선택됩니다. 대상이 북미 파티션으로 구성되고 이메일 주소 및 회사 이름이 중복 제거 필드로 구성된 경우 기존 레코드에 변경 사항을 적용하려면 세 필드가 모두 일치해야 합니다. 예:

* 대상은 북미 파티션으로 구성됩니다.
* Experience Platform에서 전자 메일이 <test@example.com>이고 회사 이름이 Example Inc.인 사람이 대상 대상자와 일치합니다.
* 해당 값을 가진 레코드가 Marketo의 북미 파티션에 이미 존재하지 않으면 새 잠재 고객 레코드가 만들어집니다

일치하는 잠재 고객 레코드가 없으면 새 레코드가 만들어집니다.

![대상 세부 정보](../../assets/catalog/adobe/marketo-engage-person-sync/destination-details.png)

## 대상자 활성화 {#activate-audiences}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

대상자 활성화 단계에서는 표시되는 개인 대상자 중에서 선택할 수 있습니다.

![대상자 활성화](../../assets/catalog/adobe/marketo-engage-person-sync/activate-audiences.png)

## 필드 매핑 {#field-mapping}

특정 개인 속성에 대한 변경 사항을 Marketo Engage으로 보내려면 필드를 Real-Time CDP 필드에서 Marketo 필드로 매핑해야 합니다.

![필드 매핑](../../assets/catalog/adobe/marketo-engage-person-sync/field-mapping.png)

Experience Platform 데이터 유형 및 Marketo 데이터 유형은 다음과 같은 방법으로 매핑할 수 있습니다.

| Experience Platform 데이터 유형 | Marketo 데이터 유형 |
| ----------------------------- | ------------------------------------ |
| 문자열 | 문자열, 텍스트 영역, Url, 전화, 이메일 |
| 열거형 | 문자열 |
| 날짜 | 날짜 |
| 날짜-시간 | 날짜/시간 |
| 정수 | 정수 |
| 짧음 | 정수 |
| Long | 부동 |
| 더블 | 통화, 부동 소수점, 백분율 |
| 부울 | 부울 |
| 배열 | 지원되지 않음 |
| 오브젝트 | 지원되지 않음 |
| 맵 | 지원되지 않음 |
| 바이트 | 지원되지 않음 |

{style="table-layout:auto"}

어떤 경우에는 통합에서 값이 이미 있는 필드에 대한 업데이트를 금지하면서 값이 없는 경우 필드 값을 설정하도록 허용하는 것이 좋습니다.  대상 커넥터가 Marketo Engage 인스턴스의 기존 값을 덮어쓰지 않도록 해야 하는 경우 Marketo 인스턴스의 관리->필드 관리 섹션에서 업데이트를 차단하고 Adobe Experience Platform 소스 유형을 토글하도록 필드를 구성할 수 있습니다.

![필드 업데이트 차단](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates.png)

![필드 업데이트 차단](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates-2.png)

## 데이터 사용 및 관리 {#data-usage-and-governance}

모든 Adobe Experience Platform 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. Adobe Experience Platform에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
