---
title: Adobe Experience Platform 릴리스 노트 2026년 2월
description: Adobe Experience Platform의 2026년 2월 릴리스 정보.
exl-id: a677026f-e07e-4e69-bd6c-5ddcb13e8e38
source-git-commit: a11c00c218ffbbd5618616f401613a604c35859a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 46%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2026년 2월 17일 수요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [경고](#alerts)
- [대상](#destinations)
- [소스](#sources)
- [경험 데이터 모델 (XDM)](#xdm)

## 경고 {#alerts}

Experience Platform을 통해 다양한 Experience Platform 활동에 대한 이벤트 기반 알림을 구독할 수 있습니다. Experience Platform 사용자 인터페이스의 [!UICONTROL Alerts] 탭을 통해 다양한 경고 규칙을 구독할 수 있으며 UI 자체 내에서 또는 이메일 알림을 통해 경고 메시지를 수신하도록 선택할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 고객 응대 경고에 대한 [!DNL Slack] 통합 | 이제 [!DNL Slack]에게 고객 응대 경고를 제공할 수 있습니다. [단계별 자습서](../../observability/alerts/slack-integration.md)에 따라 [!DNL Slack] 통합을 설정하고 [!DNL Slack] 작업 영역에서 바로 경고 알림을 받을 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [[!DNL Observability Insights] 개요](../../observability/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 대상 플랫폼과의 사전 빌드된 통합을 통해 Experience Platform의 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [[!DNL Snowflake] 일괄 처리](../../destinations/catalog/warehouses/snowflake-batch.md) 일반적으로 사용 가능 | 이제 [!DNL Snowflake] 일괄 처리 대상을 일반적으로 사용할 수 있습니다. 이제 전 세계 Real-Time CDP 고객은 이 커넥터를 사용하여 데이터를 물리적으로 복사할 필요 없이 Snowflake 계정에 데이터를 활성화할 수 있습니다. 제한된 릴리스의 모든 제한이 해제되었습니다(미국 전용 고객의 경우 사용 가능, 기본 병합 정책에 속하는 대상에 대해서만 지원). |

{style="table-layout:auto"}

**수정 사항 및 개선 사항**

| 변수 이름이 아니라, 필터링된 보고서의 머리글로 잘못 표시하는 | 설명 |
| --- | --- |
| 활성화 실패율 초과 경고 | 활성화 실패율 초과 대상 경보는 이제 경보를 평가하고 전송할 때 사용자가 구성한 임계값을 올바르게 사용합니다. 이전에는 구성한 비율에 관계없이 실패율 1%로 경고가 트리거되었습니다. 이 경고에 대한 자세한 내용은 [표준 경고 규칙](../../observability/alerts/rules.md#destinations)을 참조하세요. |
| Google 고객 일치 제외된 ID 보고 | Google Customer Match 대상에 대해 부풀려진 제외된 프로필 카운트가 표시되던 생략된 레코드 계산 로직의 버그를 수정했습니다. 활성화 및 내보내기 동작은 영향을 받지 않았습니다. 보고된 수치만 올바르지 않습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 또는 업데이트된 소스**

| 소스 | 설명 |
| --- | --- |
| [!DNL Databricks] 원본 커넥터의 Unity 카탈로그 지원 | 이제 [!DNL Databricks] 원본 커넥터가 Unity 카탈로그를 지원합니다. 소스 연결을 구성할 때 Unity 카탈로그를 사용하는 방법에 대해 알아보려면 업데이트된 [[!DNL Databricks]](../../sources/connectors/databases/databricks.md) 설명서를 읽어 보십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.


## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Experience Platform에 가져온 데이터에 대한 공통 구조와 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 데이터 세트가 있는 스키마에 대한 제한된 편집 | 변경 내용을 중단시키는 편집 작업은 스키마에 대한 데이터 세트가 존재하면 이제 제한됩니다. 데이터 세트가 연결되면 더 이상 필드의 이름 변경 또는 삭제, 필드 데이터 유형 또는 형식 변경, ID 설명자 수정, 기존 필드를 제거하기 위한 관련 필드 관리 또는 할당된 클래스 변경을 수행할 수 없습니다. 추가 변경 사항 및 필드 사용 중단 기능은 계속 지원됩니다. |

자세한 내용은 [XDM 개요](../../xdm/home.md)를 참조하십시오.
