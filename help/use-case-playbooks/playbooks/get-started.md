---
solution: Experience Platform
title: 사용 사례 플레이북 시작
description: 사용 사례 플레이북 기능을 시작하는 방법에 대해 알아봅니다.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 703c84e61af105bc3933e4750a3cb27df8ac19fe
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 14%

---


# 시작하기

자동으로 설정되지 않은 경우 Real-time Customer Data Platform 및 Adobe Journey Optimizer용으로 설계된 사용 사례 플레이북에 대한 계정을 설정하는 방법을 알아봅니다. 세 가지 주요 구성 단계는 다음과 같습니다.

* 샌드박스 만들기
* 사용자 권한 구성
* 이메일, 푸시 및 SMS 알림에 대한 Journey Optimizer 채널 표면 구성(Journey Optimizer 플레이북을 사용할 계획인 경우)

Experience Platform UI에서 사용 사례 플레이북의 다양한 갤러리에 액세스하려면 왼쪽 탐색에서 **[!UICONTROL 플레이북]**&#x200B;을 선택하십시오. [사용 사례 플레이북을 탐색](../playbooks/navigate.md)하고 [영감을 주는 샌드박스](../playbooks/navigate.md)를 시작하는 방법에 대한 설명서를 읽어 보십시오.

## 사용 사례 플레이북 구성 - 비디오 연습 {#video}

이 비디오를 통해 Journey Optimizer에서 샌드박스를 만들고, 권한을 구성하고, 이메일, 푸시 및 SMS 알림에 대한 채널 표면을 구성하는 데 필요한 단계에 대해 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## 개발 샌드박스 만들기 {#create-development-sandbox}

사용 사례 플레이북은 특수한 유형의 개발 샌드박스를 사용합니다. [[!UICONTROL 사용 사례 플레이북]](/help/use-case-playbooks/playbooks/overview.md) 기능을 시작하고 액세스하려면 아래와 같이 접미사에 `-ucp` 또는 `-UCP`가 포함된 이름(제목이 아닌)으로 [새 개발 샌드박스를 만듭니다](/help/sandboxes/ui/user-guide.md#create)(프로덕션 샌드박스는 선택하지 않음).

>[!IMPORTANT]
>
>새 개발 샌드박스를 만들 때 이름에 접미사에 `-ucp` 또는 `-UCP`이(가) 포함되어 있는지 확인하십시오.


![사용 사례 플레이북을 위한 개발 샌드박스 생성](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

이제 [!UICONTROL 사용 사례 플레이북]의 왼쪽 레일에 [!UICONTROL 플레이북]이 표시됩니다.

![샌드박스를 만든 후에 UI에서 사용 사례 플레이북을 사용합니다.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

위와 같이 왼쪽 레일에 [!UICONTROL 플레이북]이 표시되지 않으면 해당 링크(`https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates`)를 사용하여 직접 이동합니다. 이 링크에서 `<YOUR_ORG>`는 조직 이름이며 `<YOUR_SANDBOX_NAME>`는 생성한 개발 샌드박스의 이름입니다.

## 팀에 필요한 액세스 권한 부여 {#grant-access-permissions}

[!UICONTROL 사용 사례 플레이북]을 시작하려면 마케팅 팀원이 만든 플레이북 목록을 보거나 직접 플레이북을 만들 수 있도록 올바른 권한이 필요합니다.

**필요한 권한**

필요한 권한을 추가하려면 권한 UI에서 [이미 구성한 역할](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role)에 새 사용 사례 플레이북 샌드박스를 포함하십시오. 여기에는 다른 개발 샌드박스에 사용된 역할도 포함됩니다.

![이미 구성된 역할에 대한 플레이북 샌드박스](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**플레이북에 대한 역할 설정:**

또는 [필요한 권한](/help/access-control/home.md#sandboxes-and-permissions)을 사용하여 새 역할을 추가하는 방법도 고려해 볼 수 있습니다.

필수 플레이북 작업에 필요한 권한을 가진 [새 역할을 설정](/help/access-control/abac/ui/permissions.md)합니다. 아래 표시된 대로 역할을 만들고 새 샌드박스를 추가합니다.

![역할을 만들어 샌드박스에 추가](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

플레이북 인스턴스에 대한 **권한**

사용 사례 플레이북의 일부로 스키마, 대상, 여정 등 다양한 에셋을 만들 수 있습니다. 이러한 개체를 만들려면 사용자와 다른 사용자에게 올바른 권한이 필요합니다.

**스키마에 대한 권한**

스키마를 만들고 관리하려면 데이터 모델링 권한을 활용하십시오. **[!UICONTROL 스키마 관리]**, **[!UICONTROL 스키마 보기]**, **[!UICONTROL 관계 관리]**, **[!UICONTROL ID 메타데이터 관리]**

대상에 대한 **권한**

대상을 만들고 관리하려면 대상 권한을 사용합니다. **[!UICONTROL 관리]**, **[!UICONTROL 대상]**, **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 매핑하지 않고 세그먼트 활성화]**, **[!UICONTROL 데이터 세트 대상 관리 및 활성화]**, **[!UICONTROL 대상 작성]**.

**여정에 대한 권한**

여정을 만들고 관리하려면 여정 권한(**[!UICONTROL 여정 관리]**, **[!UICONTROL 여정 보기]**, **[!UICONTROL 여정 보고서 보기]**, **[!UICONTROL 여정 관리]**, **[!UICONTROL 이벤트]**, **[!UICONTROL 데이터 소스 및 작업 보기]**, **[!UICONTROL 여정 보기]**, **[!UICONTROL 이벤트]**, **[!UICONTROL 데이터 소스 및 작업, Publish 여정]**)을 사용합니다.

아래 이미지는 플레이북과 플레이북에서 생성된 에셋을 보고, 만들고, 관리하는 데 사용할 수 있는 권장 권한의 스냅숏을 표시합니다.

![플레이북의 모든 인스턴스를 만드는 데 필요한 모든 권한 항목의 스냅숏](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**역할에 사용자 추가**

위에서 참조한 대로 [새 역할을 만든](/help/access-control/abac/ui/permissions.md#managing-users-for-role)후 자신을 사용자로 추가합니다. 보기 전용 액세스 권한을 가진 다른 사용자 집합에 대해 제한된 액세스 권한을 가진 역할을 만드는 경우 이러한 권한과 연결된 필요한 보기 항목만 포함하십시오.

## Journey Optimizer에서 샌드박스 및 채널 표면 구성 {#configure-channel-surfaces}

조직에서 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko-KR)에 대한 라이선스를 보유하고 있으며 Journey Optimizer용으로 설계된 플레이북을 사용하려는 경우 샌드박스에서 메시지에 필요한 기술 매개 변수를 정의하는 채널 사전 설정을 구성해야 합니다. [Adobe Journey Optimizer에서 채널 표면을 설정하는 방법에 대해 알아봅니다](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Journey Optimizer에서 플레이북의 인스턴스를 생성하려면 이메일, 푸시 및 SMS 알림에 대한 채널 표면을 구성해야 합니다.

### 전자 메일 채널 표면

Journey Optimizer 인터페이스의 `Channels`(으)로 이동합니다. 아직 구성되지 않은 경우 마케팅 이메일 및 트랜잭션 메시지를 위한 별도의 하위 도메인 및 IP 풀을 구성합니다. 다음은 주문 확인 이메일과 같은 트랜잭션 메시지가 고객에게 전달되도록 하는 모범 사례입니다. 이름, 이메일 주소 및 추가 설정을 입력합니다. 페이지 오른쪽 상단에서 **제출**&#x200B;을 선택하여 마케팅 채널 표면을 만듭니다. [전자 메일 채널 표면을 설정하는 방법](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html)에 대한 설명서를 읽어 보십시오.

### SMS 채널 표면

SMS 채널 표면을 만들려면 먼저 SMS API 자격 증명을 만들고 기본 공급업체(예: Sinch)를 선택합니다. SMS 채널 표면의 이름을 지정하고(예: SMS 마케팅) 구성을 선택한 다음 발신자 번호를 입력합니다. SMS 채널 표면을 저장하려면 페이지 오른쪽 상단에서 **제출**&#x200B;을 선택합니다. [SMS 채널 표면을 설정하는 방법](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=ko#message-preset-sms)에 대한 설명서를 읽어 보십시오.

또한 주문 확인과 같은 트랜잭션 메시지가 포함된 플레이북에 대한 채널을 구성합니다.

### 푸시 채널 표면

채널 구성이 Experience Platform 또는 데이터 컬렉션 인터페이스에서 구성되었는지 확인합니다. 이는 데이터 수집 환경에서 채널 구성이 어떻게 표시되는지 보여 줍니다.

<!-- ![Channel configurations in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

그런 다음 채널 구성에서 확인한 채널, 플랫폼 및 앱을 선택합니다. 푸시 채널 표면을 만들려면 **제출**&#x200B;을 선택합니다.

[푸시 채널 표면을 설정하는 방법](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html)에 대한 설명서를 읽어 보십시오.

## 다음 단계 {#next-steps}

이 문서의 모든 단계를 수행했으므로 왼쪽 탐색에서 사용 사례 플레이북을 사용할 수 있는 개발 샌드박스를 생성해야 합니다. 이제 팀원에게 플레이북을 보고 관리하고 에셋을 생성하는 데 필요한 권한을 부여하는 방법도 알아봅니다. 다음 단계로 [올바른 플레이북을 선택](/help/use-case-playbooks/playbooks/choose.md)한 다음 [인스턴스를 만드는 방법](/help/use-case-playbooks/playbooks/create-share-reuse.md)을 읽어 보십시오.
