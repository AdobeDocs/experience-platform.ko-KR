---
title: 대상 분석 대상
description: 고객이 Customer Journey Analytics에 참여할 수 있는 대상을 봅니다.
badgeLimitedAvailability: label="제한된 가용성" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 3%

---

# 대상 분석 대상

다음 [!UICONTROL 대상 분석] 대상 을 사용하면 Adobe Experience Platform 대상 데이터를에 보강할 수 있습니다. [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=ko). 보강된 결과 데이터에 포함할 대상을 선택할 수 있습니다. 그런 다음 대상 자격은 의 차원으로 사용할 수 있습니다. [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) 보고.

>[!AVAILABILITY]
>
>이 대상은 제한된 테스트 단계에 있습니다. 이 대상을 사용하려면 Adobe 계정 팀에 문의하십시오.

## 전제 조건

이 대상을 사용하기 전에 다음 항목이 필요합니다.

* Audience Analysis 대상을 사용하도록 프로비저닝되어야 합니다. 이 대상을 사용하도록 아직 프로비저닝되지 않은 경우 Adobe 계정 팀에 문의하십시오.
* Customer Journey Analytics을 사용하려면 프로비저닝되어야 합니다.
* Adobe Experience Platform에서 만든 대상자가 한 명 이상 있어야 합니다.

## 지원되는 ID

Audience Analysis는 아래 표에 설명된 ID 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/features/namespaces.md). 일반적으로 Experience Cloud ID(ECID)가 사용됩니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 에 대한 다음 문서를 참조하십시오. [ECID](/help/identity-service/features/ecid.md) 추가 정보. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 지원되는 대상자

이 대상을 사용할 때 지원되는 대상자 유형은 다음과 같습니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ 덧신 | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | Audience Analysis 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 새 대상 구성

>[!IMPORTANT]
> 
>대상을 만들려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상을 만들려면 다음에 설명된 단계를 수행합니다 [대상 구성 자습서](../../ui/connect-destination.md).

### 대상 세부 정보

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 대상 이름입니다.
* **[!UICONTROL 설명]**: 대상 설명입니다.
* **[!UICONTROL 데이터 스트림 ID]**: 자격 있는 대상으로 보강할 데이터 스트림 ID입니다. 이 ID는 [데이터 스트림 관리자](/help/datastreams/overview.md).
* **[!UICONTROL 통합 별칭]**: 통합 별칭입니다.

### 경고

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

* **[!UICONTROL 활성화 건너뛰기 속도 초과]**: 활성화 건너뛰기 비율이 임계값을 초과하는 경우 알림을 받습니다.

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

### 거버넌스 정책 및 시행 작업

이 선택적 섹션을 통해 데이터 거버넌스 정책을 정의하고 대상자를 보내고 활성화할 때 사용된 데이터가 준수되는지 확인할 수 있습니다.

대상에 대해 원하는 마케팅 작업 선택을 마치면 을 선택합니다. **[!UICONTROL 만들기]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

대상이 만들어지면 대상에 대해 원하는 대상을 활성화할 수 있습니다.

1. 생성된 대상에 없는 경우 로 이동하여 다시 찾을 수 있습니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**.
1. 선택 **[!UICONTROL 대상자 활성화]**.
1. 자격을 분석할 대상을 선택합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 다음]**.
1. 대상 구성 및 대상 설정을 검토한 다음 을 선택합니다 **[!UICONTROL 완료]**.

로 다시 이동하여 나중에 분석할 대상을 더 추가할 수 있습니다. **[!UICONTROL 대상자 활성화]** 페이지를 가리키도록 업데이트하는 중입니다. 대상자가 활성화되면 제거할 수 없습니다.
