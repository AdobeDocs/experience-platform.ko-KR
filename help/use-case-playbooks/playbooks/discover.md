---
solution: Experience Platform
title: 플레이북 살펴보기
description: 플레이북의 갤러리를 탐색하고 영감을 주는 샌드박스를 시작하는 방법에 대해 알아봅니다.
role: User
source-git-commit: ad3f746580f85e77cba390208d147b35b6854e10
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---

# 플레이북 살펴보기

사용 사례 플레이북은 모든 Adobe Experience Platform 고객에게 추가 비용 없이 제공됩니다. Experience Platform UI에서 사용 사례 플레이북의 풍부한 갤러리에 액세스하려면 다음을 선택합니다. **[!UICONTROL 플레이북]** 왼쪽 탐색에서.

![사용 사례 플레이북 갤러리.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![왼쪽 탐색 막대에서 사용 사례 플레이북에 직접 액세스합니다.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

세부 정보 페이지로 이동할 플레이북을 선택한 다음 을 선택합니다. **[!UICONTROL 영감을 주는 샌드박스로 이동]**. 확인 모달이 나타납니다. 선택 **확인** 다양한 사용 사례를 탐색하고 실험할 수 있는 영감을 주는 샌드박스로 이동합니다.

샌드박스를 생성할 수 있는 권한이 없는 경우 관리자에게 문의하여 영감을 주는 샌드박스를 생성하십시오.

>[!TIP]
>
>영감을 주는 샌드박스는 Adobe Experience Platform 내의 개발 샌드박스로, 라이브 프로덕션 환경에서 구현하기 전에 다양한 사용 사례를 만들고, 테스트하고, 실험할 수 있습니다.

![영감을 주는 샌드박스로 이동합니다.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

영감을 주는 샌드박스를 아직 설정하지 않았다면 다음을 선택합니다. **[!UICONTROL 영감을 주는 샌드박스 만들기]**. 모달이 나타납니다. 다음을 입력합니다. **이름** 및 **제목** 필수 필드 상자에서 **만들기**. 영감을 주는 샌드박스를 만들고 나면 [권한 정의](/help/access-control/home.md) 인스턴스를 만들기 위해 사용 사례 플레이북 세부 사항 페이지로 돌아가기 전에.

![영감을 주는 샌드박스를 제작합니다.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![영감을 주는 샌드박스를 제작하려면 이름과 제목을 입력합니다.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

영감을 주는 샌드박스 외부에서 사용 사례 플레이북을 선택하면 인스턴스를 만들 수 없습니다. 세부 정보 페이지에서 **영감을 주는 샌드박스로 이동** 기존 영감을 주는 샌드박스로 이동한 다음 **[!UICONTROL 인스턴스 만들기]**.

샌드박스를 생성할 수 있는 권한이 없는 경우 관리자에게 문의하여 영감을 주는 샌드박스를 생성하십시오.

![샌드박스를 생성할 수 있는 권한이 없습니다.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

할당된 샌드박스 수의 한도에 도달한 경우 조직 관리자에게 문의하여 한도를 늘리거나 일부 활성 샌드박스를 비활성화 또는 제거하라는 메시지가 나타납니다. 샌드박스 제한이 조정되거나 활성 샌드박스 수가 감소되면 영감을 주는 샌드박스를 계속 만들 수 있습니다.

![샌드박스 제한에 도달했습니다.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

영감을 주는 샌드박스를 만들 때 이메일, 푸시 및 SMS 알림에 대한 채널 표면이 자동으로 설정되지 않습니다. IT 관리자에게 문의하여 인스턴스를 수동으로 구성하십시오. 그렇지 않으면 인스턴스 만들기에 실패할 수 있습니다.

![채널 사전 설정을 구성합니다.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Journey Optimizer에서 샌드박스 및 채널 표면 구성 {#configure-channel-surfaces}

조직에 라이센스가 부여된 경우 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko-KR), 그리고 Journey Optimizer용으로 설계된 플레이북을 사용하려는 경우 샌드박스에서 메시지에 필요한 기술 매개 변수를 정의하는 채널 사전 설정을 구성해야 합니다. [Adobe Journey Optimizer에서 채널 표면을 설정하는 방법에 대해 알아봅니다](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Journey Optimizer에서 플레이북의 인스턴스를 생성하려면 이메일, 푸시 및 SMS 알림에 대한 채널 표면을 구성해야 합니다.

### 전자 메일 채널 표면

다음으로 이동 `Channels` Journey Optimizer 인터페이스에서 다음을 수행합니다. 아직 구성되지 않은 경우 마케팅 이메일 및 트랜잭션 메시지를 위한 별도의 하위 도메인 및 IP 풀을 구성합니다. 다음은 주문 확인 이메일과 같은 트랜잭션 메시지가 고객에게 전달되도록 하는 모범 사례입니다. 이름, 이메일 주소 및 추가 설정을 입력합니다. 선택 **제출** 페이지 오른쪽 상단에서 마케팅 채널 표면을 만듭니다. 의 설명서를 읽어 보십시오. [전자 메일 채널 표면 설정 방법](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS 채널 표면

SMS 채널 표면을 만들려면 먼저 SMS API 자격 증명을 만들고 기본 공급업체(예: Sinch)를 선택합니다. SMS 채널 표면의 이름을 지정하고(예: SMS 마케팅) 구성을 선택한 다음 발신자 번호를 입력합니다. 선택 **제출** 페이지 오른쪽 상단에서 SMS 채널 표면을 저장합니다. 의 설명서를 읽어 보십시오. [sms 채널 표면을 설정하는 방법](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=ko#message-preset-sms).

또한 주문 확인과 같은 트랜잭션 메시지가 포함된 플레이북에 대한 채널을 구성합니다.

### 푸시 채널 표면

앱 표면이 Experience Platform 또는 데이터 컬렉션 인터페이스에서 구성되었는지 확인합니다. 이는 데이터 수집 환경에서 앱 표면이 어떻게 보이는지 설명합니다.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 영감을 주는 샌드박스를 설정하는 방법을 알아보고 Platform 내에서 사용 사례 플레이북에 액세스하는 다양한 방법을 숙지해야 합니다. 다음 단계로, 방법 을 읽어 보십시오. [찾기](/help/use-case-playbooks/playbooks/find.md) 올바른 플레이북입니다.

