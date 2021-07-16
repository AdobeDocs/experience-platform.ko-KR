---
title: 확장 릴리스
description: Adobe Experience Platform에서 태그 확장을 비공개 또는 공개적으로 릴리스하는 방법을 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 39%

---

# 확장 릴리스

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

테스트 및 문서화가 완료되면 확장을 릴리스할 수 있습니다. 현재 수행할 수 있는 릴리스 유형은 다음의 두 가지입니다.

- **비공개 릴리스**: 완성된 확장을 회사 내의 모든 속성에 사용할 수 있지만 Adobe Experience Platform의 다른 회사에는 사용할 수 없습니다.
- **공개 릴리스**: 완성된 확장을 모든 Adobe Experience Platform 사용자의 공용 마켓플레이스에서 사용할 수 있습니다.

>[!NOTE]
>
>확장을 릴리스한 후에는 더 이상 변경할 수 없으며 릴리스를 취소할 수 없습니다.  릴리스한 이후에는 확장 패키지의 새 버전을 `POST`하고 해당 새 버전에 대한 위의 테스트 및 릴리스 단계를 따라 버그 수정 및 기능 추가 기능을 수행합니다.

확장을 공개하려면 먼저 확장을 비공개 확장으로 릴리스해야 합니다.

## 비공개 릴리스

비공개 릴리스로 확장을 릴리스하기 위한 가장 쉬운 방법은 [태그 확장 릴리스](https://www.npmjs.com/package/@adobe/reactor-releaser)를 사용하는 것입니다. 자세한 지침은 해당 설명서에서 제공됩니다.

API를 사용하여 확장을 직접 사용 가능한 상태로 전환하려면 API 문서에서 [확장 패키지](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/)에 대한 예제 호출을 참조하십시오.

## 공개 릴리스

비공개 릴리스를 완료하면 Adobe에 공개적으로 릴리스하도록 요청할 수 있습니다.  그러면 공개 카탈로그에서 확장을 사용할 수 있게 됩니다. 모든 데이터 수집 사용자는 모든 속성에 확장을 설치할 수 있습니다.

릴리스 프로세스를 시작하려면 [공개 릴리스 요청 양식](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U)을 작성해 주십시오.
