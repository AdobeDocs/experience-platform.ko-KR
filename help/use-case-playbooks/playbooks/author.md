---
solution: Experience Platform
title: AI Assistant를 사용하여 나만의 플레이북을 작성하고 공유하는 방법을 알아봅니다.
description: 사용 사례 플레이북을 만들고 공유하는 방법
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 5cdbc160369a146da3ae8ca39d8c3095887e03b5
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# 나만의 플레이북 작성 및 공유(Beta)

Adobe Experience Platform의 AI Assistant에서 제공하는 [!DNL Playbook Authoring Framework]을(를) 사용하면 Adobe Experience Platform 내에서 플레이북을 효율적으로 만들고, 관리하고, 공유할 수 있습니다.

프레임워크는 다음 3단계 프로세스를 따릅니다.

1. **메타데이터 캡처**: AI Assistant 또는 웹 양식을 사용하여 플레이북 메타데이터를 캡처합니다.

2. **기술 연결**: 플레이북에 여정 또는 대상과 같은 특정 기술 자산을 추가합니다. 개발 샌드박스 내에서 플레이북 생성 프로세스를 완벽하게 제어하여 스키마 및 기타 고유한 데이터 구조와 정렬되도록 합니다.

3. **플레이북 배포**: 다른 조직에서 플레이북을 공유합니다. 예를 들어 ACME의 독일 마르테크 우수센터는 &#39;황금&#39; 플레이북을 만들어 태국, 호주 등의 지역 단체에 배포할 수 있다. 마케팅 사용 사례를 표준화하는 데 도움이 됩니다.

## 플레이북 만들기

AI Assistant를 사용하거나 수동으로 두 가지 방법으로 플레이북을 만들 수 있습니다. 다음 섹션을 읽고 AI Assistant를 사용하여 플레이북을 만드는 방법을 알아보십시오.

### 플레이북 개요

다음 단계에 따라 AI Assistant를 사용하여 플레이북을 만듭니다.

왼쪽 탐색 패널에서 **[!UICONTROL 플레이북]**&#x200B;을 선택합니다.

![왼쪽 탐색 패널에서 &quot;플레이북&quot; 옵션이 강조 표시된 플랫폼 UI.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

**[!UICONTROL 새 플레이북]**&#x200B;을 선택한 다음 **AI Assistant를 사용하여 플레이북 생성**&#x200B;을 선택합니다.

![AI Assistant를 사용하여 플레이북 생성 옵션을 선택한 플레이북 생성 인터페이스입니다.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

프롬프트 필드를 사용하여 사용 사례를 설명합니다. 예:

&quot;러닝화를 검색했지만 구매를 완료하지 않은 ACME 고객을 참여하십시오.&quot;

![사용자가 프롬프트를 입력할 수 있는 웹 폼 영역을 강조 표시하는 플레이북 만들기 인터페이스입니다.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

플레이북 메타데이터를 만들려면 **[!UICONTROL 생성]**&#x200B;을 선택하십시오.

![프롬프트 영역에서 강조 표시된 &quot;생성&quot; 단추를 표시하는 플레이북 만들기 인터페이스입니다.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

생성된 제목, 설명 및 메타데이터를 필요에 따라 수정하려면 **[!UICONTROL 편집]**&#x200B;을(를) 선택하십시오.

![사용자가 메타데이터를 수정할 수 있도록 &quot;편집&quot; 단추가 강조 표시된 생성된 플레이북입니다.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

데이터 엔지니어가 사용 사례를 설정하는 데 필요한 모든 세부 정보를 포함하도록 하려면 **[!UICONTROL 플레이북 세부 정보]** 섹션을 채우십시오. 이러한 필드는 주요 정보를 캡처하는 데 도움이 되지만, 적절한 기술 구성 요소를 보다 쉽게 연결할 수 있습니다(선택 사항). **[!UICONTROL 편집]**&#x200B;을(를) 선택하여 다음 필드에 값을 추가하십시오.

* **업계**
* **타겟 대상자**
* **마케팅 채널**

![업계, 대상 고객 및 마케팅 채널과 같은 세부 정보를 추가하거나 수정할 수 있도록 &quot;편집&quot; 단추가 강조 표시된 플레이북 세부 정보 섹션입니다.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

메타데이터가 생성되면 **[!UICONTROL 여정 맵 편집]**&#x200B;을(를) 선택하여 필요에 따라 여정 맵의 단계를 조정합니다.

![여정 맵의 단계를 수정하기 위한 &quot;여정 맵 편집&quot; 단추](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![플레이북 메타데이터를 캡처한 후 단계를 조정할 수 있는 여정 맵 편집기 인터페이스입니다.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

그런 다음 계속 진행하여 플레이북을 기술 에셋과 연결합니다. 플레이북을 수동으로 만들려면 **[!UICONTROL 플레이북 수동으로 만들기]**&#x200B;를 선택하십시오.

![플레이북을 빈 템플릿에서 시작하는 &quot;플레이북 수동으로 만들기&quot; 옵션입니다.](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

빈 플레이북 템플릿이 나타납니다. **제목** 및 **설명** 등 세부 정보를 입력하십시오. 필요에 따라 여정 맵을 편집하여 이벤트와 터치포인트를 추가할 수도 있습니다.

## 플레이북을 기술 자산과 연결

플레이북을 수동으로 만드는지 또는 AI Assistant를 사용하는지에 관계없이 플레이북을 필요한 기술 에셋과 연결해야 합니다. **[!UICONTROL 기술 Assets]** 탭으로 이동하여 필요한 제품을 선택합니다. 이 예제에서는 **[!UICONTROL Journey Optimizer]**&#x200B;을(를) 선택합니다.

>[!NOTE]
>
> Real-Time CDP에 대한 지원은 향후 릴리스에 추가될 예정입니다.

![기술 자산을 플레이북과 연결하는 데 사용할 수 있도록 &quot;필수 제품 추가&quot; 단추가 강조 표시된 &quot;기술 Assets&quot; 탭입니다.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

아래 이미지에 표시된 대로 이 플레이북을 여정과 연결하려면 **[!UICONTROL 자산 선택]**&#x200B;을 선택하십시오. 그런 다음 **플레이북 게시**&#x200B;를 선택하여 플레이북을 완료합니다.

![플레이북과 여정을 연결하는 데 사용할 수 있도록 &quot;에셋 선택&quot; 단추가 강조 표시된 &quot;기술 Assets&quot; 탭입니다.](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![플레이북과 연결할 여정을 선택하십시오.](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

플레이북이 게시되면 자동으로 여정의 스키마와 대상자 세부 사항을 추출하고 연결합니다.

![메타데이터 및 관련 기술 자산을 보여 주는 게시된 플레이북입니다.](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

만든 모든 플레이북은 **플레이북** 탭에서 사용할 수 있습니다.

![&quot;플레이북&quot; 탭에 생성된 플레이북 목록이 표시됩니다.](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

카탈로그에서 임의 플레이북을 선택하여 재사용할 인스턴스를 생성할 수 있습니다. 설명서를 참조하여 [인스턴스를 만드는 방법을 알아보세요](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![인스턴스 만들기 옵션이 강조 표시된 &quot;플레이북 개요&quot; 탭입니다.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> 플레이북이 게시되면 편집할 수 없습니다. 변경하려면 플레이북을 삭제하고 다시 시작하십시오.

## 프롬프트 예

AI 비서가 불필요한 정보를 걸러내면서 다양한 프롬프트 구조를 처리하고 주요 세부 정보를 추출할 수 있다. 다음은 사용자 프롬프트와 시스템에서 이를 해석하는 방법에 대한 몇 가지 예입니다.

**예 1:**

&quot;매출과 CLV를 늘리기 위해 &quot;룩을 완성하기&quot;라는 캠페인을 만듭니다. 이 캠페인에서는 주방용품이나 가구를 구매한 고객이 개별 추천과 구매 관련 오퍼를 통해 보완적으로 구매하도록 유도합니다. 고객에게 제품 추천을 알리는 메시지를 먼저 보냅니다. 7일 이내에 구매하지 않을 경우 제품 추천 및 오퍼와 함께 두 번째 메시지를 받게 됩니다. 푸시 알림 및 이메일을 사용하여 고객에게 연락합니다. 주방용품 또는 가구 범주에서 지난 7일 동안 구입한 고객으로 최근 30일 동안 대상이 되지 않은 고객을 대상으로 합니다. 캠페인의 일부로, 클릭 수(이메일, 앱, SMS, 푸시), CTR, E-Wallet CTR, AOV Conversion.CLV 매출, 총 구매 이벤트(매장 내, 디지털, 콜센터) 등의 KPI를 측정하려고 합니다.&quot;

![플레이북을 생성하기 위해 텍스트 입력란에 입력한 긴 프롬프트의 예입니다.](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**예 2:**

&quot;프로젝트 이름: 패션 뉴스레터
배경: (문제에 대한 사전 예방 또는 해결): 뉴스레터 커뮤니케이션을 구독한 ACME 고객에게 패션 뉴스레터를 보내도록 설계된 여정.
목표: 커뮤니케이션을 구독한 ACME 고객에게 패션 뉴스레터 이메일을 전송합니다.
프로모션 세부 사항: 고객은 매주 이메일 채널에서 패션 뉴스를 수신합니다. 이메일은 성별, 언어 및 시장에 따라 개인화되고 콘텐츠가 달라야 합니다.
프로젝트 채널/터치포인트: 이메일
타겟 대상: ACME 패션 뉴스레터 커뮤니케이션을 구독한 고객.
타겟 KPI/참여 지표/ROI: 1. 제품 수익 증대 2. 고객 충성도를 높입니다.&quot;

![플레이북을 생성하기 위해 텍스트 입력란에 입력한 조직화된 목록 스타일 프롬프트의 예입니다.](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**예 3:**

&quot;지속적인 제품 홍보 캠페인 동안 쇼핑객이 제품을 구입하도록 유도합니다.
이메일, SMS 또는 푸시 알림을 통해 적절한 커뮤니케이션을 전송하여 제품을 구매함으로써 지속적인 프로모션을 통해 쇼핑객과 소통할 수 있습니다. 24시간 동안 프로모션에 참여하지 않은 경우 알림 이메일을 보내십시오.&quot;

![플레이북을 생성하기 위해 텍스트 입력란에 입력한 간결한 프롬프트의 예입니다.](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**예 4:**

&quot;고등학교 선수들에게 신발을 팔아라.&quot;

![플레이북을 생성하기 위해 텍스트 입력란에 입력한 한 줄 프롬프트의 예입니다.](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

AI 어시스턴트는 &#39;프로젝트 이름&#39;이나 &#39;배경&#39;과 같은 불필요한 세부 정보를 모두 제거한다. 대상&quot;, &quot;캠페인 목표&quot; 및 &quot;마케팅 채널&quot;과 같은 주요 요소를 추출하고 모든 입력 스타일에서 작동합니다.

이러한 예는 AI가 사용자 프롬프트에서 중요한 세부 사항을 구체화하고 추출하는 방법을 보여줍니다.

>[!NOTE]
>
> 프롬프트를 작성하는 동안 PII 또는 명시적인 단어를 사용하지 마십시오.

## 콘텐츠 지침 및 중재

플레이북을 만들 때는 포함하는 언어와 콘텐츠를 염두에 두어야 합니다. 플레이북은 조직 전체에 표시되며, 사용자가 플래그 지정한 불쾌하거나 부적절한 콘텐츠도 표시됩니다.

### 플래그 지정 및 검토 프로세스

플레이북에 부적절하거나 불쾌한 콘텐츠가 포함되어 있는 경우 Adobe은 검토를 위해 보고서를 자동으로 수신합니다. Adobe은 플래그가 지정된 콘텐츠를 검토하고 적합하지 않다고 판단되면 고객에게 알리고 플레이북을 제거합니다.

## 샌드박스 간 플레이북 공유 {#share-playbooks-sandboxes}

하나의 샌드박스에서 플레이북을 만들고 게시하면 조직 내의 모든 샌드박스에서 자동으로 사용할 수 있게 됩니다. 이 기능을 사용하면 수동으로 공유할 필요가 없고 다른 샌드박스에서 플레이북의 인스턴스를 원활하게 만들 수 있습니다.

>[!TIP]
>
>플레이북이 대상 샌드박스의 유니온 스키마에서 사용할 수 없는 필드를 참조하거나 필요한 권한이 없는 경우 인스턴스를 만들려고 하면 오류 메시지가 표시됩니다. 이 메시지는 누락된 필드 및/또는 권한을 지정합니다.

유니온 스키마에서 누락된 필드가 있는 경우 가져오는 동안 대화 상자가 강조 표시됩니다.

![플레이북 가져오기 프로세스 중에 유니온 스키마에서 누락된 필드를 나열하는 대화 상자입니다.](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## 조직 간 플레이북 공유 {#sharing-playbooks-organizations}

조직 간에 플레이북을 공유하면 여러 팀이 동일한 모범 사례를 따라야 할 때 일관성과 효율성을 확보할 수 있습니다. 한 조직에서 다른 조직으로 플레이북을 공유하려면 다음 단계를 수행합니다.

1. **소스 조직에 로그인**: 만든 플레이북이 포함된 조직으로 이동하여 **[!UICONTROL 플레이북의]** 탭에서 공유합니다.
2. **플레이북 게시**: 플레이북이 아직 게시되지 않은 경우 공유하기 전에 먼저 게시해야 합니다.

   >[!NOTE]
   >
   >플레이북 공유를 활성화하려면 소스 조직과 대상 조직 간에 파트너십을 구축해야 합니다. [조직 파트너 관계 요청을 만드는 방법](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request)을 알아보세요.

3. **공유 시작**: 플레이북이 게시되고 파트너 관계가 설정되면 **[!UICONTROL 플레이북 공유]**&#x200B;를 선택합니다.
4. **대상 조직 선택**: 메시지가 표시되면 플레이북을 공유할 조직을 선택합니다.
5. **확인 및 공유**: 선택 내용을 확인합니다. 성공적인 공유를 나타내는 확인 메시지를 받게 됩니다.
6. **대상 조직 확인**: 대상 조직에 로그인하여 플레이북을 사용할 수 있는지 확인합니다.
7. **플레이북 가져오기**: **[!UICONTROL 가져오기]**&#x200B;를 선택하여 플레이북을 대상 조직으로 가져옵니다. **플레이북** 탭에서 볼 수 있습니다.

플레이북이 나타나지 않으면 게시되었는지, 그리고 조직 파트너십이 활성화되어 있는지 확인하십시오.

>[!IMPORTANT]
>
>전이적 플레이북 공유는 지원되지 않습니다. 한 조직에서 다른 조직으로 플레이북을 공유한 다음 가져오는 경우 받는 조직에서 다른 조직으로 다시 공유할 수 없습니다.

## 필요한 권한 {#required-permissions}

샌드박스에 액세스하여 이 기능을 사용하려면 다음 권한이 필요합니다.

### 샌드박스 권한

기능이 있는 샌드박스 환경에 액세스하려면 다음 권한이 필요합니다.

* **샌드박스 관리**
* **샌드박스 보기**

* **패키지 공유 권한**:

내부 공유 기능에는 다음 권한이 필요합니다.

* [**패키지 관리**](/help/sandboxes/ui/sandbox-tooling.md)
* [**패키지 공유**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

이 권한을 사용하여 다음을 수행할 수 있습니다.

* 샌드박스 환경 입력
* 샌드박스 내의 기능에 액세스
* 필요에 따라 패키지 관리 및 공유

이러한 권한은 권한 목록의 **[!UICONTROL 샌드박스]** 섹션에 있습니다.

![플레이북의 관리 및 공유에 대한 관련 권한이 강조 표시된 권한 목록입니다.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### 여정 및 관련 개체 - 권한

플레이북을 사용하는 여정을 작성할 때 **채널**, **대상** 및 기타 엔터티와 같은 다른 개체를 참조할 수 있습니다. 이러한 각 객체에는 고유한 사용 권한 집합이 있습니다.

다음은 여정 관련 작업에 대한 주요 권한입니다. 예:

* **여정 보기**
* **여정 관리**
* 대상 및 채널과 같은 오브젝트 관련 권한

또한 다음 대상 권한이 필요합니다.

* **세그먼트 읽기**
* **프로필 읽기**
* **데이터 세트 읽기**

여정은 유연성이 높고 상호 연결된 여러 개체가 포함될 수 있으므로 해당 [전체 권한](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions)은 별도로 문서화되며 특정 사용 사례에 따라 달라질 수 있습니다.

## 다음 단계

이제 AI Assistant를 사용하여 플레이북을 만들고, 게시하고, 공유하는 방법에 대해 알아보았으므로, 사용 가능한 플레이북을 시작하고 [플레이북 목록](/help/use-case-playbooks/playbooks/choose.md)에서 사용 사례에 적합한 플레이북을 선택하는 방법에 대해 알아보십시오.