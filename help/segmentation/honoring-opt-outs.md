---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 옵트아웃 준수
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 세그먼트에서 옵트아웃 요청 준수

Adobe Experience Platform을 통해 고객은 실시간 고객 프로필 내에서 데이터의 사용 및 저장과 관련된 옵트아웃 요청을 보낼 수 있습니다. 이러한 옵트아웃 요청은 캘리포니아 거주자에게 개인 데이터에 액세스하고 삭제할 수 있는 권한과 개인 데이터의 판매 또는 공개(및 누구에게) 여부를 알 수 있는 권한을 제공하는 CCPA(California Consumer Privacy Act)의 일부입니다.

고객이 옵트아웃한 후에는 마케팅 활동을 위해 고객을 생성할 때 해당 옵트아웃을 준수해야 합니다. 이 문서에서는 옵트아웃 요청 수리와 관련된 중요한 세부 사항에 대해 설명합니다.

## 시작하기

옵트아웃 요청을 준수하려면 관련된 다양한 Adobe Experience Platform 서비스를 이해해야 합니다. 옵트아웃 요청을 사용하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [실시간 고객 프로필](../profile/home.md):다양한 소스의 데이터를 집계하여 실시간으로 통합된 고객 프로파일을 제공합니다.
- [Adobe Experience Platform 세그멘테이션 서비스](./home.md):실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
- [XDM(Experience Data Model)](../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [Adobe Experience Platform 개인 정보 보호 서비스](../privacy-service/home.md):조직에서 플랫폼 내에서 고객 데이터와 관련된 데이터 개인 정보 보호 규정 준수를 자동화할 수 있습니다. 이러한 규정에는 다음이 포함됩니다.
   - CPA(California Consumer Privacy Act):개인 데이터를 액세스 및 삭제할 권리, 개인 데이터의 판매 또는 공개 여부(그리고 누구에게) 알 권리 등 캘리포니아 거주자를 위한 데이터 개인정보 보호 권리.
   - 개인 정보 보호 규정(GDPR):&#39;액세스 권한&#39; 및 &#39;잊혀질 권리&#39;를 비롯하여 유럽 연합 회원들에 대한 데이터 개인 정보 보호 권리.

## 옵트아웃 믹싱

CPA 옵트아웃 요청을 준수하려면 결합 스키마에 속하는 스키마 중 하나에 필요한 XDM(Experience Data Model) 옵트아웃 필드를 포함해야 합니다. 스키마에 옵트아웃 필드를 추가하는 데 사용할 수 있는 두 가지 믹스가 있으며, 각 믹스는 다음 섹션에서 더 자세히 다룹니다.

- [프로필 개인 정보](#profile-privacy):다양한 옵트아웃 유형(일반 또는 판매/공유)을 캡처하는 데 사용됩니다.
- [프로필 환경 설정 세부](#profile-preferences-details)사항:특정 XDM 채널에 대한 옵트아웃 요청을 캡처하는 데 사용됩니다.

스키마에 혼합을 추가하는 방법에 대한 단계별 지침은 다음 XDM 설명서의 &quot;믹서 추가&quot; 섹션을 참조하십시오.
- [스키마 레지스트리 API 자습서입니다](../xdm/api/getting-started.md).:스키마 레지스트리 API를 사용하여 스키마 빌드.
- [스키마 편집기 자습서](../xdm/tutorials/create-schema-ui.md):플랫폼 사용자 인터페이스를 사용하여 스키마 작성

다음은 사용자 인터페이스에서 스키마에 추가된 옵트아웃 믹스를 보여주는 예제 이미지입니다.

![](images/opt-outs/opt-out-mixins-user-interface.png)

각 혼합의 구조와 스키마에 기여하는 필드에 대한 설명이 다음 섹션에 자세히 설명되어 있습니다.

### 프로필 개인 정보

프로필 개인정보 보호 믹싱을 사용하면 고객의 두 가지 유형의 CPA 옵트아웃 요청을 캡처할 수 있습니다.

1. 일반 옵트아웃
2. 영업/공유 옵트아웃

![](images/opt-outs/profile-privacy.png)

프로필 개인 정보 혼합에는 다음 필드가 포함되어 있습니다.

- 개인 정보 옵트아웃(`privacyOptOuts`):옵트아웃 개체 목록이 포함된 배열.
- 옵트아웃 유형(`optOutType`):옵트아웃 유형입니다. 이 필드는 두 개의 가능한 값이 있는 열거형입니다.
   - 일반 옵트아웃(`general_opt_out`)
   - 영업 공유 옵트아웃(`sales_sharing_opt_out`)
- 옵트아웃 값(`optOutValue`):지정된 옵트아웃 유형을 기준으로 옵트아웃 신호의 값이라고도 하는 옵트아웃 상태의 활성 상태입니다. 이 필드는 4개의 가능한 값을 가진 열거형입니다.
   - 제공되지 않음(`not_provided`):옵트아웃 요청이 제공되지 않았습니다.
   - 검증 대기 중(`pending`):옵트아웃 요청이 확인 보류 중입니다.
   - 옵트아웃(`out`):고객이 수신 거부되었습니다.
   - 옵트인(`in`):고객이 선택하였습니다.
- 옵트아웃 타임스탬프(`timestamp`):수신된 옵트아웃 신호의 타임스탬프입니다.

프로필 개인 정보 혼합의 전체 구조를 보려면 XDM 공개 [GitHub 리포지토리를](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) 참조하거나 플랫폼 UI를 사용하여 믹싱을 미리 보십시오.

### 프로필 환경 설정 세부 사항

프로필 환경 설정 세부 사항 믹스인에서는 이메일 포맷, 기본 언어, 표준 시간대 등 고객 프로파일에 대한 기본 설정을 나타내는 여러 필드를 제공합니다. 이 믹스에 포함된 필드 중 하나인 OptInOut(`optInOut`)을 사용하면 개별 채널에 대해 옵트아웃 값을 설정할 수 있습니다.

![](images/opt-outs/profile-preferences-details.png)

프로필 환경 설정 세부 사항 믹스에는 옵트아웃과 관련된 다음 필드가 포함되어 있습니다.

- 옵트인아웃(`optInOut`):각 키가 통신 채널에 대해 유효하고 알려진 URI를 나타내고 각 채널에 대한 옵트아웃 상태의 활성 상태를 나타내는 개체입니다. 각 채널에는 다음 네 가지 값 중 하나를 사용할 수 있습니다.
   - 제공되지 않음(`not_provided`):이 채널에 대해 옵트아웃 요청이 제공되지 않았습니다.
   - 검증 대기 중(`pending`):이 채널에 대한 옵트아웃 요청이 확인 보류 중입니다.
   - 옵트아웃(`out`):고객이 이 채널을 선택 해제했습니다.
   - 옵트인(`in`):고객이 이 채널을 선택했습니다.
- 전역 옵트아웃(`globalOptout`):true로 설정되면 프로필에 대한 전역 옵트아웃 재정의를 설정하는 부울 값입니다. 이 필드의 기본값은 false입니다.

아래 JSON에서는 OptInOut 개체가 서로 다른 통신 채널에 대한 여러 옵트아웃 신호를 캡처하는 방법을 설명합니다.

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

프로필 환경 설정 세부 정보 혼합의 전체 구조를 보려면 XDM 공개 [GitHub 리포지토리를](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) 방문하거나 플랫폼 UI를 사용하여 믹싱을 미리 보십시오.

## 세그멘테이션의 옵트아웃 처리

CPA 옵트아웃 플래그로 표시된 프로파일이 세그먼트에 포함되지 않도록 하기 위해 특수 필드를 기존 세그먼트에 추가하거나 세그먼트 작성 중에 포함해야 합니다.

아래 섹션에서는 두 가지 유형의 옵트아웃 플래그에 적합한 필드를 추가하는 방법을 보여줍니다.
1. 일반 옵트아웃
2. 영업/공유 옵트아웃

### 일반 옵트아웃

세그멘테이션은 &quot;일반 옵트아웃&quot; 플래그가 포함된 모든 프로파일을 자동으로 처리합니다. 즉, 이러한 프로필은 기본적으로 대상 또는 내보내기에 포함되지 않습니다. 그러나 적합한 필드를 추가하여 옵트아웃 프로필이 대상 및 마케팅 활동에 포함되지 않도록 하는 것이 좋습니다.

이 작업은 개인 정보 옵트아웃 속성을 추가하여 세그먼트 빌더 사용자 인터페이스를 사용하여 수행할 **수** 있습니다. 이 경우 세그먼트는 옵트인을 선택한 사람만 포함하도록 설정됩니다(즉, 프로필에 일반적인 옵트아웃 플래그가 없습니다.). 이 작업은 &quot;옵트아웃 유형&quot;이 &quot;일반 옵트아웃&quot;이고 &quot;옵트아웃 값&quot;이 &quot;옵트아웃&quot;이라고 선언함으로써 수행됩니다.

![](images/opt-outs/segment-general-opt-out.png)

### 영업/공유 옵트아웃

사용자의 프로필에 판매/공유 옵트아웃 플래그가 설정된 경우 이 프로필은 더 이상 세그먼트 생성 또는 마케팅 활동에 사용되지 않습니다. 이 플래그가 적용되도록 하려면 &quot;옵트아웃 유형&quot;이 &quot;판매 공유 옵트아웃&quot;과 같아야 하며 &quot;옵트아웃 값&quot;은 &quot;옵트아웃&quot;과 같아야 합니다.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## 다음 단계

API 및 사용자 인터페이스를 통해 세그먼트 정의 및 대상을 사용한 작업을 포함하여 세그멘테이션에 대한 자세한 내용은 [세그멘테이션 개요를](./home.md)읽으십시오.

개인정보 보호 서비스가 법률 및 조직의 개인 정보 보호 규정을 자동으로 준수하도록 돕는 방법을 비롯하여 플랫폼 내의 데이터 개인 정보에 대한 자세한 내용은 개인 정보 보호 서비스 [설명서를](../privacy-service/home.md)참조하십시오.
