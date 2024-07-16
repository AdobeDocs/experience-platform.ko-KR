---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;fullName;xdm:fullName;개인 이름;이름;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 개인 이름 데이터 유형
description: 개인 이름 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# [!UICONTROL 사용자 이름] 데이터 형식

[!UICONTROL 개인 이름]은(는) 개인의 전체 이름을 설명하는 표준 XDM 데이터 형식입니다. 이름 구조에 대한 규칙은 언어와 문화권에 따라 다르므로 항상 이 데이터 형식을 사용하여 이름을 모델링해야 합니다.

또한 데이터 유형은 공식 또는 비공식 인사말 생성과 같이 전체 이름의 단편만 사용해야 하는 상황에서 사용할 수 있는 여러 선택적 속성을 제공합니다.

<img src="../images/data-types/person-name.png" width="500" /><br />

| 속성 | 설명 |
| --- | --- |
| `courtesyTitle` | 사용자 제목, 경칭 또는 경어의 약어입니다(예: `Mr.`, `Miss.` 또는 `Dr.`). |
| `firstName` | 가장 일반적으로 수락된 언어로 작성된 이름의 첫 번째 세그먼트. |
| `fullName` | 가장 일반적으로 수락된 언어로 작성된 개인의 전체 이름. |
| `lastName` | 가장 일반적으로 수락된 언어로 작성된 이름의 마지막 세그먼트. |
| `middleName` | 이름과 성 사이에 제공되는 중간, 대체 또는 추가 이름. |
| `suffix` | 추가 정보를 제공하기 위해 사용자 이름 뒤에 제공되는 글자 그룹(예: `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III` 등). |

{style="table-layout:auto"}

개인 이름 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
