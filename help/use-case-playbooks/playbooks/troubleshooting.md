---
solution: Experience Platform
title: 플레이북의 알려진 제한 사항 및 문제 해결
description: 플레이북의 알려진 문제 및 일반적인 문제와 이러한 문제를 해결하는 방법에 대해 자세히 알아보십시오
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 문제 해결 {#troubleshooting}

사용 사례 플레이북으로 작업할 때 발생하는 일반적인 오류에 대한 문제 해결 제안 사항 보기

## Adobe Journey Optimizer 표면이 구성되지 않음 {#surfaces-not-configured}

플레이북의 인스턴스를 만들 때 아래 메시지가 표시될 수 있습니다.

![문제 해결](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

이는 Journey Optimizer 플레이북이 이메일, 푸시 및 SMS 채널에 대한 메시지를 만들기 때문입니다. 다른 표면을 구성하려면 [시작](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) 안내서를 읽어 보십시오.

## 새 인스턴스를 만들 때 *실패* 상태 {#status-failed}

인스턴스를 만들려고 할 때 실패 메시지가 표시되는 경우, 관리자가 사용자에게 필요한 사용자 권한을 부여하지 않았기 때문일 수 있습니다. 플레이북에는 다양한 에셋이 포함되어 있으며 사용자가 플레이북의 인스턴스를 성공적으로 만들려면 해당 에셋을 만들 수 있는 권한이 필요합니다. 사용 권한을 설정하는 방법은 이 안내서의 [사용 권한](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 섹션을 참조하십시오.

## 가져오기 실패 {#import-failure}

고객은 다양한 테스트 환경에서 작동하며 가끔 환경에서 Adobe 샌드박스로 인스턴스를 가져오는 동안 오류가 발생할 수 있습니다. 이러한 가져오기의 상태를 보려면 왼쪽 탐색에서 샌드박스 를 선택한 다음 작업 을 선택합니다. 여기에서 가져온 파일의 모든 세부 정보를 볼 수 있습니다. 실패 상태의 파일을 선택한 다음 작업 세부 사항 보기를 선택합니다. 모달이 나타납니다. JSON 파일 보기 를 선택하고 아래로 스크롤하여 &quot;메시지&quot; 아래에 표시되는 오류 메시지를 복사합니다. 여러 오류 메시지가 표시될 수 있으므로 모두 복사하십시오. 버그 티켓을 기록하려는 동안 Adobe 팀에게 이를 전송하십시오. 이렇게 하면 해결 프로세스가 빨라지고 팀에게 진행 상황에 대한 더 많은 컨텍스트가 제공됩니다.
