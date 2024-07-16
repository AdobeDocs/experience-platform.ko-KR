---
title: AI Assistant의 개인정보 보호, 보안 및 거버넌스
description: AI Assistant의 개인정보 보호, 보안 및 거버넌스 사례에 대해 알아봅니다.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: e14bf4191319d646c6c4bfd55656fc6de141e9ca
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# AI Assistant의 개인정보 보호, 보안 및 거버넌스

Adobe Experience Platform의 AI Assistant는 개인정보 보호, 보안 및 거버넌스를 전면에 내세워 구축되었습니다.

AI Assistant에서 기대할 수 있는 고객 신뢰 중심 기능에 대해 알아보려면 이 문서 를 참조하십시오.

* 현재 AI Assistant는 교육 목적으로도 개인 데이터를 사용하지 않습니다.
* AI 어시스턴트는 소비자 데이터를 인식하지 못합니다.
* 기존의 모든 [액세스 제어](../access-control/home.md) 정책은 AI Assistant에 의해 부여됩니다.
   * 새로운 속성 기반 액세스 제어 정책은 최대 24시간 후에 AI Assistant에 반영됩니다.*
* AI Assistant와 상호 작용하려면 명시적인 권한이 있어야 합니다.
   * [권한 UI](../access-control/abac/ui/permissions.md)를 사용하여 Experience Platform 및 Journey Optimizer에 대한 권한을 다르게 설정할 수 있으며 [Admin Console](../access-control/ui/browse.md)을 사용하여 Customer Journey Analytics에 대한 권한을 할당할 수 있습니다.
   * 권한은 세분화되며 샌드박스 관리자는 다양한 질문 카테고리(AI Assistant를 통한 제품 지식 기반 질문 또는 운영 통찰력에 대한 질문)를 물을 수 있는 사용자를 구성할 수 있습니다.
* AI Assistant는 Adobe Experience Platform Healthcare Shield와 함께 사용할 때 HIPAA에 대비하는 기능입니다.
* 30일 보존 정책으로 AI Assistant와의 이전 상호 작용 로그를 볼 수 있습니다.
* AI Assistant는 사용자 프롬프트에 응답할 때 샌드박스별 데이터 및 공개 Adobe 설명서에 기반합니다. 데이터는 샌드박스 간에 공유되지 않습니다.
* AI Assistant에 제공하는 프롬프트는 다른 고객에게 공유되지 않습니다.

**필드 및 개체에 새 레이블을 추가하거나 새 정책을 만드는 경우 AI Assistant에서 레이블을 적용하는 데 최대 24시간이 소요됨을 의미합니다. 24시간 동안 새로 액세스가 제한된 사용자는 해당 필드와 개체에 계속 액세스할 수 있습니다.*
