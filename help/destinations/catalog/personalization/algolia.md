---
title: 알골리아
description: 이 커넥터를 사용하여 Algolia에 대한 대상자를 활성화하여 개인화하고 검색 및 권장 사항 전반에서 사용할 수 있습니다. 그런 다음 Algolia 사용자 프로필 소스 커넥터를 사용하여 프로필을 Real-Time CDP으로 가져와 리치 대상자를 구축할 수 있습니다.
source-git-commit: 2205ba48a6c17b8f34c4796c1777bfc53a6a7fe5
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 3%

---


# [!DNL Algolia] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>[!DNL Algolia] 대상 커넥터 및 문서 페이지는 Algolia Integration Services 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 [adobe-algolia-solutions@algolia.com](adobe-algolia-solutions@algolia.com)로 문의하십시오.

[!DNL Algolia] 대상 연결을 사용하여 Adobe Experience Platform 대상자를 Algolia로 보내 개인화된 검색 및 추천을 받으십시오. [!DNL Algolia] 대상 커넥터를 사용하려면 먼저 [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) 원본 커넥터를 설정해야 합니다. 소스 커넥터 설정 자습서 중에 Algolia 사용자 토큰 ID를 만듭니다. 이 ID는 대상 커넥터를 구성할 때 매핑에 필요합니다.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL Algolia] 대상 연결 및 데이터 흐름을 만드는 단계를 제공합니다.

![Algolia 대상이 있는 대상 카탈로그입니다.](../../assets/catalog/personalization/algolia/catalog.png)

## 사용 사례 {#use-cases}

[!DNL Algolia] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### Personalization 일관성 {#personalization-consistency}

이 대상 커넥터를 사용하여 홈페이지에서 검색까지 사이트 간에 일관된 개인화를 제공할 수 있습니다.

예를 들어 마케터는 Algolia를 비롯한 여러 사용자 데이터 소스에서 Adobe Experience Platform에 풍부한 대상을 구축할 수 있습니다. [!DNL Algolia] 대상 커넥터를 사용하여 타깃팅 전략에 대한 대상을 공유할 수 있으므로 캠페인 개인화 및 전환이 향상됩니다.

이 사용 사례를 구현하려면 [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) 원본 및 [!DNL Algolia] 대상 커넥터를 모두 사용해야 합니다.

먼저 기존 [!DNL Algolia] 사용자 프로필을 Adobe Experience Platform Real-Time CDP 및 기타 소스로 가져와서 소스 커넥터를 사용하여 풍부한 대상을 만들 수 있습니다. 마케터는 검색 및 권장 사항 개인화를 위해 Algolia로 보낼 수 있는 프로필 데이터를 사용하여 대상을 만듭니다.

그런 다음 해당 [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) 소스 커넥터를 사용하여 고객 프로필을 다시 Real-Time CDP으로 수집 및 보완합니다.

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>* 대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

## 지원되는 ID {#supported-identities}

[!DNL Algolia]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---------|---------|----------|
| userId | [!DNL Algolia] 사용자 토큰 | `AlgoliaUserToken` 원본 ID를 [!DNL Algolia] 플랫폼의 `userToken`에 매핑하려면 이 대상 ID를 선택하십시오. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|---------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!DNL Audience export]** | [!DNL Algolia] 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 데이터 집합 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL 응용 프로그램 ID]**: [!DNL Algolia] 응용 프로그램 ID는 [!DNL Algolia] 계정에 할당된 고유 식별자입니다.
* **[!UICONTROL API 키]**: [!DNL Algolia] API 키는 [!DNL Algolia]의 검색 및 인덱싱 서비스에 대한 API 요청을 인증하고 권한을 부여하는 데 사용되는 자격 증명입니다.

이러한 자격 증명에 대한 자세한 내용은 [!DNL Algolia] [인증 설명서](https://www.algolia.com/doc/tools/cli/get-started/authentication/)를 참조하세요.

![새 계정](../../assets/catalog/personalization/algolia/connection.png)

### 대상 세부 정보 입력

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 대상의 용도에 대한 간략한 설명입니다.
* **[!UICONTROL 지역]**: 옵션은 **US** 또는 **EU**&#x200B;입니다. 고객 데이터가 저장되는 영역을 선택합니다.


![계정 세부 정보](../../assets/catalog/personalization/algolia/account.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* ID를 내보내려면 ID 그래프 보기 [액세스 제어 권한](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home#permissions)이 필요합니다.

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)를 참조하십시오.

### 속성 및 ID 매핑 {#mapping-attributes-identities}

[!UICONTROL 매핑 단계] 동안 AlgoliaUserToken 소스 ID를 userId 대상 ID에 매핑해야 합니다.

![매핑 완료](../../assets/catalog/personalization/algolia/mapping-complete.png)

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 사용자 프로필로 내보냈는지 확인하려면 [!DNL Algolia] 대시보드를 확인하고 **[!UICONTROL 고급 Personalization]**(으)로 이동한 다음 **[!UICONTROL 사용자 검사기]**&#x200B;를 클릭하십시오. 내보낸 Adobe Experience Platform 대상자와 연결된 사용자 프로필을 찾아 User Inspector에서 검색합니다. 대상 ID는 세그먼트 섹션에 표시됩니다.

![Algolia User Inspector](../../assets/catalog/personalization/algolia/verify-segment-user-profile.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 다음 [!DNL Algolia] 설명서를 참조하십시오.

* [고급 Personalization란 무엇입니까?](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/)
* [사용자 프로필](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/concepts/user-profiles/)
* [규칙 컨텍스트가 있는 세그먼트 사용자](https://www.algolia.com/doc/guides/personalization/advanced-personalization/implement/guides/segment-users-with-rule-contexts/#assign-a-segment-context-at-query-time)

## 다음 단계 {#next-steps}

이 자습서를 따라 Experience Platform에서 [!DNL Algolia] 응용 프로그램으로 대상을 내보내는 데이터 흐름을 만들었습니다. [!DNL Algolia] 플랫폼에 대한 자세한 내용은 [Algolia 설명서](https://www.algolia.com/doc/)를 참조하십시오.