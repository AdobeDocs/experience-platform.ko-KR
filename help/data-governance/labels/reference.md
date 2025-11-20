---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api;지원되는 데이터 사용 레이블;계약 레이블;id 레이블;중요 레이블
solution: Experience Platform
title: 데이터 사용 레이블 용어집
description: 이 문서에서는 현재 Adobe Experience Platform에서 지원하는 모든 데이터 사용 레이블에 대해 간략하게 설명합니다.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 7%

---

# 데이터 사용 레이블 용어 {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="레이블 유형"
>abstract="데이터 사용 레이블 카테고리가 몇 가지 있습니다. Adobe에서 정의한 레이블에는 약정 레이블, ID 레이블과 중요 레이블이 포함됩니다. 조직에서 정의한 레이블은 사용자 정의 레이블로 분류됩니다."
>text="See the data usage labels glossary for more information on these label types."

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 [거버넌스 정책](../policies/overview.md) 및 [액세스 제어 정책](../../access-control/abac/overview.md)에 따라 데이터 세트와 필드를 분류할 수 있습니다. Adobe Experience Platform은 데이터 분류를 시작하는 데 사용할 수 있는 몇 가지 핵심 데이터 사용 레이블 을 즉시 제공합니다.

이 문서에서는 현재 Experience Platform에서 제공하는 핵심 데이터 사용 레이블에 대해 간략하게 설명합니다.

## 약정 레이블 {#contract}

계약 &quot;C&quot; 레이블은 계약 의무가 있거나 조직의 데이터 거버넌스 정책과 관련된 데이터를 분류하는 데 사용됩니다.

| 레이블 | 정의 |
| --- | --- |
| [C1](#c1) | Adobe Experience Cloud에서는 개별 또는 장치 식별자를 포함하지 않고 집계된 형태로만 데이터를 내보낼 수 있습니다. |
| [C2](#c2) | 데이터를 서드파티로 내보낼 수 없습니다. |
| [C3](#c3) | 데이터는 직접 식별 가능한 정보와 결합하거나 사용할 수 없습니다. |
| [C4](#c4) | 온사이트 또는 크로스 사이트에서 광고 또는 콘텐츠를 타겟팅하는 데 데이터를 사용할 수 없습니다. |
| [C5](#c5) | Data cannot be used for interest-based, cross-site targeting of content or ads. |
| [C6](#c6) | 온사이트 광고 타겟팅에는 데이터를 사용할 수 없습니다. |
| [C7](#c7) | Data cannot be used for on-site targeting of content. |
| [C8](#c8) | Data cannot be used for measurement of your organization&#39;s websites or apps. |
| [C9](#c9) | Data cannot be used in data science workflows. |
| [C10](#c10) | 결합된 ID 활성화에는 데이터를 사용할 수 없습니다. |
| [C11](#c11) | 세그먼트 일치 파트너와 데이터를 공유할 수 없습니다. |
| [C12](#c12) | 어떤 방식으로도 데이터를 내보낼 수 없습니다. |

## ID 레이블 {#identity}

ID &quot;I&quot; 레이블은 특정 사용자를 식별하거나 연결할 수 있는 데이터를 분류하는 데 사용됩니다.

| 레이블 | 정의 |
| --- | --- |
| **I1** | 장치가 아닌 특정 사용자를 식별하거나 연결할 수 있는 직접 식별 가능한 데이터입니다. |
| **I2** | 특정 사용자를 식별하거나 연결하기 위해 다른 모든 데이터와 함께 사용할 수 있는 간접 식별 가능한 데이터입니다. |

## 민감 레이블 {#sensitive}

중요 &quot;S&quot; 레이블은 사용자 및 조직에서 중요하다고 간주하는 데이터를 분류하는 데 사용됩니다.

중요하다고 고려할 수 있는 데이터 유형 중 하나는 서로 다른 유형의 지리적 데이터일 수 있지만 이 범주는 지리적 데이터로 제한되지 않습니다.

| 레이블 | 정의 |
| --- | --- |
| **S1** | 장치의 정확한 위치를 결정하는 데 사용할 수 있는 위도와 경도를 지정하는 데이터입니다. |
| **S2** | 광범위하게 정의된 지오펜스 영역을 결정하는 데 사용할 수 있는 데이터입니다. |
| **PSPD** | 허용된 중요 개인 데이터(PSPD)는 계약상 Adobe에서 &quot;중요&quot;, &quot;특별한 데이터 범주&quot; 또는 해당 법률에서 사용하는 유사한 용어로 간주되는 업로드를 허용하는 데이터를 의미합니다. 이는 특별히 보호된 건강 정보 (PHI) 및 기타 규제 된 건강 데이터를 제외한다. |
| **RHD** | Adobe에서 계약상 업로드할 수 있는 PHI(보호 상태 정보) 또는 환자에 대한 정보를 참조하는 데이터입니다. |

## 파트너 에코시스템 레이블 {#partner}

파트너 에코시스템 레이블은 조직 외부의 소스에서 얻은 데이터를 분류하는 데 사용됩니다.

이 레이블은 잠재 고객 데이터 사용을 제어하는 데 사용됩니다.

| 레이블 | 정의 |
| --- | --- |
| **타사** | 타사 데이터는 타사 데이터 공급업체에서 제공한 데이터입니다. 서드파티 데이터 공급업체는 Experience Platform과 함께 서드파티의 데이터에 액세스하고, 사용하고, 표시하고, 전송할 수 있도록 귀하에게 승인하는 계약을 조직과 체결한 엔티티입니다. |
| **타사 데이터 보강** | 데이터 주체와 직접 관련이 없는 서드파티 조직에서 수집한 데이터. 레이블은 자사 프로필을 보강하는 데 사용되는 타사 데이터에 적용해야 합니다. |
| **타사 잠재 고객 확보** | 데이터 주체와 직접 관련이 없는 서드파티 조직에서 수집한 데이터. 레이블은 신규 고객을 대상으로 하는 funnel 전망 상단에 사용되는 서드파티 데이터에 적용되어야 합니다. |

## 부록

아래 섹션에서는 사용 가능한 데이터 사용 레이블에 대한 추가 정보를 제공합니다.

### 계약 레이블 세부 정보

다음 섹션에서는 특정 계약 &quot;C&quot; 레이블의 이행과 관련된 자세한 정보를 제공합니다.

#### C1 {#c1}

일부 데이터는 개별 또는 장치 식별자를 포함하지 않고 집계된 양식으로 Adobe Experience Cloud에서만 내보낼 수 있습니다. 예를 들어 소셜 네트워크에서 시작된 데이터입니다.

#### C2 {#c2}

일부 데이터 제공업체는 원래 수집된 위치에서 데이터 내보내기를 금지하는 조건을 계약서에 포함합니다. 예를 들어 소셜 네트워크 계약은 종종 이들로부터 받는 데이터의 전송을 제한합니다. C2 레이블은 집계 및 익명 데이터만 필요한 [C1](#c1)보다 더 제한적이지만 [C12](#c12)보다 덜 제한적이어서 대상에 관계없이 데이터를 완전히 내보낼 수 없습니다.

#### C3 {#c3}

Some data providers have terms in their contracts that prohibit the combination or use of that data with directly identifiable information. For example, contracts for data sourced from ad networks, ad servers, and third-party data providers often include specific contractual prohibitions on the use of such data with directly identifiable data.

#### C4 {#c4}

C4는 [C5](#c5), [C6](#c6) 및 [C7](#c7) 레이블을 포함합니다. [C12](#c12)에 이어 가장 제한적인 레이블 중 하나입니다.

#### C5 {#c5}

Interest-based targeting, or personalization, occurs if the following three conditions are met: The data collected on-site is (1) used to make inferences about a users&#39; interests, (2) is used in another context, such as on another site or app (off-site) AND (3) is used to select which content or ads are served based on those inferences.

온사이트 데이터와 오프사이트 데이터의 조합 또는 여러 오프사이트 소스의 데이터 조합을 포함하는 여러 사이트의 데이터 조합을 크로스 사이트 데이터라고 합니다. Different sites represent different contexts such that the use of cross-site data in any context is different than the original. 크로스 사이트 데이터는 일반적으로 사용자의 관심 분야를 추론하기 위해 수집 및 처리됩니다. As a result, the use of cross-site data for targeting ads or content typically qualifies as interest-based targeting, regardless of whether the ad or content appears on-site or off-site. For example, if on-site data was used in combination with off-site data to select which ad to show a user on an organization&#39;s own site, that use would qualify as interest-based targeting. As another example, retargeting ads to users off-site would also likely qualify as interest-based targeting.

Use of off-site data alone for targeting would likely also qualify as interest-based targeting since off-site data is usually collected and processed to make inferences about users&#39; interests.

그러나 온사이트 데이터만 사용하는 콘텐츠 또는 광고는 일반적으로 관심 기반 타깃팅으로 적합하지 않습니다. 달리 관심 기반 타깃팅으로 분류되지 않는 온사이트 타깃팅은 두 개의 개별 레이블로 처리됩니다. 특히 레이블 C6은 온사이트 광고 타기팅 및 보고를 다루고 광고 선택, 전달 및 보고를 특별하게 설명하며, 레이블 C7은 온사이트 콘텐츠 선택, 전달 및 보고(온사이트 콘텐츠 타기팅)를 다룹니다.

궁극적으로 레이블의 해석 및 해당 레이블의 데이터 사용이 적용되는 방식은 사용자가 결정합니다. 참고로 IAB 및 DAA 프레임워크는 아래에 나와 있습니다.

Personalization. 시간이 지남에 따라 다른 웹 사이트 또는 앱과 같은 다른 컨텍스트에서 광고 및/또는 콘텐츠를 개인화하기 위해 이 서비스를 사용하는 것에 대한 정보의 수집 및 처리. 일반적으로 사이트 또는 앱의 콘텐츠는 향후 광고 및/또는 콘텐츠 선택을 알리는 관심사에 대한 추론을 만드는 데 사용됩니다.

DAA: 온라인 행동 광고. 시간 경과에 따른 웹 보기 동작과 관련된 특정 컴퓨터 또는 장치에서 데이터를 수집하여 이러한 웹 보기 동작으로 추론된 환경 설정 또는 관심 사항을 기반으로 해당 컴퓨터 또는 장치에 광고를 게재하기 위해 이러한 데이터를 사용하여 사용자 환경 설정 또는 관심 사항을 예측합니다.

#### C6 {#c6}

광고는 주로 상품 또는 서비스의 판매를 촉진하기 위한 웹 사이트 또는 앱에 나타나는 텍스트 및 이미지를 포함하는 메시지 또는 알림입니다. 이러한 메시지 또는 알림의 목적을 결정하는 것은 귀하의 책임입니다. 광고는 온 사이트 콘텐츠와 별개이며 레이블 [C7](#c7)에 포함됩니다. C6 레이블이 있는 데이터는 조직의 웹 사이트 또는 앱에서 광고를 선택 및 전달하거나 그러한 광고의 전달 및 효과를 측정하는 등 온사이트 광고 타겟팅에 사용할 수 없습니다. 여기에는 사용자의 관심사에 대해 이전에 수집된 현장 데이터를 사용하여 광고를 선택하고, 어떤 광고가 표시되었는지, 언제 어디서 표시되었는지, 사용자가 광고 선택 또는 구매 등 광고와 관련된 작업을 수행했는지 등이 포함됩니다. 일반적으로 해당 사용자의 온사이트 활동을 기반으로 사용자 환경 설정을 추정한 다음 온사이트 광고 타겟팅에서 이러한 환경 설정을 사용하면 관심 기반 타겟팅에 필요한 세 가지 요구 사항을 모두 충족하지 않으므로 관심 기반 타겟팅(개인화)으로 적합하지 않습니다. *[이러한 요구 사항에 대해서는 레이블 C5를 참조하십시오.](#c5)*

Ultimately, the interpretation of the label and how usage of data with that label is enforced is up to you. For reference, the IAB and DAA frameworks are provided below:

IAB: 3. Ad selection, delivery, reporting: The collection of information, and combination with previously collected information, to select and deliver advertisements for you, and to measure the delivery and effectiveness of such advertisements. This includes using previously collected information about your interests to select ads, processing data about what advertisements were shown, how often they were shown, when and where they were shown, and whether you took any action related to the advertisement, including for example selecting an ad or making a purchase. This does not include Personalization, which is the collection and processing of information about your use of this service to subsequently personalize advertising and/or content for you in other contexts, such as websites or apps, over time.

DAA: Online Behavioral Adverting does not include the activities of First Parties, Ad Delivery or Ad Reporting, or contextual advertising (i.e. advertising based on the content of the Web page being visited, a consumer&#39;s current visit to a Web page, or a search query).

#### C7 {#c7}

현장 콘텐츠는 정보, 교육 또는 접대를 위해 고안된 텍스트 및 이미지이며, 상품 또는 서비스의 판매를 촉진하기 위해 만들어지지 않습니다. 콘텐츠가 기본 광고로 적합한지 여부를 포함하여 콘텐츠의 목적을 결정하는 것은 귀하의 책임입니다. C7 레이블은 레이블 [C6](#c6)에 포함된 온사이트 광고를 다루지 않습니다. C7 레이블이 있는 데이터는 조직의 웹 사이트 또는 앱에서 컨텐츠를 선택하고 전달하는 것을 포함하여 온사이트 컨텐츠 타깃팅에 사용하거나 이러한 컨텐츠의 전달 및 효과를 측정하는 데 사용할 수 없습니다. 여기에는 선택한 컨텐츠에서 사용자의 관심 분야, 컨텐츠가 표시된 횟수 또는 기간, 컨텐츠가 표시된 시기 및 위치, 사용자가 컨텐츠 선택을 포함하여 컨텐츠와 관련된 작업을 수행했는지 여부에 대해 이전에 수집된 정보가 포함됩니다. 일반적으로 해당 사용자의 온사이트 활동을 기반으로 사용자 환경 설정을 추정한 다음 온사이트 콘텐츠 타겟팅에서 이러한 환경 설정을 사용하면 관심 기반 타겟팅에 필요한 세 가지 요구 사항을 모두 충족하지 않으므로 관심 기반 타겟팅(개인화)으로 적합하지 않습니다. *[이러한 요구 사항에 대해서는 레이블 C5를 참조하십시오.](#c5)*

궁극적으로 레이블의 해석 및 해당 레이블의 데이터 사용이 적용되는 방식은 사용자가 결정합니다. 참고로 IAB 및 DAA 프레임워크는 아래에 나와 있습니다.

IAB: 4. 콘텐츠 선택, 전달, 보고: 정보 수집 및 이전에 수집된 정보와의 결합을 통해 콘텐츠를 선택하고 전달하며 해당 콘텐츠의 전달 및 효과를 측정합니다. 여기에는 컨텐츠를 선택하기 위해 이전에 수집된 관심 분야에 대한 정보를 사용하고, 컨텐츠가 표시된 횟수, 컨텐츠가 표시된 빈도 또는 시간, 컨텐츠가 표시된 시기 및 위치, 컨텐츠 선택을 포함하여 컨텐츠와 관련된 작업을 수행했는지 여부 등이 포함됩니다. 여기에는 Personalization이 포함되지 않으며, 이는 웹 사이트 또는 앱과 같은 다른 컨텍스트에서 시간에 따라 이후에 콘텐츠 및/또는 광고를 개인화하기 위해 이 서비스를 사용하는 것에 대한 정보의 수집 및 처리입니다.

DAA: 온라인 행동 광고에는 자사, 광고 게재 또는 광고 보고 또는 상황별 광고(즉, 방문 중인 웹 페이지의 콘텐츠, 소비자의 현재 웹 페이지 방문 또는 검색 쿼리를 기반으로 하는 광고)는 포함되지 않습니다.

#### C8 {#c8}

데이터를 사용하여 조직의 사이트 또는 앱에 대한 사용자의 사용을 측정, 이해 및 보고할 수 없습니다. 여기에는 관심 기반 타기팅(사이트 간 타기팅)이 포함되지 않습니다. 이는 귀하의 이 서비스 사용에 대한 정보 수집으로, 시간이 지남에 따라 다른 컨텍스트(예: 웹 사이트 또는 앱과 같은 다른 서비스)에서 귀하를 위해 콘텐츠 및/또는 광고를 개인화하는 것입니다.

#### C9 {#c9}

일부 계약에는 데이터 과학을 위한 데이터 사용에 대한 명시적 금지가 포함되어 있습니다. 간혹 인공지능(AI), 머신러닝(ML), 모델링 등에 데이터 사용을 금지하는 용어로 표현된다.

#### C10 {#c10}

일부 데이터 거버넌스 정책은 개인화를 위해 결합된 ID 데이터의 사용을 제한합니다. 병합 정책에서 &quot;비공개 그래프&quot; 옵션을 사용하는 경우 C10 레이블이 대상에 자동으로 적용됩니다.

#### C11 {#c11}

Adobe Experience Platform 세그먼트 일치를 사용하면 Experience Platform 생성 대상자를 개인 정보 및 동의 환경 설정과 일치시켜 풍부한 프로파일링 및 다운스트림 인사이트를 촉진할 수 있습니다. C11 레이블은 [!DNL Segment Match] 프로세스에서 사용하지 않아야 하는 데이터를 나타냅니다. 세그먼트 일치에서 제외할 데이터 세트 및/또는 필드를 결정하고 그에 따라 C11 레이블을 추가하면 레이블이 세그먼트 일치 워크플로에 의해 자동으로 적용됩니다.

#### C12 {#c12}

어떤 방식으로든 Experience Platform에서 이 레이블이 있는 데이터를 내보낼 수 없습니다. C12 레이블 필드가 CSV 다운로드, API 사용 및 활성화 워크플로에서 제외됩니다.
