---
title: Real-Time CDP B2B 에디션의 관련 계정
type: Documentation
description: Real-Time CDP B2B Experience Platform의 관련 계정 기능에 대한 개요 및 추가 정보입니다.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 4%

---

# Real-Time CDP B2B 에디션의 관련 계정

## 개요 {#overview}

B2B 기업은 고객 정보가 여러 시스템에 저장되어 있는 경우가 많으며, 각 시스템에는 동일한 실제 사업체에 대한 부분적인 데이터만 포함되어 있거나 심지어 충돌하는 데이터도 포함되어 있습니다. 따라서 B2B 마케팅 및 판매 노력의 효율성과 효과를 줄이기 위해 고객을 정확하게 파악해야 하는 과제가 커집니다.

| ID | 이름 | 웹 사이트 | 산업 | 주/도 | 휴대폰 | 금액이 `$1 million`보다 큰 영업 기회가 열려 있습니다. |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | 소프트웨어 | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | 소프트웨어 | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Acme 컨설팅 서비스 | `http://www.acme.com/consulting` | 기술 컨설팅 | 뉴욕 | (212)471-0904 | x |
| 5 | 어크미 |   |   | CA |   |   |

{style="table-layout:auto"}

이제 관련 계정을 사용하여 [!DNL Real-Time CDP B2B]에 검색 중인 계정과 유사한 계정 목록이 표시됩니다.

![Experience Platform UI에서 관련 계정을 표시하는 화면입니다.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

이 기능을 사용하여 Experience Platform UI에서 계정 프로필에 대한 관련 계정 프로필을 본 다음 세그먼트 정의에 관련 계정을 포함시켜 범위를 넓히거나 대상에 더 넓은 기준을 적용할 수 있습니다.

## 관련 계정 서비스 활성화 {#enable}

서비스를 사용하려면 사이드바에서 **[!UICONTROL 프로필]**&#x200B;을 선택한 후 **[!UICONTROL 설정]**&#x200B;을 선택하십시오.

![Experience Platform UI에서 프로필 및 설정을 강조 표시합니다.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

[!UICONTROL 관련 계정 사용] 옆의 토글을 선택하여 서비스를 사용하도록 설정한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![전환 및 저장을 강조 표시하는 계정 설정 화면](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## 작동 방식 {#how-it-works}

일별 실행 머신 러닝 작업은 계층 알고리즘을 사용하여 유사한 계정 프로필을 다음 세 가지 요소를 기반으로 그룹으로 클러스터링합니다.

* 상위 계정 링크
* 웹 도메인
* 계정 이름

처리 작업이 완료되면 계정 프로필 그룹의 각 구성원에는 관련 계정 목록이 표시됩니다. 계정 프로필 페이지의 **관련 계정** 탭에서 목록을 보고 세그먼트 정의에 관련 계정을 사용할 수 있습니다.

[프로필 보강 관련 계정 작업](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)에 대한 자세한 내용은 설명서를 참조하세요.

## 관련 계정을 보는 방법 {#how-to-view}

Experience Platform UI에서 탐색 중인 계정에 대한 관련 계정을 볼 수 있습니다.

[UI에서 관련 계정을 찾는 방법](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)에 대한 자세한 내용은 설명서를 참조하세요.

## 관련 계정을 사용하는 방법 {#how-to-use}

세분화에서 계정 및 관련 계정을 사용할 수 있습니다. 세그먼트 정의에서 관련 계정을 사용할지 여부는 마케팅 사용 사례에 따라 다릅니다. 예를 들어 이메일 마케팅 또는 광고 캠페인에 관련 계정을 사용하여 정확도를 낮추고 범위를 넓힐 수 있습니다.

관련 계정을 사용하는 [세그먼테이션 예제](/help/rtcdp/segmentation/b2b.md#related-accounts)를 참조하세요.
