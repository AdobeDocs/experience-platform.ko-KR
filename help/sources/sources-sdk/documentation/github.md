---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: GitHub 웹 인터페이스를 사용하여 소스 설명서 페이지 만들기
description: 이 문서에서는 GitHub 웹 인터페이스를 사용하여 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법에 대한 단계를 제공합니다.
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# GitHub 웹 인터페이스를 사용하여 소스 설명서 페이지 만들기

이 문서에서는 GitHub 웹 인터페이스를 사용하여 설명서를 작성하고 가져오기 요청(PR)을 제출하는 방법에 대한 단계를 제공합니다.

>[!TIP]
>
>Adobe 기여 안내서의 다음 문서를 사용하여 설명서 프로세스를 추가로 지원할 수 있습니다. <ul><li>[Git 및 Markdown 작성 도구 설치](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=ko)</li><li>[로컬에서 설명서를 위한 Git 리포지토리 설정](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=ko)</li><li>[주요 변경 사항에 대한 GitHub 기여 워크플로](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=ko)</li></ul>

## GitHub 환경 설정

GitHub 환경을 설정하는 첫 번째 단계는 [Adobe Experience Platform GitHub 저장소](https://github.com/AdobeDocs/experience-platform.en)로 이동하는 것입니다.

![platform-repo](../assets/platform-repo.png)

그런 다음 **포크**&#x200B;를 선택합니다.

![포크](../assets/fork.png)

포크가 완료되면 **마스터**&#x200B;를 선택하고 표시되는 드롭다운 메뉴에 새 분기 이름을 입력하십시오. 분기를 설명하는 이름을 지정하십시오. 이 이름은 작업을 포함하는 데 사용됩니다. 그런 다음 **분기 만들기**&#x200B;를 선택하십시오.

![create-branch](../assets/create-branch.png)

포크된 리포지토리의 GitHub 폴더 구조에서 [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create)&#x200B;(으)로 이동한 다음 목록에서 소스에 대한 적절한 범주를 선택합니다. 예를 들어 새 CRM 원본에 대한 설명서를 만드는 경우 **crm**&#x200B;을 선택하십시오.

>[!TIP]
>
>UI에 대한 설명서를 만드는 경우 [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create)&#x200B;(으)로 이동하여 소스에 적합한 범주를 선택합니다. 이미지를 추가하려면 [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create)&#x200B;(으)로 이동한 다음 스크린샷을 `sdk` 폴더에 추가합니다.

![crm](../assets/crm.png)

기존 CRM 소스의 폴더가 표시됩니다. 새 소스에 대한 설명서를 추가하려면 **파일 추가**&#x200B;를 선택한 다음 표시되는 드롭다운 메뉴에서 **새 파일 만들기**&#x200B;를 선택하십시오.

![create-new-file](../assets/create-new-file.png)

소스 파일 이름을 `YOURSOURCE.md`로 지정합니다. 여기서 YOURSOURCE는 Experience Platform의 소스 이름입니다. 예를 들어 회사가 ACME CRM인 경우 파일 이름은 `acme-crm.md`이어야 합니다.

![git-interface](../assets/git-interface.png)

## 소스에 대한 설명서 페이지 작성

새 소스에 대한 설명서를 시작하려면 [소스 설명서 템플릿](./template.md)의 내용을 GitHub 웹 편집기에 붙여 넣으십시오. [여기](../assets/api-template.zip)에서 템플릿을 다운로드할 수도 있습니다.

GitHub 웹 편집기 인터페이스에 복사된 템플릿을 사용하여 템플릿에 설명된 지침에 따라 소스에 대한 관련 정보가 포함된 값을 편집합니다.

![템플릿 붙여넣기](../assets/paste-template.png)

완료되면 분기에서 파일을 커밋합니다.

![커밋](../assets/commit.png)

## 검토를 위해 설명서 제출

파일이 커밋되면 가져오기 요청(PR)을 열어 작업 분기를 Adobe 설명서 저장소의 마스터 분기로 병합할 수 있습니다. 작업 중인 분기가 선택되었는지 확인한 다음 **비교 및 가져오기 요청**&#x200B;을 선택하십시오.

![compare-pr](../assets/compare-pr.png)

기준 및 비교 분기가 올바른지 확인합니다. PR에 업데이트를 설명하는 메모를 추가한 다음 **끌어오기 요청 만들기**&#x200B;를 선택합니다. 이렇게 하면 작업의 작업 분기를 Adobe 저장소의 마스터 분기로 병합하기 위한 PR이 열립니다.

>[!TIP]
>
>Adobe 설명서 팀이 PR을 편집할 수 있도록 **유지 관리자가 편집 허용** 확인란을 선택한 상태로 두십시오.

![create-pr](../assets/create-pr.png)

이때 Adobe 기여자 라이선스 계약(CLA)에 서명하라는 메시지가 표시됩니다. 필수 단계입니다. CLA에 서명한 후 PR 페이지를 새로 고치고 끌어오기 요청을 제출합니다.

https://github.com/AdobeDocs/experience-platform.en에서 가져오기 요청 탭을 검사하여 가져오기 요청이 제출되었는지 확인할 수 있습니다.

![confirm-pr](../assets/confirm-pr.png)
