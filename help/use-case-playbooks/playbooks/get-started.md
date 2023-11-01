---
solution: Experience Platform
title: 시작하기
description: 사용 사례 플레이북 기능을 시작하는 방법에 대해 알아봅니다.
badgeBeta: label="Beta" type="Informative"
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 100%

---

# (Beta) 시작하기

>[!AVAILABILITY]
>
>이 기능은 현재 Beta 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개발 샌드박스 만들기 {#create-development-sandbox}

[[!UICONTROL 사용 사례 플레이북]](/help/use-case-playbooks/playbooks/overview.md) 기능을 시작하고 액세스하려면 아래와 같이 접미사에 `-ucp` 또는 `-UCP`가 포함된 이름(제목이 아닌)으로 [새 개발 샌드박스를 만듭니다](/help/sandboxes/ui/user-guide.md#create)(프로덕션 샌드박스는 선택하지 않음).

![사용 사례 플레이북을 위한 개발 샌드박스 생성](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

이제 왼쪽 레일의 [!UICONTROL 사용 사례 플레이북] 또는 [!UICONTROL 마케터 플레이그라운드] 아래에 [!UICONTROL 플레이북]이 표시됩니다.

![샌드박스를 만든 후에 UI에서 사용 사례 플레이북을 사용합니다.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

위와 같이 왼쪽 레일에 [!UICONTROL 플레이북]이 표시되지 않으면 해당 링크(`https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates`)를 사용하여 직접 이동합니다. 이 링크에서 `<YOUR_ORG>`는 조직 이름이며 `<YOUR_SANDBOX_NAME>`는 생성한 개발 샌드박스의 이름입니다.

### Adobe Journey Optimizer 사용자를 위한 샌드박스 구성 {#sandbox-configuration-journey-optimizer}

조직에 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 라이선스가 부여된 경우 메시지에 필요한 기술 매개변수를 정의하는 채널 사전 설정을 샌드박스에 구성해야 합니다. [Adobe Journey Optimizer에서 채널 표면을 설정하는 방법에 대해 알아봅니다](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

## 팀에 필요한 액세스 권한 부여 {#grant-access-permissions}

[!UICONTROL 사용 사례 플레이북]을 시작하려면 마케팅 작업 팀원들에게 올바른 권한이 필요합니다. 다음과 같이 팀 권한을 부여할 수 있습니다.

* 플레이북 검색만 원하는 마케팅 작업 팀원은 **읽기** 권한을 받을 수 있습니다.
* 플레이북에서 인스턴스를 생성하려는 마케팅 작업 팀원은 **읽기 및 쓰기** 권한을 받을 수 있습니다.

## 다음 단계 {#next-steps}

이 문서를 읽고 난 후에는 [!UICONTROL 사용 사례 플레이북]을 시작하는 방법에 대해 알게 됩니다. 다음으로 [자신에게 적합한 플레이북을 검색](/help/use-case-playbooks/playbooks/discover.md)하고 [이를 기반으로 인스턴스를 생성](/help/use-case-playbooks/playbooks/create-share-reuse.md)하는 방법에 대해 읽어 보십시오.
