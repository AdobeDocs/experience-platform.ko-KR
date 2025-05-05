---
keywords: adform 통합; adform;
title: 인증되지 않은 재타겟팅을 위한 Adobe Form 통합
description: 이 Adobe Experience Platform 통합을 사용하면 ECID를 기반으로 사용자를 재타겟팅할 수 있습니다.
last-substantial-update: 2025-03-26T00:00:00Z
source-git-commit: 23da6e12b1f5bdc37240d7aa11a44e040b29e3f7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# [!DNL Adform] 확장 개요

[[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) 확장을 사용하면 Adobe Experience Platform에서 서버측 이벤트 전달을 사용할 수 있으므로 광고주, 미디어 에이전시 및 게시자가 데이터를 Adobe의 ID Fusion 시스템과 직접 동기화할 수 있습니다. 이 통합을 통해 기업은 여러 채널에서 대상자를 참여시킬 수 있으므로 캠페인 성과를 향상시킬 수 있으며 디지털 광고 전략을 구체화하고 광고 지출 효과를 극대화할 수 있는 맞춤형 솔루션을 제공합니다.

기존 클라이언트측 추적과 달리, 이 확장은 자사 ID, 특히 Adform과 동기화된 ECID(Experience Cloud ID)를 활용하여 타사 쿠키를 필요로 하지 않습니다. 이렇게 하면 클라이언트측 JavaScript 배포 없이 매끄러운 대상 재타겟팅을 수행할 수 있습니다.

이 안내서에서는 방문자를 원활하게 재타겟팅할 수 있도록 확장을 설치, 구성 및 배포하여 Adobe의 Edge Network을 통해 브랜드의 디지털 속성에서 Adform으로 이벤트를 전달하는 방법을 다룹니다.

## 오프사이트 리타기팅

오프사이트 재타겟팅을 통해 웹 사이트를 방문했지만 전환하지 않은 잠재적 고객을 다시 참여시킬 수 있습니다. Adform은 다양한 플랫폼에서 이러한 대상에게 도달하도록 지원하여 브랜드 입지를 강화하고 전환 기회를 늘립니다. 이 통합을 사용하여 다음을 수행할 수 있습니다.

* 서드파티 쿠키를 사용하지 않고 알 수 없는 방문자를 다시 참여시킵니다.
* 디지털 속성에 타사 쿠키 대체 식별자 또는 추가 태그를 사용하지 않고 ECID에서 직접 대상을 활성화합니다.

Adform을 사용하면 다음 작업을 수행할 수 있습니다.

* ECID에 표시된 자사 대상을 디지털 광고 캠페인용 주소 지정 가능한 ID로 쉽게 변환할 수 있습니다.
* ECID를 40개 이상의 바인딩 가능한 ID 솔루션에 연결하여 타깃팅된 대상에 대해 도달 범위, 빈도 및 성능을 최적화합니다.

### [!DNL Adform]&#x200B;(으)로 서버측 대상 활성화 {#server-side-activation}

기존 클라이언트측 ID 배포와 달리, 이 통합에서는 디지털 속성에 ID 공급업체의 솔루션을 배포할 필요가 없습니다. 대신 이미 Adform과 동기화된 ECID를 활용하여 서버측 대상 활성화를 활성화합니다. 주요 이점은 다음과 같습니다.

* **클라이언트측 JavaScript 배포가 없음**: 클라이언트측 방문자 인식 논리를 관리하거나 클라이언트측 ID를 해독하여 오래 지속되는 안정적인 버전으로 만들 필요가 없습니다.
* **원활한 대상 동기화**: ECID가 Adform의 내부 ID 그래프에 매핑되어 플랫폼 간에 효율적으로 재타겟팅할 수 있습니다.
* **도달 및 중복 제거 개선**: ID Fusion 그래프는 ECID를 여러 식별자에 연결하여 고품질 대상 일치를 보장합니다.

## 전제 조건 {#prerequisites}

Adform을 Adobe과 통합하기 전에 다음 전제 조건이 충족되는지 확인하십시오.

1. **Adobe Web SDK 설치**: 데이터 수집 및 이벤트 전달을 용이하게 하기 위해 Adobe Web SDK을 구현해야 합니다.

2. **CDP 또는 연결 SKU**: 원활한 클라이언트측 및 서버측 통신을 사용하려면 Adobe CDP(고객 데이터 플랫폼) Prime 또는 Ultimate SKU 또는 연결 SKU가 있어야 합니다.

3. **Adobe Experience Platform Edge Network 구성**:
   * Edge Network이 오프사이트 재타겟팅을 위해 실시간 이벤트 전달을 지원하도록 구성되어 있는지 확인합니다. 자세한 내용은 Adobe의 [이벤트 전달 시작 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/getting-started)를 참조하십시오.
   * 이 단계는 Adform의 서버측 끝점에 데이터를 효율적으로 전송하는 데 중요합니다.

이러한 필수 구성 요소가 준비되면 [!DNL Adform] 확장을 계속 구성하고 배포할 수 있습니다.

## [!DNL Adform] 확장 구성 {#configure-adform-extension}

[!DNL Adform] 확장을 구성하려면 아래 섹션에 설명된 단계를 수행합니다.

### 확장 설치 및 구성

이벤트 전달 UI에서 [!DNL Adform extension]&#x200B;(으)로 이동하고 필요한 값을 입력합니다.

| 입력 | 설명 |
| --- | --- |
| 추적 설정 ID | 이벤트 추적을 위해 Adform에서 제공하는 고유 식별자입니다. |
| 글로벌 도메인 | 성능을 최적화하고 지역 지연 문제를 방지하려면 `a1.adform.net`을(를) 사용하십시오. |

이러한 세부 정보를 입력한 후 구성을 저장합니다.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### 추적 매개 변수 정의

&quot;추적&quot; 작업은 기본 이벤트 규칙입니다. 미리 정의된 작업을 기반으로 트리거됩니다. 일반적으로 `page load.`에는 다음 매개 변수가 포함됩니다.

**필수 매개 변수:**

| 매개 변수 | 설명 |
| --- | --- |
| `Page Name` | 페이지 또는 사용자 작업을 식별합니다. |
| `User Agent` | 대상자 일치를 위한 정보를 캡처합니다. |
| `IP Address` | 정확한 타겟팅 및 재타겟팅에 중요합니다. |

**권장 매개 변수:**

| 매개 변수 | 설명 |
| --- | --- |
| `Page URL` | 페이지 또는 사용자 작업을 식별합니다. |
| `Referral URL` | 대상자 일치를 위한 정보를 캡처합니다. |
| `ECID` | 정확한 타겟팅 및 재타겟팅에 중요합니다. |
| `Source Domain` | 정확한 타겟팅 및 재타겟팅에 중요합니다. |

<!-- ![Tracking parameters for Adform]() -->

### 규칙 첨부

확장이 제대로 작동하려면 규칙에 첨부해야 합니다. 설정된 조건이 없으면 글로벌 규칙을 만들어 항상 실행되도록 합니다.

>[!NOTE]
>
>확장이 실행되지 않는 경우 Adobe Experience Platform 데이터 수집의 유효한 규칙에 연결되어 있는지 확인합니다.

<!-- ![Attach a rule to the Adform extension]() -->

## 유효성 검사 및 배포

확장이 올바르게 설치 및 구성되어 있고 다음을 포함하여 필요한 모든 데이터 요소가 매핑되어 있는지 확인합니다.
* [ECID](/help/identity-service/features/ecid.md)
* 페이지 이름
* 참조 URL
* 사용자 에이전트
* IP 주소

필수 필드를 모두 입력하고 테스트를 마치면 **빌드**&#x200B;를 선택하여 확장을 배포합니다.

## 다음 단계

이제 Adform이 Adobe의 서버측 기능과 어떻게 통합되는지 이해해야 하며 기존 인프라 내에서의 통합의 타당성을 평가할 수 있습니다. 자세한 내용은 [Adform의 공식 설명서](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud)를 참조하세요.