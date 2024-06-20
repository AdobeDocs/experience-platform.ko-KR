---
solution: Experience Platform
title: 플레이북의 알려진 제한 사항
description: 플레이북의 알려진 문제 및 일반적인 문제와 이러한 문제를 해결하는 방법에 대해 자세히 알아보십시오
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# 알려진 제한 사항 {#known-limitations}

사용 사례 플레이북으로 작업할 때 발생하는 오류를 해결하는 방법을 알아보고, 일반 가용성 릴리스의 알려진 제한 사항을 이해합니다.

## 알려진 제한 사항

플레이북의 인스턴스를 만들고 에셋을 생성하면 알려진 두 가지 제한 사항이 표시됩니다.

* 생성된 스키마의 경우 플레이북의 한 인스턴스에서 스키마가 생성되고 사용자가 편집하는 경우 다른 스키마가 생성됩니다 *다음이 아님* 플레이북의 다른 인스턴스를 활성화하면 생성됩니다. 대신, 인스턴스 내에서도 편집한 스키마를 계속 사용하십시오.

* 사용 시 [데이터 인식 기능](/help/use-case-playbooks/playbooks/data-awareness.md) 영감을 주는 샌드박스에서 개발 샌드박스로 스키마를 홍보하기 위해 다음과 유사한 오류가 표시될 수 있습니다.

![스키마 매핑 워크플로에 표시되는 오류.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

이는 스키마에서 생성된 필드 중 일부가 복사 중인 개발 샌드박스의 스키마에 없기 때문입니다. 그 필드들이 무엇인지 찾아보세요. 그런 다음 다음을 수행할 수 있는 개발 샌드박스로 돌아갑니다.

* 해당 필드를 포함하는 새 필드 그룹을 만들거나
* 누락된 필드를 포함하는 표준 사전 정의된 필드 그룹을 스키마에 포함합니다.

개발 샌드박스의 스키마에 해당 필드를 포함시킨 후 워크플로우로 돌아가 영감을 주는 샌드박스에서 개발 샌드박스로 스키마 필드를 복사합니다. 이제 오류가 사라졌습니다.

자세한 내용은 아래 비디오를 통해 스키마 필드 그룹을 만드십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
