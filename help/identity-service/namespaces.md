---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;namespaces;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform ID 서비스
topic: overview
description: 'ID 네임스페이스는 ID 서비스의 구성 요소이며 ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어, "name@email.com" 값을 이메일 주소로 구분하거나 "443522"를 숫자 CRM ID로 구별합니다. '
translation-type: tm+mt
source-git-commit: dfb16c1808ac61e6c4f4d97c08ac3d1dcc8499a8
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 4%

---


# ID 네임스페이스 개요

Identity namespaces are a component of [[!DNL Identity Service]](./home.md) that serve as indicators of the context to which an identity relates. 예를 들어 &quot;name<span>@email.com&quot;의 값을 이메일 주소로 구분하거나 &quot;443522&quot;의 값을 숫자 CRM ID로 구별합니다.

## 시작하기

ID 네임스페이스를 사용하여 작업하려면 관련 다양한 Adobe Experience Platform 서비스에 대한 이해가 필요합니다. 네임스페이스로 작업하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../profile/home.md):여러 소스에서 수집한 데이터를 기반으로 통합된 고객 프로필을 실시간으로 제공합니다.
- [[!DNL Identity Service]](./home.md):다양한 디바이스와 시스템에 ID를 연결하여 개별 고객 및 고객의 행동을 명확하게 파악할 수 있습니다.
- [[!DNL Privacy Service]](../privacy-service/home.md):ID 네임스페이스는 네임스페이스와 관련하여 GDPR 요청을 수행할 수 있는 GDPR(General Data Protection Regulation)을 준수하는 데 사용됩니다.

## ID 네임스페이스 이해

정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 프로필 데이터 병합 시 프로필 데이터 간에 레코드 데이터를 일치시킬 때는 ID 값과 네임스페이스가 모두 일치해야 합니다. [!DNL Real-time Customer Profile]

예를 들어, 두 프로필 조각에 다른 기본 ID가 포함될 수 있지만 &quot;이메일&quot; 네임스페이스에 대해 동일한 값을 공유하므로 Platform은 이러한 조각들이 실제로 동일한 개인임을 확인하여 개별 ID 그래프에 데이터를 함께 가져올 수 있습니다.

![](images/identity-service-stitching.png)

### ID 유형

여러 가지 ID 유형으로 데이터를 식별할 수 있습니다. ID 유형은 ID 네임스페이스가 만들어질 때 지정되며 데이터가 ID 그래프로 유지되는지 여부와 데이터를 처리하는 방법에 대한 특별 지침을 제어합니다.

다음 ID 유형을 다음 내에서 사용할 수 있습니다 [!DNL Platform].

| ID 유형 | 설명 |
| --- | --- |
| 쿠키 | 이러한 ID는 확장을 위해 매우 중요하며 ID 그래프의 대부분을 구성합니다. 하지만, 자연은 시간이 지남에 따라 빠르게 부패하고 그들의 가치를 잃는다. 쿠키 삭제는 ID 그래프에서 특히 처리됩니다. |
| 크로스 디바이스 | 이것은 이것을 강한 사람 식별자로 간주하여 영원히 보존해야 [!DNL Identity Service] 한다는 것을 의미합니다. 로그인 ID, CRM ID, 충성도 ID 등이 있습니다. |
| 장치 | IDFA, GAID 및 기타 IOT ID를 포함합니다. 이것은 가정에서 사람들이 공유할 수 있다. |
| 이메일 | 이 유형의 ID에는 개인 식별 정보(PII)가 포함됩니다. 섬세하게 가치를 [!DNL Identity Service] 담을 수 있는 지표다. |
| 모바일 | 이 유형의 ID에는 PII가 포함됩니다. 섬세하게 가치를 [!DNL Identity Service] 담을 수 있는 지표다. |
| 일반 사용자 | 네임스페이스가 필요하지만 사람 클러스터와 연결되지 않은 식별자를 저장하는 데 사용됩니다. 그런 다음 이러한 식별자는 ID 그래프에서 필터링됩니다. 가능한 사용 사례에는 제품, 조직, 스토어 등과 관련된 데이터가 포함됩니다. (예: 제품 SKU) |
| 전화 | 이 유형의 ID에는 PII가 포함됩니다. 섬세하게 가치 [!DNL Identity Service] 를 담글 수 있는 지표다. |

### 표준 네임스페이스 {#standard}

Adobe Experience Platform은 모든 조직에서 사용할 수 있는 몇 가지 ID 네임스페이스를 제공합니다. 이러한 네임스페이스는 표준 네임스페이스라고 하며 [!DNL Identity Service] API나 [!DNL Platform] UI를 통해 볼 수 있습니다.

UI에서 표준 네임스페이스를 보려면 왼쪽 레일에서 **[!UICONTROL ID를]** 클릭한 다음 **[!UICONTROL 찾아보기]** 탭을 클릭합니다. 조직에서 액세스할 수 있는 모든 ID 네임스페이스가 표시되지만 &quot;[!UICONTROL 표준]&quot;을 &quot;[!UICONTROL 소유자]&quot;로 사용하는 네임스페이스는 Adobe에서 제공하는 표준네임스페이스입니다.

그런 다음 나열된 네임스페이스 중 하나를 클릭하여 세부 사항을 볼 수 있습니다.

![](./images/standard-namespace-detail.png)

## 조직의 네임스페이스 관리

조직의 데이터 및 사용 사례에 따라 사용자 정의 네임스페이스가 필요할 수 있습니다.

이러한 네임스페이스는 &quot;[!UICONTROL 사용자 지정]&quot;을 &quot;[!UICONTROL 소유자]&quot;로 갖는 네임스페이스로 UI에서 볼 수 있습니다. 사용자 정의 네임스페이스는 [!DNL Identity Service] API를 사용하거나 사용자 인터페이스를 통해 만들 수 있습니다.

UI를 사용하여 사용자 정의 네임스페이스를 만들려면 ID 네임스페이스 **[!UICONTROL 만들기를]**&#x200B;클릭한 다음 대화 상자를 완료한 다음 **[!UICONTROL 만들기를 클릭합니다]**.

정의한 네임스페이스는 조직에 비공개이며, 성공적으로 만들려면 고유한 &quot;[!UICONTROL ID 기호]&quot;(또는 API를 사용하는 경우 &quot;코드&quot;)가 필요합니다.

![](./images/create-identity-namespace.png)

표준 네임스페이스와 유사하게 **[!UICONTROL 검색]** 탭에서 사용자 지정 네임스페이스를 클릭하여 세부 사항을 볼 수 있지만, 사용자 지정 네임스페이스를 사용하면 세부 사항 영역에서 표시 이름 및 설명을 편집할 수도 있습니다.

>[!NOTE]
>
>네임스페이스가 만들어지면 이를 삭제할 수 없으며 API의 &quot;ID 기호&quot;(또는 &quot;코드&quot;) 및 &quot;유형&quot;을 변경할 수 없습니다.

## ID 데이터의 네임스페이스

ID용 네임스페이스를 제공하는 것은 ID 데이터를 제공하는 데 사용하는 방법에 따라 다릅니다. 데이터 ID 데이터 제공에 대한 자세한 내용은 [개요에서 ID 데이터](./home.md#supplying-identity-data-to-identity-service) 제공 섹션을 참조하십시오 [!DNL Identity Service] .
