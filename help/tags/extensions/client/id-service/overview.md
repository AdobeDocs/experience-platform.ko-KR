---
title: Adobe Experience Cloud Identity 서비스 확장 개요
description: Adobe Experience Platform의 Adobe Experience Cloud Identity 서비스 태그 확장에 대해 알아봅니다.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 77%

---

# Adobe Experience Cloud Identity 서비스 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe Experience Cloud ID 확장 구성 및 이 확장을 사용하여 규칙을 작성할 때 사용할 수 있는 옵션에 대한 정보를 보려면 이 참조를 사용하십시오.

이 확장을 사용하여 Experience Cloud Identity 서비스를 속성과 통합합니다. Experience Cloud Identity 서비스를 사용하여 사이트 방문자에 대해 고유하고 영구적인 식별자를 만들고 저장할 수 있습니다.

## Experience Cloud ID 확장 구성

이 섹션에서는 Experience Cloud ID 확장을 구성할 때 사용할 수 있는 옵션에 대한 참조를 제공합니다.

Experience Cloud ID 확장이 아직 설치되지 않은 경우 속성을 연 다음, 를 선택합니다 **[!UICONTROL Extensions > Catalog]**&#x200B;를 마우스로 가리킨 다음 Experience Cloud ID 확장을 마우스로 가리킨 다음 을 선택합니다 **[!UICONTROL 설치]**.

확장을 구성하려면 Extensions 탭을 열고 확장을 마우스로 가리킨 다음 을 선택합니다 **[!UICONTROL 구성]**.

![](../../../images/optin.jpg)

다음 구성 옵션을 사용할 수 있습니다.

### Experience Cloud 조직 ID

Experience Cloud 조직의 ID입니다.

ID는 24자의 영숫자 문자열과 그 뒤에 오는 `@AdobeOrg`로 구성됩니다. 이 ID를 모를 경우 고객 지원 센터에 문의하십시오.

### 특정 경로 제외

URL이 지정된 경로와 일치하는 경우 Experience Cloud ID가 로드되지 않습니다.

(선택 사항) 정규 표현식인 경우 Regex를 활성화합니다.

선택 **[!UICONTROL 추가]** 다른 경로를 제외하려면 다음을 수행하십시오.

### 옵트인

옵트인 옵션을 사용하여 방문자의 활동을 추적하는 쿠키를 만들지 여부를 포함하여 방문자가 사이트에서 Adobe 서비스를 옵트인해야 하는지 여부를 결정합니다.

옵트인은 모든 플랫폼 솔루션 클라이언트측 라이브러리에 대한 중앙 참조점으로, 사용자가 사이트를 방문할 때 사용자의 장치나 브라우저에 쿠키를 만들 수 있는지 여부를 결정합니다. 옵트인은 사용자 동의 기본 설정을 수집하거나 저장하는 기능을 지원하지 않습니다.

**Enable Opt In?**

선택한 옵션은 웹 사이트에서 사이트에서의 방문자 활동 추적에 동의할 때까지 기다리는지 여부를 결정합니다.

다음 세 가지 옵션을 사용할 수 있습니다.

* **No:** 방문자 추적에 동의할 때까지 기다리지 않습니다. 옵션을 선택하지 않으면 기본 동작입니다.
* **Yes:** 방문자 추적에 동의할 때까지 기다립니다.
* **Determined at runtime using function:** 런타임 시 값이 true 또는 false인지를 프로그래밍 방식으로 결정합니다. 이 옵션을 선택하면 Select Data Element 필드를 사용할 수 있습니다. 동의할 때까지 기다릴 것인지 여부를 결정할 수 있는 데이터 요소를 선택합니다. 이 데이터 요소는 부울 값으로 확인됩니다. 예를 들어 방문자의 국가가 EU에 있는지 여부에 대해 결정된 동의를 제공하는 데이터 요소를 선택할 수 있습니다.

**Is Opt In Storage Enabled?**

활성화된 경우 동의가 도메인의 자사 쿠키에 저장됩니다. 활성화되지 않은 경우에는 동의 설정이 CMP 또는 관리하는 쿠키에 유지됩니다.

**Opt In Cookie Domain?**

이 선택적 설정을 사용하여 저장소가 활성화된 경우 옵트인 쿠키가 저장되는 도메인을 지정합니다. 도메인을 입력하거나 도메인을 포함하는 데이터 요소를 선택할 수 있습니다.

**Opt In Storage Expiry?**

저장소가 활성화된 경우 옵트인 쿠키가 만료되는 시간을 초 단위로 지정합니다.

숫자를 입력한 다음 드롭다운 목록에서 시간 단위를 선택합니다. 예를 들어, 2를 입력하고 를 선택합니다 **[!UICONTROL 주]**. 기본값은 13개월입니다.

**권한?**

옵트인 라이브러리에 이전 동의를 전달합니다. 동의가 들어 있는 데이터 요소를 선택합니다. 요소 유형은 개체 또는 JSON 문자열이어야 합니다. Pre Opt In Approvals을 무시합니다.

예:

`"{"aa":true,"aam":true,"ecid":true}"`

**Pre Opt In Approvals?**

방문자가 기본 설정을 지정하지 않은 경우 승인하거나 거부할 카테고리를 정의합니다. 동의는 페이지가 로드되는 시간부터 선택한 솔루션에 대해 간주됩니다. 요소 유형은 개체 또는 JSON 문자열이어야 합니다(예: `{aam: true}`).

### 변수

이름-값 쌍을 Experience Cloud ID 인스턴스 속성으로 설정합니다. 드롭다운을 사용하여 변수를 선택한 다음 값을 입력하거나 선택합니다. 각 변수에 대한 자세한 내용은 [Experience Cloud Identity Service 설명서](https://experiencecloud.adobe.com/resources/help/ko_KR/mcvid/mcvid-overview.html).

## Experience Cloud ID 확장 작업 유형

이 섹션에서는 Experience Cloud ID 확장에서 사용할 수 있는 작업 유형을 설명합니다.

### 작업 유형

#### 고객 ID 설정

하나 이상의 고객 ID를 설정합니다.

1. 통합 코드를 입력합니다.

   통합 코드에는 Audience Manager 또는 고객 특성에 데이터 소스로 설정된 값이 포함되어 있어야 합니다.

1. 값을 선택합니다.

   값은 사용자 ID여야 합니다. 데이터 요소는 클라이언트별 내부 시스템의 ID와 같이 동적 값에 가장 적합합니다.

1. 인증 상태를 선택합니다.

   사용 가능한 옵션은 다음과 같습니다.

   * 알 수 없음
   * Authenticated
   * 로그아웃됨

1. (선택 사항) 선택 **[!UICONTROL 추가]** 추가 고객 ID를 설정하는 중입니다.
1. 선택 **[!UICONTROL 변경 내용 유지]**.
