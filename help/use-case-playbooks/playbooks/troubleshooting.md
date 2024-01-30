---
solution: Experience Platform
title: 플레이북의 알려진 제한 사항 및 문제 해결
description: 플레이북의 알려진 문제 및 일반적인 문제와 이러한 문제를 해결하는 방법에 대해 자세히 알아보십시오
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# 문제 해결 및 알려진 제한 사항 {#troubleshooting-known-limitations}

## 문제 해결 {#troubleshooting}

### Adobe Journey Optimizer 표면이 구성되지 않음

플레이북의 인스턴스를 만들 때 아래 메시지가 표시될 수 있습니다.

![문제 해결](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

이는 Journey Optimizer 플레이북이 이메일, 푸시 및 SMS 채널에 대한 메시지를 만들기 때문입니다. 읽기 [시작하기](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) 안내서를 사용하여 여러 서피스를 구성할 수 있습니다.

### 상태 *실패* 새 인스턴스 생성 시

인스턴스를 만들려고 할 때 실패 메시지가 표시되는 경우, 관리자가 사용자에게 필요한 사용자 권한을 부여하지 않았기 때문일 수 있습니다. 플레이북에는 다양한 에셋이 포함되어 있으며 사용자가 플레이북의 인스턴스를 성공적으로 만들려면 해당 에셋을 만들 수 있는 권한이 필요합니다. 다음을 참조하십시오. [권한](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 권한 설정 방법에 대한 이 안내서의 섹션입니다.

## 알려진 제한 사항

플레이북의 인스턴스를 만들고 에셋을 생성하면 알려진 두 가지 제한 사항이 표시됩니다.

* 생성된 스키마의 경우 플레이북의 한 인스턴스에서 스키마가 생성되고 사용자가 편집하는 경우 다른 스키마가 생성됩니다 *다음이 아님* 플레이북의 다른 인스턴스를 활성화하면 생성됩니다. 대신, 인스턴스 내에서도 편집한 스키마를 계속 사용하십시오.

* 사용 시 [데이터 인식 기능](/help/use-case-playbooks/playbooks/data-awareness.md) 영감을 주는 샌드박스에서 개발 샌드박스로 스키마를 홍보하기 위해 다음과 유사한 오류가 표시될 수 있습니다.

![스키마 오류](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

이는 스키마에서 생성된 필드 중 일부가 복사 중인 개발 샌드박스의 스키마에 없기 때문입니다. 그 필드들이 무엇인지 찾아보세요. 그런 다음 다음을 수행할 수 있는 개발 샌드박스로 돌아갑니다.

* 해당 필드를 포함하는 새 필드 그룹을 만들거나
* 누락된 필드를 포함하는 표준 사전 정의된 필드 그룹을 스키마에 포함합니다.

개발 샌드박스의 스키마에 해당 필드를 포함시킨 후 워크플로우로 돌아가 영감을 주는 샌드박스에서 개발 샌드박스로 스키마 필드를 복사합니다. 이제 오류가 사라졌습니다.

자세한 내용은 아래 비디오를 통해 스키마 필드 그룹을 만드십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
