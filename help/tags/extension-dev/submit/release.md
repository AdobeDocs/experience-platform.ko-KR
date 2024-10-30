---
title: 확장 릴리스
description: Adobe Experience Platform에서 태그 확장을 비공개 또는 공개적으로 릴리스하는 방법을 알아봅니다.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 2152cf98d9809654cca7abd7b8469a72e8387b2a
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 25%

---

# 확장 릴리스

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

테스트 및 문서화가 완료되면 확장을 릴리스할 수 있습니다. 현재 수행할 수 있는 릴리스 유형은 다음의 두 가지입니다.

- **비공개 릴리스**: 완성된 확장을 회사 내의 모든 속성에 사용할 수 있지만 Adobe Experience Platform의 다른 회사에는 사용할 수 없습니다.
- **공개 릴리스**: 완성된 확장을 모든 Adobe Experience Platform 사용자의 공용 마켓플레이스에서 사용할 수 있습니다.

>[!NOTE]
>
>확장을 릴리스한 후에는 더 이상 변경할 수 없으며 릴리스를 취소할 수 없습니다.  릴리스한 이후에는 확장 패키지의 새 버전을 `POST`하고 해당 새 버전에 대한 위의 테스트 및 릴리스 단계를 따라 버그 수정 및 기능 추가 기능을 수행합니다.

확장을 공개하려면 먼저 확장을 비공개 확장으로 릴리스해야 합니다.

## 비공개 릴리스

비공개 릴리스로 확장을 릴리스하는 가장 쉬운 방법은 [태그 확장 releaser](https://www.npmjs.com/package/@adobe/reactor-releaser)를 사용하는 것입니다.

```bash
npx @adobe/reactor-releaser
```

`npx`을(를) 사용하면 npm 패키지를 컴퓨터에 실제로 설치하지 않고도 다운로드하여 실행할 수 있습니다. 이 방법은 릴리스를 실행하는 가장 간단한 방법입니다.

>[!NOTE]
> 기본적으로 릴리스에는 서버 간 Oauth 흐름에 대한 Adobe I/O 자격 증명이 필요합니다. 기존 `jwt-auth` 자격 증명
> 2025년 1월 1일에 사용이 중단될 때까지 `npx @adobe/reactor-releaser@v3.1.3`을(를) 실행하여 사용할 수 있습니다. 필요한 매개 변수
> `jwt-auth` 버전을 실행하려면 [여기](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5)에 있습니다.

릴리스에는 몇 가지 정보만 입력해야 합니다. Adobe I/O 콘솔에서 `clientId` 및 `clientSecret`을(를) 검색할 수 있습니다. I/O 콘솔에서 [통합 페이지](https://console.adobe.io/integrations)(으)로 이동합니다. 드롭다운에서 올바른 조직을 선택하고 올바른 통합을 찾은 다음 **[!UICONTROL 보기]**&#x200B;를 선택합니다.

- `clientId`은(는) 무엇입니까? I/O 콘솔에서 이 파일을 복사하여 붙여넣습니다.
- `clientSecret`은(는) 무엇입니까? I/O 콘솔에서 이 파일을 복사하여 붙여넣습니다.

릴리스는 확장 매니페스트에서 `name` 및 `platform` 필드를 읽고 Development 가용성의 일치하는 확장 패키지에 대해 API를 쿼리합니다.
그런 다음 릴리스에서는 비공개 릴리스로 릴리스할 올바른 확장 패키지를 찾았는지 확인하라는 메시지가 표시됩니다.

API를 사용하여 확장을 직접 사용할 수 있는 상태로 릴리스하려면 API 문서에서 [확장 패키지 비공개 릴리스](../../api/endpoints/extension-packages.md/#private-release)에 대한 예제 호출을 참조하십시오.

## 공개 릴리스

비공개 릴리스를 완료하면 Adobe에 공개적으로 릴리스하도록 요청할 수 있습니다.  그러면 공개 카탈로그에서 확장을 사용할 수 있습니다. 모든 데이터 수집 사용자는 모든 속성에 확장을 설치할 수 있습니다.

릴리스 프로세스를 시작하려면 [공개 릴리스 요청 양식](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest)을 작성해 주십시오.
