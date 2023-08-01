---
title: Snap Inc 연결
description: Snapchat Ads Platform에 연결하고 Experience Platform에서 대상을 내보내는 방법에 대해 알아봅니다.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 1%

---

# Snap Inc 연결

## 개요 {#overview}

[Snapchat 광고](https://forbusiness.snapchat.com/) 규모나 업종에 상관없이 모든 비즈니스를 위해 만들어집니다. 전체 화면 디지털 광고를 통해 Snapchatters의 일상적인 대화에 참여하여 비즈니스에 가장 중요한 사용자들의 행동을 고취하십시오.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 *스냅* 팀. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. *dev-support@snap.com*

## 사용 사례 {#use-cases}

이 대상을 사용하면 마케터는 Experience Platform에서 만든 사용자 대상을 Snapchat 광고로 가져와 이 대상을 사용하여 광고를 타깃팅할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

이 대상을 사용하려면 Snapchat 광고 계정이 있어야 합니다. 만드는 방법에 대한 자세한 내용은 이 설명서 를 참조하십시오.

[Snapchat Advertising 시작하기](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 제한 사항 {#limitations}

* Snap Inc는 특정 대상 세그먼트에 대해 여러 ID를 지원하지 않습니다. 세그먼트를 활성화할 때 하나의 ID만 매핑하십시오.
* Snap Inc는 세그먼트 이름 변경을 지원하지 않습니다. 세그먼트의 이름을 변경하려면 세그먼트를 비활성화하고 이름을 바꾼 다음 활성화해야 합니다.
* 대상 세그먼트 멤버에 대한 보존 기간을 정의할 수 없습니다. 모든 멤버는 라이프타임 유지가 있으며 제거될 때까지 대상자에 포함됩니다.

## 지원되는 ID {#supported-identities}

다음 *스냅* 대상 은 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

에 전송된 모든 식별자 *스냅* 대상은 SHA-256 형식으로 해시해야 합니다. 일반 텍스트 식별자를 대상으로 보내기 전에 해시하려면 **[!UICONTROL 변환 적용]** 대상에 대한 대상 식별자를 매핑할 때 선택합니다.

>[!WARNING]
> 
> 해시되지 않은 식별자는 Snap Inc 대상에서 허용되지 않으며 이러한 식별자를 보내면 오류가 발생할 수 있습니다.


>[!IMPORTANT]
> 
> Snap Inc 대상은 여러 ID를 지원하지 않습니다. ID를 하나만 선택하십시오.

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| Email Address | SHA-256 해시된 이메일 주소 | 이메일 주소를 대상 ID 필드에 매핑 *emailAddress*. |
| 전화 번호 | SHA-256 해시된 전화 번호 | 이메일 주소를 대상 ID 필드에 매핑 *전화번호*. |
| GAID | SHA-256 해시된 Google 광고 ID | Google 광고 ID를 대상 ID 필드에 매핑 *gaid*. |
| IDFA | SHA-256 해시된 Apple 광고 ID | Apple 광고 ID를 대상 ID 필드에 매핑 *idfa*. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. *대상* 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Snap Inc에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

### 대상에 인증 {#authenticate}

대상에 인증하려면 다음 단계를 수행합니다.

1. 다음 찾기 *스냅* Adobe Experience Platform 대상 카탈로그의 대상 및 선택 **설정**.
2. 선택 **[!UICONTROL 대상에 연결]**. 다음 화면으로 리디렉션됩니다.
   ![인증 화면 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Snapchat 자격 증명을 입력하고 다음을 선택합니다. **로그인**.
4. Adobe Experience Platform에서 액세스할 수 있는 Snapchat 데이터가 표시됩니다. 선택 **계속** 연결 프로세스를 진행합니다.

![인증 화면 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

계속을 선택한 후 Adobe Experience Platform으로 다시 리디렉션될 때까지 기다립니다.

### 대상 세부 정보 입력 {#destination-details}

![대상 세부 사항](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

대상에 대한 세부 정보를 구성하려면 필수 필드를 입력한 다음 을(를) 선택합니다 **[!UICONTROL 다음]**.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 대상자를 가져오려는 광고 계정과 연결된 광고 계정 ID입니다. 이 항목을 찾는 방법에 대한 자세한 내용은 다음을 참조하십시오. [snapchat 비즈니스 도움말 센터에 대한 이 설명서](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>잘못되거나 잘못된 Snapchat 광고 계정 ID를 입력하면 대상자 활성화에 실패하게 됩니다. 적절한 광고 계정 ID를 입력했는지 다시 확인하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상자를 활성화한 후 *스냅* 대상: 스냅 광고 관리자의 대상자를 볼 수 있습니다. [**대상** 섹션](https://businesshelp.snapchat.com/s/article/audience-sharing). 이 섹션으로 이동하려면 다음 단계를 수행합니다.

1. 에 로그인합니다 [스냅 광고 관리자](https://ads.snapchat.com/)
2. 선택 **대상** 을 클릭합니다. Adobe Experience Platform에서 활성화한 대상이 대상 라이브러리의 대상 라이브러리에 표시됩니다.

![대상자](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Adobe 대상자가 Snap Inc.에 처음 활성화되면 처음에는 빈 대상자로 표시됩니다. 이는 Adobe Experience Platform이 대상자를 평가할 때까지 멤버 데이터를 Snap Inc로 내보내지 않기 때문입니다. Experience Platform에서 대상을 평가하는 방법에 대한 자세한 내용은 [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
