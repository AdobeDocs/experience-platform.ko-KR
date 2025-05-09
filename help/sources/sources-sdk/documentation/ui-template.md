---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: UI에 대한 셀프서비스 설명서 템플릿
description: Adobe Experience Platform UI를 사용하여 YOURSOURCE 연결을 만드는 방법을 알아봅니다.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 1%

---

# UI에서 *YOURSOURCE* 소스 연결 만들기

*이 서식 파일을 사용할 때 이탤릭체로 된 모든 단락을 바꾸거나 삭제합니다(이 단락부터 시작).*

*페이지 맨 위에 있는 메타데이터(제목 및 설명)를 업데이트하여 시작합니다. 이 페이지에서 UICONTROL의 모든 인스턴스를 무시하십시오. 이것은 기계 번역 프로세스가 페이지를 지원하는 여러 언어로 올바르게 번역할 수 있도록 도와주는 태그입니다. 문서를 제출하면 문서에 태그를 추가합니다.*

이 자습서에서는 Experience Platform 사용자 인터페이스를 사용하여 *YOURSOURCE* 소스 커넥터를 만드는 단계를 제공합니다.

## 개요

*고객에게 제공하는 가치를 포함하여 회사에 대한 간략한 개요를 제공합니다. 자세한 내용을 보려면 제품 설명서 홈 페이지에 대한 링크를 포함하십시오.*

>[!IMPORTANT]
>
>이 원본 커넥터 및 문서 페이지는 *YourSource* 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청이 있으면 *링크 또는 이메일 주소 삽입*&#x200B;을 통해 직접 연락하십시오.

## 전제 조건

*Adobe Experience Platform 사용자 인터페이스에서 소스 설정을 시작하기 전에 고객이 알아야 할 사항에 대한 정보를 이 섹션에 추가합니다. 이 값은*&#x200B;일 수 있습니다.

* *허용 목록에 추가해야 함*
* *전자 메일 해시에 대한 요구 사항*
* *모든 계정 세부 정보*
* *플랫폼에 연결할 인증 자격 증명을 얻는 방법*

### 필요한 자격 증명 수집

*YOURSOURCE*&#x200B;을(를) Experience Platform에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| *자격 증명 원* | *여기에서 원본의 인증 자격 증명에 대한 간단한 설명을 추가하십시오.* | *여기에 원본의 인증 자격 증명의 예제를 추가하십시오* |
| *자격 증명 2* | *여기에서 원본의 인증 자격 증명에 대한 간단한 설명을 추가하십시오.* | *여기에 원본의 인증 자격 증명의 예제를 추가하십시오* |
| *자격 증명 3* | *여기에서 원본의 인증 자격 증명에 대한 간단한 설명을 추가하십시오.* | *여기에 원본의 인증 자격 증명의 예제를 추가하십시오* |

이러한 자격 증명에 대한 자세한 내용은 *YOURSOURCE* 인증 설명서를 참조하십시오. *여기에서 플랫폼의 인증 설명서에 대한 링크를 추가하십시오*.

## *YOURSOURCE* 계정 연결

Experience Platform UI의 왼쪽 탐색 모음에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*YOURSOURCE의 범주* 범주 아래에서 *YOURSOURCE*&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

>[!TIP]
>
>아래에 사용된 스크린샷은 예입니다. 설명서를 만들 때 이미지를 실제 소스의 스크린샷으로 바꾸십시오. 동일한 파일 이름뿐만 아니라 동일한 마크업 패턴 및 색상을 사용할 수 있습니다. 스크린샷에 전체 Experience Platform UI 화면이 캡처되는지 확인하십시오. 스크린샷을 업로드하는 방법에 대한 자세한 내용은 [검토할 문서 제출](./github.md)에 대한 안내서를 참조하십시오.

![카탈로그](../assets/ui/catalog.png)

**[!UICONTROL 원본 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 *YOURSOURCE* 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속하십시오.

![기존](../assets/ui/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 설명(선택 사항) 및 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새로 만들기](../assets/ui/new.png)

## 다음 단계

데이터 흐름을 만드는 나머지 단계에 대한 *워크플로가 모듈화되었습니다. 소스에 대해 수행할 특정 콜아웃이 있는 경우 아래의 추가 리소스 섹션을 참조하십시오.*

이 자습서를 따라 *YOURSOURCE* 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html?lang=ko)할 수 있습니다.

## 추가 리소스

*제품 설명서나 고객이 성공하기 위해 중요하다고 생각하는 다른 단계, 스크린샷, 뉘앙스에 대한 추가 링크를 제공할 수 있는 선택적 섹션입니다. 이 섹션을 사용하여 원본의 전체 워크플로에 대한 정보 또는 팁을 추가할 수 있습니다. 특히 최종 사용자에게 표시될 수 있는 특정 &quot;gotchas&quot;가 있는 경우에 유용합니다.*
