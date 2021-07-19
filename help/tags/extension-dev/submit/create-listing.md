---
title: 확장에 대한 Exchange 목록 만들기
description: Adobe Experience Platform의 공개 카탈로그에 확장을 추가하는 방법을 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 28%

---

# 확장에 대한 Exchange 목록 만들기

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../term-updates.md)을 참조하십시오.

Adobe Experience Platform에는 사용자가 설치를 위해 사용할 수 있는 태그 확장을 볼 수 있는 단일 통합 카탈로그가 있습니다. 이 카탈로그는 제품 내에서 사용할 수 있으며 다음 세 가지 유형의 확장을 포함합니다.

1. **공개 확장**: 이는 모든 사용자가 프로덕션 사용을 위해 디자인된 완성된 확장입니다.
1. **비공개 확장**: 이러한 확장은 프로덕션에 맞게 디자인되었지만 회사의 다른 사용자가 개발했으며 회사 내의 사용자만 사용할 수 있습니다.
1. **개발 확장**: 이러한 확장은 현재 개발 중이며 회사 내에서만 사용할 수 있으며, 개발 속성으로 특별히 지정된 자산에서만 사용할 수 있습니다.

제품 카탈로그의 확장과 별도로 일부 확장에도 [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product)에 목록이 있습니다.

이러한 목록을 통해 확장 개발자는 기능에 대한 설명을 게시하고, 추가 지원 및 설명서에 대한 링크를 제공하며, 회사 또는 확장의 기능을 알지 못할 가능성이 있는 사용자에게 확장을 마케팅할 수 있습니다. 이 마켓플레이스에서 확장은 Platform에 대한 인증을 받지 않은 사용자가 볼 수 있는 공개 목록을 가질 수 있습니다.  많은 개발자들이 Exchange 목록을 개발하는 것이 유용하다고 판단하지만 이는 필수 단계는 아닙니다.

확장 패키지를 업로드하고 테스트할 회사가 없는 경우 Exchange 프로그램에 등록하고 목록을 시작해야 합니다.  이렇게 하면 회사 계정 생성이 트리거됩니다(시간이 오래 걸리며 이 작업이 완료되면 이메일을 받게 됨). 확장을 업로드하고 테스트하는 데 사용할 수 있습니다.  그 목록을 공개시킬 필요는 없다.

이미 회사 계정이 있거나 목록을 완료할 계획이 없는 경우 이 단계의 나머지 작업을 건너뛰고 [확장 업로드 및 테스트](./upload-and-test.md)로 진행할 수 있습니다.

## 목록 만들기

>[!NOTE]
>
>다음 프로세스는 Exchange Adobe 프로그램에서 응용 프로그램 목록 만들기에 대해 자세히 설명합니다. Adobe Experience Platform의 다양한 통합 및 확장에 사용되는 용어입니다.

![앱 관리자 링크 위치 Experience Cloud](../images/getting-started/app-mgr-link.png)

1. [Exchange Partner 사이트](https://partners.adobe.com/exchangeprogram/experiencecloud)에 로그인합니다. 로그인하고 나면 이름 옆에 있는 **App Manager** 링크를 선택합니다.
1. **새 애플리케이션 만들기** 탭을 선택한 다음 사용자 지정된 솔루션에 대해 **새 앱 만들기**&#x200B;를 선택하거나 적용 가능한 템플릿을 선택합니다.
1. 목록 정보를 제공합니다. App Manager에 대한 자세한 내용은 전체 [문서](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931)를 참조하십시오. 목록 정보는 확장의 기능 및 이 확장이 유용한 이유에 대해 매우 명확히 해야 합니다. 목록은 앱의 마케팅 공간 역할을 합니다. 명확한 설명, 사이트의 랜딩 페이지에 대한 링크, 도움말 문서에 대한 링크 또는 지원 이메일 주소 등을 사용하여 여기서 확장을 프로모션합니다. 확장 보기의 공간이 제한되어 있지만 Exchange 목록은 확장과 회사를 모두 홍보할 수 있는 기회를 제공합니다. 다음은 확장의 프로모션을 개선하기 위한 제안 사항입니다.
   - **앱 아이콘** - Exchange 목록의 아이콘에 적합한 크기로, png의 경우 512 x 512 또는 jpg의 1:1 종횡비여야 합니다.

   >[!NOTE]
   >
   >확장 코드에서 사용되는 것과 다른 파일 형식입니다. 확장 자체에는 svg 파일이 [아이콘](../manifest.md)으로 포함됩니다.
   
   - **주요 이미지**  - 독립 실행형 이미지를 사용하여 브랜드를 표시하고 애플리케이션을 강조할 수 있습니다. 주요 이미지는 Exchange 목록에 대한 링크 또는 소셜 미디어에서 게시물에 대한 링크를 공유할 때 표시되는 이미지입니다. 따라서 브랜드를 대표할 수 있어야 합니다.
   - **앱 게시자의 로고** - 회사의 로고이며, 아이콘 크기가 1280 x 720 또는 2560 x 1440(16:9)인 png 또는 jpg 포맷인지 확인하십시오.
   - **구성 지침**  - Adobe Experience Platform 확장을 구성하는 방법을 고객에게 설명합니다. 속성에 확장을 설치한 직후에 [구성 보기](../configuration.md)가 나타날 때 필요한 설정과 다음 단계를 이해하는지 확인합니다. 
   - **태그** - 목록을 편집하는 첫 번째 페이지에서 &#39;사용자 지정 태그&#39; 필드에 &quot;Launch&quot;라는 단어를 포함해야 합니다. 그러면 Exchange 마켓플레이스의 태그 검색에 목록이 표시됩니다.
      ![](../images/getting-started/custom-tags.jpg)
   - **샌드박스**  - Adobe 솔루션에 대한 액세스는 Adobe Experience Platform의 완전히 작동하는 버전에 액세스할 수 있는 샌드박스 계정을 통해 수행됩니다. 이러한 Sandbox 계정은 애플리케이션 목록을 만들 때 요청할 수 있습니다. **연결** 섹션에서, 만든 애플리케이션(태그 확장)에 적용할 수 있는 특정 연결을 선택하고 **저장**&#x200B;을 누르면 필요한 경우 Sandbox 요청이 생성됩니다.
1. 목록을 제출하십시오. Adobe Exchange 팀이 애플리케이션을 검토하고 업데이트가 필요한 경우 피드백을 제공합니다. 목록을 제출할 때 **즉시 게시** 확인란을 선택하면 승인 즉시 게시됩니다. 나중에 애플리케이션을 게시하려면 확인란을 선택 취소합니다. 확장 목록이 승인되면 앱(확장) 목록 페이지의 해당 단추 옆에 파란색 **게시** 단추가 표시됩니다.

### 유효한 목록 만들기

가장 매력적인 목록을 만드는 방법에 대한 자세한 내용은 [앱 제출 가이드라인](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html)을 참조하십시오.

#### Exchange 목록을 제출한 후

제출되면, Adobe Exchange 팀이 애플리케이션을 검토하고 애플리케이션을 승인하거나 변경 사항에 대한 의견을 제출합니다. 이 프로세스는 앱 제출 가이드라인에 자세히 설명되어 있습니다.

Exchange 사이트에 로그인하지 않은 경우 [프로그램 등록 안내서](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html)의 지침에 따라 Exchange 프로그램에 이메일이 등록되어 있는지 확인합니다. 각 사용자는 자신의 이메일을 회사의 파트너 계정과 연결해야 합니다. 이 프로세스에 대한 질문이 이메일을 통해 <ExchangeHelpEC@adobe.com>으로 전송될 수 있습니다.

#### 초기 승인 후 Exchange 목록 업데이트

확장을 업데이트하거나 Exchange 목록을 업데이트해야 하는 경우 [Partner Portal](https://partners.adobe.com/exchangeprogram/experiencecloud)에 로그인한 다음 이름 옆에 있는 App Manager 버튼을 선택합니다. 그런 다음 애플리케이션을 선택하고 목록을 만드는 데 처음 사용한 위의 흐름을 따릅니다. 다시 제출하면 Adobe Exchange 팀이 변경 내용을 검토하고 변경 내용을 승인하거나 변경 내용에 대한 의견을 제공합니다.

## 목록에 확장 패키지를 연결합니다

목록이 승인되고 공개적으로 사용 가능한 경우, 확장 패키지 내의 `extension.json` 파일의 `exchange_url` 필드에 공개 목록에 대한 링크를 제공하는 것이 좋습니다.  이렇게 하면 Platform launch 확장 카탈로그 내에 &quot;추가 정보&quot; 링크가 생성되므로 제품 내의 사용자가 목록을 찾을 수 있고 추가 정보가 있습니다.
