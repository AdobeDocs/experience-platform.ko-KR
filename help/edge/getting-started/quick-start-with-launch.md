---
title: 빠른 시작
seo-title: Adobe Experience Platform 웹 SDK 빠른 시작(Launch)
description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
seo-description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
translation-type: tm+mt
source-git-commit: 51acb07efe624c7cf1dfaabc4b03f04c76ac88f8
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 4%

---


# (베타) 사전 요구 사항

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

현재 Adobe Experience Platform 웹 SDK는 XDM을 사용하여 Adobe Experience Platform으로 데이터 전송을 지원합니다. 다음 전제 조건을 충족해야 합니다.

- 자사 도메인(CNAME)이 [활성화되어 있어야](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) 합니다. 이미 Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다.
- Adobe Experience Platform 이용 권한 부여
- 최신 버전의 방문자 ID 서비스 사용

## 플랫폼 준비

Adobe Experience Platform으로 데이터를 전송하려면 XDM 스키마 및 해당 스키마를 사용하는 데이터 세트를 만들어야 합니다.

- [스키마 만들기](../../xdm/tutorials/create-schema-ui.md)
- 만든 스키마에 Adobe Experience Platform 웹 SDK 믹신 추가
- [데이터](https://platform.adobe.com/dataset/overview) 육지에 사용할 스키마로 데이터 집합 만들기

## 구성 ID 만들기

실행 시 [에지 구성 도구를 사용하여 구성 ID를](../fundamentals/edge-configuration.md) 만들 수 있습니다.

>참고: 이 기능을 사용하려면 조직에서 허용 목록에 포함되어야 합니다. 최종 허용 목록에 포함하려면 CSM에 문의하십시오.

## Launch에서 SDK 설치

Launch에 로그인하여 `AEP Web SDK` 익스텐션을 설치합니다. SDK 설치 시 익스텐션을 구성하라는 메시지가 표시됩니다. 위에 요청한 구성 ID를 입력합니다. 익스텐션은 조직 ID에 자동으로 채워집니다.

다양한 구성 옵션에 대한 자세한 내용은 SDK [구성을 참조하십시오](../fundamentals/configuring-the-sdk.md).

## 이벤트 보내기

익스텐션이 설치되면 AEP 웹 SDK 익스텐션에서 &quot;비콘 전송&quot; 동작을 추가하여 이벤트 전송을 시작합니다. &quot;보기 시작 시 발생&quot; 옵션이 선택된 상태로 페이지가 로드될 때마다 하나 이상의 이벤트를 전송하는 것이 좋습니다.

이벤트를 추적하는 방법에 대한 자세한 내용은 이벤트 [추적을 참조하십시오](../fundamentals/tracking-events.md).

## 데이터 전송

이전에 만든 스키마와 일치하는 데이터를 이벤트와 함께 보낼 수 있습니다. 예를 들어 상거래 사이트를 소유하고 있고 상거래 믹스를 스키마에 추가한 경우 사용자가 제품을 볼 때 다음 구조가 전송됩니다.

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
