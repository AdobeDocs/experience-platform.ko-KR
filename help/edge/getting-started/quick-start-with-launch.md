---
title: 빠른 시작
seo-title: Adobe Experience Platform 웹 SDK 빠른 시작(Launch)
description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터 수집을 위한 빠른 시작 가이드
seo-description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터 수집을 위한 빠른 시작 가이드
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (베타) 사전 요구 사항

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

현재 Adobe Experience Platform Web SDK는 XDM을 사용하여 Adobe Experience Platform으로 데이터를 전송하는 것만 지원합니다. 다음 전제 조건을 충족해야 합니다.

- 자사 [도메인(CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) 이 활성화되어 있어야 합니다. 이미 Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다.
- Adobe Experience Platform 이용 권한 부여
- 최신 버전의 방문자 ID 서비스 사용

## 플랫폼 준비

Adobe Experience Platform으로 데이터를 전송하려면 XDM 스키마와 해당 스키마를 사용하는 데이터 세트를 만들어야 합니다.

- [다음과 같은 혼합으로 스키마를](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) 만듭니다.
   - ExperienceEvent 구현 세부 사항
   - ExperienceEvent 환경 세부 사항
   - ExperienceEvent 웹 세부 사항
- 만든 스키마에 Adobe Experience Platform 웹 SDK 믹신 추가
- [데이터를 배치할 스키마로 데이터 집합](https://platform.adobe.com/dataset/overview) 만들기

## 구성 ID 요청

SDK를 사용하려면 구성 ID가 있어야 합니다. 구성 ID를 사용하면 데이터가 올바른 위치로 라우팅됩니다. 컨설턴트나 Client Care를 통해 구성 ID를 얻을 수 있습니다. 이러한 사용자는 다음 정보가 필요합니다.

- **조직 ID:** 이 방법은 [여기에서 지침을 참조하십시오](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **데이터 집합 ID:** 데이터 세트를 클릭하면 데이터 세트 UI에서 사용할 수 있습니다
- **스키마 ID:** 스키마 생성 화면의 URL에서 사용할 수 있습니다.
- **친숙한 이름:** 이 구성에 대해 향후 UI에서 사용할 친숙한 이름입니다.

## Launch에서 SDK 설치

Launch에 로그인하여 `AEP Web SDK` 익스텐션을 설치합니다. SDK 설치의 일부로 확장을 구성하라는 메시지가 표시됩니다. 위에서 요청한 구성 ID를 입력합니다. 익스텐션은 조직 ID를 자동으로 채웁니다.

다양한 구성 옵션에 대한 자세한 내용은 SDK [구성을 참조하십시오](../fundamentals/configuring-the-sdk.md).

## 이벤트 보내기

익스텐션이 설치되면 AEP 웹 SDK 익스텐션에서 &quot;비콘 전송&quot; 동작을 추가하여 이벤트 전송을 시작합니다. &quot;보기 시작 시 발생&quot; 옵션이 선택된 상태로 페이지가 로드될 때마다 하나 이상의 이벤트를 보내는 것이 좋습니다.

이벤트를 추적하는 방법에 대한 자세한 내용은 이벤트 [추적을 참조하십시오](../fundamentals/tracking-events.md).

## 데이터 보내기

이전에 만든 스키마와 일치하는 데이터를 이벤트와 함께 보낼 수 있습니다. 예를 들어, 상거래 사이트를 소유하고 있고 상거래 믹스를 스키마에 추가한 경우 다른 사람이 제품을 볼 때 다음 구조를 보냅니다.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
