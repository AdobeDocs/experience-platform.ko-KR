---
title: Real-Time CDP B2B Edition의 관련 계정
type: Documentation
description: Real-Time CDP B2B Experience Platform의 관련 계정 기능에 대한 개요 및 추가 정보.
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 6%

---

# Real-Time CDP B2B Edition의 관련 계정

## 개요 {#overview}

B2B 기업은 동일한 실제 비즈니스 업체에 대해 일부 또는 충돌하는 데이터만 포함하여 여러 시스템에 고객 정보를 저장하는 경우가 많습니다. 이를 통해 고객의 정확한 관점을 파악할 수 있으므로 B2B 마케팅 및 영업 활동의 효율성과 효율성을 줄일 수 있습니다.

| ID | 이름 | 웹사이트 | 업종 | 주/도 | 전화 | 금액 > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | 소프트웨어 | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | 소프트웨어 | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Acme 컨설팅 서비스 | `http://www.acme.com/consulting` | 기술 컨설팅 | NY | (212)471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

관련 계정, [!DNL Real-Time CDP B2B] 이제 탐색 중인 계정과 유사한 계정 목록이 표시됩니다.

![Experience Platform UI에서 관련 계정을 표시하는 화면](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

이 기능을 사용하여 Experience Platform UI에서 계정 프로필에 대한 관련 계정 프로필을 보고 세그먼트 정의에 관련 계정을 포함하여 도달 범위를 넓히거나 세그먼트에서 더 넓은 기준을 적용할 수 있습니다.

## 작동 방법 {#how-it-works}

일별 기계 학습 작업은 계층 알고리즘을 사용하여 다음과 같은 세 가지 요소를 기반으로 유사한 계정 프로필을 그룹으로 클러스터링합니다.

* 상위 계정 링크
* 웹 도메인
* 계정 이름

처리 작업이 성공하면 계정 프로필 그룹의 각 구성원에게 관련 계정 목록에 태그가 지정됩니다. 여기에서 목록을 볼 수 있습니다 **관련 계정** 계정 프로필 페이지의 탭에서 세그먼트 정의에서 관련 계정을 사용합니다.

에 대한 자세한 내용은 설명서 를 참조하십시오. [프로필 보강 관련 계정 작업](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## 관련 계정을 보는 방법 {#how-to-view}

Experience Platform UI에서 탐색 중인 계정에 대한 관련 계정을 볼 수 있습니다.

에 대한 자세한 내용은 설명서 를 참조하십시오. [UI에서 관련 계정을 찾는 방법](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## 관련 계정을 사용하는 방법 {#how-to-use}

세그먼테이션에서 계정 및 관련 계정을 사용할 수 있습니다. 세그먼트 정의에서 관련 계정을 사용할지 여부를 결정하는 것은 마케팅 사용 사례에 따라 다릅니다. 예를 들어 이메일 마케팅 또는 광고 캠페인에 관련 계정을 사용할 수 있습니다. 이 경우 더 광범위한 도달 범위를 제공하는 대신 정확도가 낮아집니다.

다음을 참조하십시오 [세분화 예](/help/rtcdp/segmentation/b2b.md#related-accounts) 는 관련 계정을 사용합니다.
