---
title: 대상 분석 대상
description: 고객이 Customer Journey Analytics에서 사용할 수 있는 대상을 봅니다.
badgeLimitedAvailability: label="제한된 가용성" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---

# 대상 분석 대상

[!UICONTROL Audience Analysis] 대상을 사용하면 Adobe Experience Platform 대상 데이터를 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko)에 보강할 수 있습니다. 보강된 결과 데이터에 포함할 대상을 선택할 수 있습니다. 그런 다음 대상 자격은 [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) 보고에서 차원으로 사용할 수 있습니다.

>[!AVAILABILITY]
>
>이 대상은 제한된 테스트 단계에 있습니다. 이 대상을 사용하는 데 관심이 있는 경우 Adobe 계정 팀에 문의하십시오.

## 전제 조건

이 대상을 사용하기 전에 다음 항목이 필요합니다.

* Audience Analysis 대상을 사용하도록 프로비저닝되어야 합니다. 이 대상을 사용하도록 아직 프로비저닝되지 않은 경우 Adobe 계정 팀에 문의하십시오.
* Customer Journey Analytics을 사용하려면 프로비저닝되어야 합니다.
* Adobe Experience Platform에서 만든 대상자가 한 명 이상 있어야 합니다.

## 지원되는 ID

Audience Analysis는 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요. 일반적으로 ECID(Experience Cloud ID)가 사용됩니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 자세한 내용은 [ECID](/help/identity-service/features/ecid.md)에서 다음 문서를 참조하십시오. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 지원되는 대상자

이 대상을 사용할 때 지원되는 대상자 유형은 다음과 같습니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | Audience Analysis 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 새 대상 구성

>[!IMPORTANT]
> 
>대상을 만들려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상을 만들려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 대상 세부 정보

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL Name]**: 대상 이름입니다.
* **[!UICONTROL Description]**: 대상 설명입니다.
* **[!UICONTROL Datastream ID]**: 자격 있는 대상으로 보강할 데이터 스트림 ID입니다. 이 ID는 [데이터 스트림 관리자](/help/datastreams/overview.md)에서 얻을 수 있습니다.
* **[!UICONTROL Integration alias]**: 통합 별칭입니다.

### 경고

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

* **[!UICONTROL Activation Skipped Rate Exceed]**: 활성화 건너뛰기 비율이 임계값을 초과하는 경우 알림을 받습니다.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

### 거버넌스 정책 및 시행 작업

이 선택적 섹션을 통해 데이터 거버넌스 정책을 정의하고 대상자를 보내고 활성화할 때 사용된 데이터가 준수되는지 확인할 수 있습니다.

대상에 대해 원하는 마케팅 작업 선택을 마치면 **[!UICONTROL Create]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

대상이 만들어지면 대상에 대해 원하는 대상을 활성화할 수 있습니다.

1. 생성된 대상에 아직 없는 경우 **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**(으)로 이동하여 다시 찾을 수 있습니다.
1. **[!UICONTROL Activate audiences]**&#x200B;를 선택합니다.
1. 자격을 분석할 대상을 선택합니다. 완료되면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.
1. 대상 구성 및 대상 설정을 검토한 다음 **[!UICONTROL Finish]**&#x200B;을(를) 선택하십시오.

**[!UICONTROL Activate audiences]** 페이지로 다시 이동하여 나중에 분석할 대상을 더 추가할 수 있습니다. 대상자가 활성화되면 제거할 수 없습니다.
