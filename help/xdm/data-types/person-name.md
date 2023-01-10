---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;전체 이름;xdm:fullName;이름;이름;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 개인 이름 데이터 유형
description: 이 문서에서는 개인 이름 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# [!UICONTROL 개인 이름] 데이터 유형

[!UICONTROL 개인 이름] 는 개인의 전체 이름을 설명하는 표준 XDM 데이터 유형입니다. 이름 구조에 대한 규칙은 언어와 문화권에서 광범위하게 서로 다르므로 항상 이 데이터 유형을 사용하여 이름을 모델링해야 합니다.

또한 데이터 유형에서는 형식이나 비공식적 인사말 생성과 같이 전체 이름의 조각만 사용해야 하는 상황에서 사용할 수 있는 여러 가지 선택적 속성을 제공합니다.

<img src="../images/data-types/person-name.png" width="500" /><br />

| 속성 | 설명 |
| --- | --- |
| `courtesyTitle` | 개인의 제목, 존칭이나 인사말(예: `Mr.`, `Miss.`, 또는 `Dr.`). |
| `firstName` | 작성 순서에서 이름의 첫 번째 세그먼트는 이름의 언어로 가장 일반적으로 사용됩니다. |
| `fullName` | 그 사람의 전체 이름은 그 이름의 언어로 가장 흔하게 받아들여지고 있다. |
| `lastName` | 이름 언어로 가장 일반적으로 허용되는 쓰기 순서의 이름 마지막 세그먼트입니다. |
| `middleName` | 이름과 성 사이에 제공된 중간, 대체 또는 추가 이름 |
| `suffix` | 개인 이름 뒤에 제공되는 문자 그룹(예: `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, 등). |

{style=&quot;table-layout:auto&quot;}

개인 이름 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
