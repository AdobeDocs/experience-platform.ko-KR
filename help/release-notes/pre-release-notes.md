---
title: Experience Platform 프리릴리스 노트
description: Adobe Experience Platform의 최신 릴리스 정보 미리보기.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9cf809f8fd6e424b4dcd800c3d554e4eb0e337dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 33%

---

# Adobe Experience Platform 프리릴리스 노트

>[!IMPORTANT]
>
>이 문서는 이번 달 릴리스 정보의 **미리 보기**&#x200B;로 작성되었습니다. 릴리스 항목은 변경될 수 있으며 최종 릴리스에서 추가 또는 제거될 수 있습니다.

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 날짜: 2025년 10월**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [경고](#alerts)
- [대상](#destinations)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL 경고] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며, 원하는 경우 UI 자체 또는 이메일 알림을 통해 알림 메시지를 수신할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 실패율 경고 | 대상에 대한 새 경고가 추가되었습니다. **대상 실패율이 임계값을 초과합니다**. 이 경고는 데이터 활성화 중 실패한 레코드 수가 허용된 임계값을 초과하는 경우 사용자에게 알려주므로 활성화 문제에 신속하게 대응할 수 있습니다. |

{style="table-layout:auto"}

경고에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../observability/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [!DNL AdForm] | 이 대상을 사용하여 Adobe Real-Time CDP ID(ECID) 및 [!DNL AdForm]의 ID Fusion을 기반으로 활성화할 수 있도록 [!DNL AdForm]&#x200B;(으)로 Experience Cloud 대상을 보냅니다. [!DNL AdForm]의 ID Fusion은 ECID(Experience Cloud ID)를 기반으로 자사 대상을 활성화할 수 있는 ID 확인 서비스입니다. |
| `Amazon Ads` | `firstName`, `lastName`, `street`, `city`, `state`, `zip` 및 `country`과(와) 같은 추가 개인 식별자 지원을 추가했습니다. 이러한 필드를 타겟 ID로 매핑하면 대상자 일치율을 향상시킬 수 있습니다. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL AES256] 대상에서 [!DNL Amazon S3] 서버측 암호화 지원 | [!DNL Amazon S3] 대상이 이제 [!DNL AES256] 서버측 암호화를 지원하므로 내보낸 데이터에 대해 향상된 보안을 제공합니다. [!DNL Amazon S3] 대상 연결을 설정하거나 업데이트할 때 이 암호화 방법을 구성하면 산업 표준 [!DNL AES256] 암호화 알고리즘을 사용하여 데이터를 사용하지 않고 암호화할 수 있습니다. 자세한 내용은 [[!DNL Amazon] 설명서](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html)를 참조하십시오. |
| [대상 수준 모니터링을 지원하는 몇 가지 새로운 대상](../dataflows/ui/monitor-destinations.md#audience-level-view) | 이제 다음 대상이 대상자 수준 모니터링을 지원합니다. <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] 계정 참여</li><li>[!DNL The Trade Desk]</li></ul> |
| 데이터 세트 내보내기 보호 문제 해결 | 데이터 세트 내보내기 가드레일에 대한 수정 사항이 구현되었습니다. 이전에는 타임스탬프 열이 포함되어 있지만 XDM 경험 이벤트 스키마를 기반으로 하는 _not_&#x200B;인 일부 데이터 세트가 경험 이벤트 데이터 세트로 잘못 처리되어 내보내기가 365일 전환 확인 기간으로 제한되었습니다. 문서화된 365일 전환 확인 가드레일은 이제 경험 이벤트 데이터 세트에만 적용됩니다. XDM 경험 이벤트 스키마 이외의 스키마를 사용하는 데이터 세트는 이제 100억 개의 레코드 가드레일이 제어합니다. 일부 고객은 365일 전환 확인 기간에 잘못 포함된 데이터 세트에 대한 내보내기 횟수가 증가할 수 있습니다. 이를 통해 긴 전환 확인 기간이 있는 예측 워크플로우에 대한 데이터 세트를 내보낼 수 있습니다. 자세한 내용은 [데이터 집합 내보내기 보호](../destinations/guardrails.md#dataset-exports)를 참조하십시오. |
| 엔터프라이즈 대상에 대한 대상 수준 보고 개선 | 엔터프라이즈 대상에 대한 대상 수준 보고 논리가 개선되었습니다. 이 릴리스 이후 고객은 선택한 대상과 관련된 대상만 포함하는 더 정확한 대상 보고 번호를 볼 수 있습니다. 이 모니터링 조정을 통해 데이터 흐름에 매핑된 대상자만 보고에 포함되므로 실제 데이터 활성화에 대한 보다 명확한 통찰력을 얻을 수 있습니다. 활성화 중인 데이터 양에는 영향을 주지 않습니다. 보고 정확도를 개선하기 위한 모니터링 개선 사항입니다. |

자세한 내용은 [대상 개요](../destinations/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 세분화 모니터링 | 스트리밍 세그멘테이션을 위한 실시간 모니터링은 샌드박스, 데이터 세트 및 대상 수준에서 평가 속도, 지연 시간 및 데이터 품질 지표에 대한 투명성을 제공합니다. 이를 통해 데이터 엔지니어는 용량 위반 및 수집 문제를 식별하는 데 도움이 되는 사전 예방적 경고 및 실행 가능한 인사이트를 얻을 수 있습니다. 모니터링 지표에는 평가 비율, P95 수집 지연은 물론 수신, 평가, 실패 및 건너뛴 기록이 포함됩니다. 데이터 세트별 보기 및 대상별 보기 기능은 자격을 부여하거나 자격을 박탈한 순 신규 프로필에 대한 포괄적인 가시성을 제공합니다. |

자세한 내용은 [[!DNL Segmentation Service] 개요](../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| 충성도 데이터의 [!BADGE Beta]{type=Informative} [!DNL Talon.one] 소스 | [!DNL Talon.One] 소스를 사용하여 일괄 처리 및 스트리밍 충성도 데이터를 Experience Platform으로 수집합니다. 커넥터는 획득한 포인트, 상환된 포인트, 만료된 포인트 및 계층 데이터를 포함하여 프로필 데이터, 거래 데이터 및 로열티 데이터의 스트리밍을 지원합니다. |

**업데이트된 원본**

| 소스 | 설명 |
| --- | --- |
| [!DNL Google Ads] 소스의 일반 가용성(API 전용) | [!DNL Google Ads] 소스의 API 버전이 이제 일반 공급 상태입니다. API 설명서에 최신 버전이 이제 `v21`이고 Experience Platform이 모든 버전 v19 이상을 지원함을 반영하여 업데이트했습니다. UI 버전은 베타 상태로 유지되며 일회성 수집만 지원합니다. 증분 데이터 수집을 사용하려면 API 경로를 사용합니다. |
| [!DNL Azure Event Hubs] 가상 네트워크 지원 | 이제 Adobe은 Azure Event Hubs에 대한 가상 네트워크 연결을 명시적으로 지원하므로 공개 네트워크가 아닌 개인 네트워크를 통해 데이터를 전송할 수 있습니다. 허용 목록에 추가하다 고객은 Experience Platform VNet를 통해 Azure 백본을 통해 개인적으로 이벤트 트래픽을 라우팅하여 데이터 수집 워크플로우에 대한 향상된 보안을 제공할 수 있습니다. |

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.
