---
title: 이벤트 전달 안내 설정
description: 안내가 있는 설정을 사용하여 이벤트 전달을 설정하는 방법에 대해 알아봅니다.
exl-id: c155dec0-9130-4452-834a-08d98a15b006
source-git-commit: a2dd6b2a5ec8ccf4ca93e845c5b7b2b39d8d1599
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 1%

---

# 이벤트 전달 안내 설정 개요

>[!IMPORTANT]
>
>가이드 설정 기능은 Real-Time CDP Prime 및 Ultimate 패키지를 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>모든 기존 클라이언트는 안내가 있는 설정 워크플로를 사용하여 다음에 사용할 수 있는 참조 구현을 만들 수 있습니다.
>
>* 완전히 새로운 구현의 시작으로 사용하십시오.
>* 이를 참조 구현으로 활용하여 구성 방법을 확인한 다음 현재 프로덕션 구현에서 복제할 수 있습니다.

가이드 설정 기능을 사용하면 쉽고 효율적으로 설정할 수 있습니다. 이 도구는 Adobe 태그 및 이벤트 전달에서 수행되는 여러 단계를 자동화하여 설정 시간을 크게 줄입니다.

이 설치 프로그램은 확장을 자동으로 설치할 수 있습니다. 이 하이브리드 구현은 [!DNL Meta]이(가) 서버측에서 이벤트 변환을 수집하고 전달하는 데 권장됩니다. 안내식 설정 기능은 이벤트 전달 구현을 시작하는 데 도움이 되도록 설계되었으며 모든 사용 사례를 수용하는 완전한 기능의 엔드 투 엔드 구현을 제공하기 위한 것이 아닙니다.

## 가이드 설정 시작 {#guided-setup}

기능을 시작하려면 **[!UICONTROL Get Started]** 데이터 컬렉션 UI에서 **[!UICONTROL Event Forwarding]**&#x200B;을(를) 선택하십시오.

![데이터 컬렉션 UI에서 시작 카드를 표시하는 이벤트 전달 홈 페이지](../../images/ui/guided-setup/get-started.png)

>[!INFO]
>
>데이터 컬렉션 홈 페이지에서 바로 가이드 설정에 액세스할 수도 있습니다.

### 새 태그 속성 만들기 {#new-property}

속성 구성 섹션에서 **[!UICONTROL New]**&#x200B;을(를) 선택하고 새 **[!UICONTROL Property Domain]** 세부 정보를 입력합니다.

![새 도메인 세부 정보를 표시하는 속성 구성](../../images/ui/guided-setup//configure-properties-new.png)

확장 추가 섹션에서 **[!UICONTROL Add]**&#x200B;에 대해 [!DNL Meta Conversion API]을(를) 선택합니다. [!DNL Meta] 정보 구성 페이지에서 **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** 및 **[!UICONTROL Data Layer Path]**&#x200B;을(를) 수동으로 입력할 수 있는 옵션이 있거나 **[!UICONTROL Connect to Meta]** 옵션을 사용할 수 있습니다.

![Meta에 연결 옵션을 표시하는 Meta 정보 페이지 구성](../../images/ui/guided-setup/connect-to-meta.png)

#### 자격 증명을 사용하여 [!DNL Meta]에 연결 {#meta-credentials}

**[!UICONTROL Connect to Meta]**&#x200B;을(를) 선택한 다음 [!DNL Meta] 자격 증명을 입력하고 **[!UICONTROL Log in]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

이제 **비즈니스 포트폴리오 만들기**&#x200B;가 요청됩니다. **[!UICONTROL Business portfolio name]**&#x200B;을(를) 입력하고 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![포트폴리오 이름으로 표시된 비즈니스 포트폴리오 페이지 만들기](../../images/ui/guided-setup/portfolio-name.png)

목록에서 비즈니스 포트폴리오를 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오. Business Portfolio, 광고 계정 및 [!DNL Meta Pixel]에 대한 설정을 볼 수 있습니다. **[!UICONTROL Continue]**&#x200B;을(를) 선택하여 설정을 확인한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

설정 프로세스가 완료될 때까지 잠시 기다린 후 **[!UICONTROL Done]**&#x200B;을(를) 선택하십시오.

**[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** 및 **[!UICONTROL Data Layer Path]**&#x200B;이(가) 자동으로 채워집니다. **[!UICONTROL Save]**&#x200B;를 선택합니다.

![채워진 Meta 정보를 표시하는 Meta 정보 구성](../../images/ui/guided-setup/meta-info.png)

#### 새 태그 속성에 대한 리소스 만들기 {#create-resources}

리소스 만들기 섹션에서 **[!UICONTROL Pre-check resources]**&#x200B;을(를) 선택하여 충돌에 대한 조직 및 속성이나 구현에 필요한 기존 리소스를 확인합니다.

![사전 확인 리소스를 표시하는 리소스 만들기](../../images/ui/guided-setup/pre-check-resources.png)

[작업] 페이지에는 작업 및 작업 목록이 표시됩니다. 이 작업을 만들려면 **[!UICONTROL Create Resources]**&#x200B;을(를) 선택하십시오.

![수행할 작업 및 작업 목록을 표시하는 작업 작업 작업](../../images/ui/guided-setup/create-resources.png)

필요한 규칙, 데이터 요소, 확장, 라이브러리, SDK 등에 대해 몇 분 정도 기다린 후 설치를 완료합니다. 리소스 만들기 섹션에서는 만든 속성 및 리소스에 대한 링크를 제공합니다.

#### 구현의 유효성 검사 {#validate-implementation}

구현 유효성 검사 섹션은 웹 사이트에서 사용할 수 있는 포함 링크를 제공합니다. **[!UICONTROL Start Validation]**&#x200B;은(는) 이 안내 설정 페이지의 현재 브라우저 세션에서 테스트를 실행합니다. 여기에서 유효성 검사가 성공하면 사이트에 포함 링크를 배포할 때 동일한 구현이 작동해야 합니다.

Adobe Experience Platform Edge Network을 통해 테스트 이벤트를 전송하려면 **[!UICONTROL Send PageView Event]**&#x200B;을(를) 선택하십시오. 그런 다음 서버측에서 [!DNL Meta]&#x200B;(으)로 전달됩니다. **[!UICONTROL Finished Validation]**&#x200B;을(를) 선택하여 설치를 완료합니다.

>[!NOTE]
>
>유효성 검사 프로세스 중에 오류가 발생하는 경우 **[!UICONTROL Assurance]** 링크를 선택하여 오류가 발생했을 수 있는 이벤트를 검토하십시오.

![유효성 검사 결과를 표시하는 유효성 검사 페이지](../../images/ui/guided-setup/finished-validation.png)

### 기존 태그 속성 사용 {#existing-property}

속성 구성 섹션에서 **[!UICONTROL Existing]**&#x200B;을(를) 선택한 다음 드롭다운 메뉴에서 태그 속성을 선택합니다. 시스템에서는 데이터 스트림을 통해 이 속성에 이미 첨부된 이벤트 전달 속성을 찾으려고 합니다. 이제 [!DNL Meta Conversion API]을(를) 계속 다시 구성한 다음 미리 확인하고 리소스를 만들 수 있습니다.

![선택한 기존 태그 속성을 표시하는 기존 속성 구성](../../images/ui/guided-setup/configure-properties-existing.png)

선택한 태그 속성이 이벤트 전달 속성에 연결되어 있지 않거나 데이터 스트림이 누락된 경우 자동으로 생성됩니다.

![선택한 기존 태그 속성을 표시하는 기존 속성 구성](../../images/ui/guided-setup/configure-properties-existing-no-event-fw.png)

[!DNL Meta Conversion API]을(를) 구성하려면 [연결 대상 [!DNL Meta] 자격 증명을 사용](#meta-credentials)에서 위에 강조 표시된 프로세스를 따르십시오.

**[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** 및 **[!UICONTROL Data Layer Path]**&#x200B;을(를) 생성했으므로 이제 **[!UICONTROL Pre-Check resources]**&#x200B;을(를) 선택하여 이벤트 전달 워크플로를 만듭니다.

기존 태그 속성을 사용하고 있으므로 설정 프로세스는 새 속성 워크플로와 약간 다릅니다. 웹 속성, 호스트 및 환경이 이미 있으므로 시스템이 해당 웹 속성, 호스트 및 환경 만들기를 건너뜁니다. 마지막으로 **[!UICONTROL Create Resources]**&#x200B;을(를) 선택하여 아직 사용할 수 없는 작업을 만듭니다.

![건너뛸 작업 및 작업 목록을 표시하는 작업 동작](../../images/ui/guided-setup/create-resources-skip.png)

>[!INFO]
>
>안내식 설정은 프로세스 중에 업데이트되는 속성에 메모를 자동으로 추가합니다. 편집 모드에 있을 때 태그 속성의 오른쪽 패널에 있는 노트 섹션에서 이를 볼 수 있습니다. 안내식 설정 도구를 통해 속성을 업데이트하거나 만든 시기를 확인할 수 있습니다. 이 감사 추적을 사용하면 안내가 있는 설정 기능으로 수정된 사항을 추적할 수 있습니다.

필요한 규칙, 데이터 요소, 확장, 라이브러리, SDK 등에 대해 몇 분 정도 기다린 후 설치를 완료합니다. 리소스 만들기 섹션에서는 만든 속성 및 리소스에 대한 링크를 제공합니다.

구현 유효성 검사 섹션은 웹 사이트에서 사용할 수 있는 포함 링크를 제공합니다. **[!UICONTROL Start Validation]**&#x200B;은(는) 이 안내 설정 페이지의 현재 브라우저 세션에서 테스트를 실행합니다. 여기에서 유효성 검사가 성공하면 사이트에 포함 링크를 배포할 때 동일한 구현이 작동해야 합니다.

Adobe Experience Platform Edge Network을 통해 테스트 이벤트를 전송하려면 **[!UICONTROL Send PageView Event]**&#x200B;을(를) 선택하십시오. 그런 다음 서버측에서 [!DNL Meta]&#x200B;(으)로 전달됩니다. **[!UICONTROL Finished Validation]**&#x200B;을(를) 선택하여 설치를 완료합니다.

>[!NOTE]
>
>유효성 검사 프로세스 중에 오류가 발생하는 경우 **[!UICONTROL Assurance]** 링크를 선택하여 오류가 발생했을 수 있는 이벤트를 검토하십시오.

![유효성 검사 결과를 표시하는 유효성 검사 페이지](../../images/ui/guided-setup/finished-validation.png)

## 다음 단계 {#next-steps}

이 안내서에서는 안내식 설치 도구를 사용하여 [!DNL Meta Conversions API]에 대한 속성을 만들고 구성하는 방법에 대해 설명합니다.

통합을 효과적으로 구현하는 방법에 대한 자세한 지침은 [!DNL Meta]의 모범 사례[&#x200B; [!DNL Conversions API]에 대한 &#x200B;](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 설명서를 참조하십시오. Adobe Experience Cloud의 태그 및 이벤트 전달에 대한 자세한 내용은 [태그 개요](../../home.md)를 참조하세요.
