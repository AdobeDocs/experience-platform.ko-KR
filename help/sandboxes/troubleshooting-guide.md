---
keywords: Experience Platform;홈;인기 주제;샌드박스 문제 해결
solution: Experience Platform
title: 샌드박스 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform의 샌드박스에 대한 FAQ에 대한 답변을 제공합니다.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 9%

---

# 샌드박스 문제 해결 안내서

이 문서에서는 Adobe Experience Platform의 샌드박스에 대한 FAQ에 대한 답변을 제공합니다. 다른 Experience Platform 서비스와 관련된 질문 및 문제 해결은 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

샌드박스는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할합니다. 자세한 내용은 [샌드박스 개요](home.md)를 참조하십시오.

## 샌드박스란?

샌드박스는 Experience Platform의 단일 인스턴스 내 가상 파티션입니다. 각 샌드박스는 Experience Platform 리소스(스키마, 데이터 세트, 프로필 등)의 자체 독립 라이브러리를 유지 관리합니다. 샌드박스 내에서 수행되는 모든 콘텐츠 및 작업은 해당 샌드박스로만 제한되고 다른 샌드박스에는 영향을 주지 않습니다. 자세한 내용은 [샌드박스 개요](home.md)를 참조하십시오.

## 어떤 유형의 샌드박스를 사용할 수 있으며 차이점은 무엇입니까? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="샌드박스 유형"
>abstract="샌드박스 유형은 프로덕션인지 또는 개발 샌드박스인지 여부를 나타냅니다. 프로덕션 샌드박스에는 라이브 데이터가 포함되고 개발 샌드박스는 테스트와 개발 목적으로 사용됩니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=ko#create" text="UI에서 샌드박스 만들기"

Experience Platform에서는 두 가지 샌드박스 유형을 사용할 수 있습니다.

* **프로덕션 샌드박스**: 프로덕션 샌드박스는 프로덕션 환경의 프로필과 함께 사용됩니다. Experience Platform을 사용하면 운영 격리를 유지하면서 데이터에 적합한 기능을 제공하기 위해 여러 프로덕션 샌드박스를 만들 수 있습니다. 이 기능을 사용하면 특정 프로덕션 샌드박스를 고유한 비즈니스, 브랜드, 프로젝트 또는 지역에 전용으로 지정할 수 있습니다. 프로덕션 샌드박스는 라이선스가 부여된 [!DNL Profile] 약정까지 다양한 프로덕션 프로필을 지원합니다(승인된 모든 프로덕션 샌드박스에서 누적적으로 측정됨). 전체 라이선스 총 데이터 볼륨(인증된 모든 프로덕션 샌드박스에서 누적적으로 측정됨)을 사용할 수 있습니다.

* **개발 샌드박스**: 개발 샌드박스는 비프로덕션 프로필로 개발 및 테스트에만 사용할 수 있는 샌드박스입니다. 개발 샌드박스는 라이선스가 부여된 [!DNL Profile] 약정의 최대 10%까지 비프로덕션 프로필을 지원합니다(승인된 모든 개발 샌드박스에서 누적적으로 측정됨). 최대 다음 권한이 있습니다.
   * 개발 샌드박스당 하루에 한 개의 일괄 처리 세분화 작업
   * 연간 [!DNL Profile]당 평균 120개의 [!DNL Profile] API 호출(승인된 모든 개발 샌드박스에서 누적적으로 측정됨).

자세한 내용은 [샌드박스 개요](./home.md)를 참조하십시오.

## 두 개 이상의 샌드박스에서 리소스에 액세스할 수 있습니까?

샌드박스는 단일 Experience Platform 인스턴스의 격리된 파티션으로, 각 샌드박스는 고유한 리소스 라이브러리를 유지 관리합니다. 샌드박스 유형(프로덕션 또는 비프로덕션)에 관계없이 다른 샌드박스에서 하나의 샌드박스에 있는 리소스에 액세스할 수 없습니다.

## 기본 프로덕션 샌드박스는 무엇입니까?

기본 프로덕션 샌드박스는 조직이 처음 프로비저닝될 때 생성되는 첫 번째 프로덕션 샌드박스입니다. 기본 프로덕션 샌드박스를 사용하면 Experience Platform에서 데이터를 수집하거나 사용할 수 있으며 샌드박스 이름 또는 샌드박스 ID에 대한 값을 포함하지 않는 요청을 수락할 수 있습니다. 기본 프로덕션 샌드박스는 재설정할 수 있지만 삭제할 수는 없습니다.

## 프로덕션 샌드박스는 몇 개까지 사용할 수 있습니까?

Experience Platform 인스턴스는 각 샌드박스가 Experience Platform 리소스(스키마, 데이터 세트 및 프로필 등)의 자체 독립 라이브러리를 유지 관리하는 여러 프로덕션 및 개발 샌드박스를 지원합니다.

기본 Experience Platform 라이선스는 프로덕션 또는 개발로 분류할 수 있는 총 5개의 샌드박스를 부여합니다. 추가 팩 10개, 최대 총 75개의 샌드박스에 대해 라이센스를 부여할 수 있습니다.

프로덕션 샌드박스를 재설정하거나 삭제할 수 있습니다. 단, Adobe Analytics에서 [CDA(Cross Device Analytics)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=ko) 기능을 위해 사용 중이거나, ID 그래프 내에서 호스팅되는 경우 [PBD(People Based Destinations)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=ko) 기능을 위해 Adobe Audience Manager에서 사용됩니다.

프로덕션 샌드박스의 제목을 업데이트할 수 있습니다. 단, 프로덕션 샌드박스의 이름은 변경할 수 없습니다.

>[!NOTE]
>
>샌드박스 이름은 API 호출에서 조회 목적으로 사용되는 반면, 샌드박스 제목은 표시 이름으로 사용됩니다.

## 개발 샌드박스를 몇 개 가질 수 있습니까?

Experience Platform에서는 현재 단일 조직 내에서 최대 75개의 총 샌드박스(프로덕션 및 개발)를 활성화할 수 있습니다.

개발 샌드박스는 재설정 기능과 삭제 기능을 모두 지원합니다.

## 방금 샌드박스를 만들었습니다. 이 샌드박스로 작업할 사용자의 권한을 설정하려면 어떻게 해야 합니까?

Adobe Admin Console은 제품 프로필을 사용하여 사용자를 샌드박스 및 권한으로 연결합니다. 새 샌드박스를 만든 후 액세스 권한을 부여하려는 제품 프로필의 **권한** 탭으로 이동한 다음 **샌드박스**&#x200B;를 클릭합니다. 다른 권한과 동일한 방식으로 새 샌드박스에 대한 액세스를 추가하거나 제거할 수 있습니다.

특정 샌드박스의 사용자에게 고유한 권한을 추가하려면 적절한 샌드박스 및 권한이 적용된 새 제품 프로필을 만들고 해당 사용자를 해당 프로필에 할당해야 할 수 있습니다.

Admin Console에서 샌드박스 및 권한을 관리하는 방법에 대한 자세한 내용은 [액세스 제어 사용 안내서](../access-control/ui/overview.md)를 참조하세요.
